---
layout: post
title: "Basic scull build from scratch"
date: 2022-02-07 14:30:00 +0800
categories: note
tags: [LDD3]
---

## Flowchart  
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/basic_scull_build_from_scratch_flowchart.png?raw=true)

## scull.c  
``` c
#include <linux/init.h>		/* essential */
#include <linux/module.h>	/* essential */

#include <linux/fs.h>		/* file system */
#include <linux/types.h>	/* dev_t */
#include <linux/errno.h>	/* error code */
#include <linux/cdev.h>		/* char device */
#include <linux/slab.h>		/* kmalloc, kfree */

#include "scull.h"

unsigned char major = 0;
unsigned char minor = 0;
unsigned char dev_amt = 1;
const unsigned short quantum_size = SCULL_QUANTUM;
const unsigned short qset_size = SCULL_QSET;

struct Scull *scull = NULL;

void scull_trim(struct Scull *scull) {
	struct Qset *next=NULL, *dptr=NULL;
	int qset = scull->qset, i=0;
	DBGMSG("[%s - %s - %d] Enter.\n", __FILE__, __func__, __LINE__);

	DBGMSG("[%s - %s - %d] clear all the list items.\n", __FILE__, __func__, __LINE__);
	for (dptr=scull->data; dptr; dptr=next) {
		if (dptr->data) {
			for (i=0; i<qset; i++)
				kfree(dptr->data[i]);
			kfree(dptr->data);
			dptr->data = NULL;
		}
		next = dptr->next;
		kfree(dptr);
	}

	DBGMSG("[%s - %s - %d] reset scull parameters.\n", __FILE__, __func__, __LINE__);
	scull->size = 0;
	scull->quantum = quantum_size;
	scull->qset = qset_size;
	scull->data = NULL;

	DBGMSG("[%s - %s - %d] Leave.\n", __FILE__, __func__, __LINE__);
}

int scull_open(struct inode *inode, struct file *filp) {
	struct Scull *dev;
	DBGMSG("[%s - %s - %d] Enter.\n", __FILE__, __func__, __LINE__);
	
	DBGMSG("[%s - %s - %d] Reserve char device for future use.\n", __FILE__, __func__, __LINE__);
	dev = container_of(inode->i_cdev, struct Scull, cdev);
	filp->private_data = dev;

	DBGMSG("[%s - %s - %d] do scull_trim() if open was write-only.\n", __FILE__, __func__, __LINE__);
	if ( (filp->f_flags & O_ACCMODE) == O_WRONLY) {
		if (mutex_lock_interruptible(&dev->lock)) {
			DBGMSG("[%s - %s - %d] mutex was interruptible.\n", __FILE__, __func__, __LINE__);
			return -ERESTARTSYS;
		}
		scull_trim(dev);
		mutex_unlock(&dev->lock);
	}

	DBGMSG("[%s - %s - %d] Leave.\n", __FILE__, __func__, __LINE__);
	return 0;
}

int scull_release(struct inode *inode, struct file *filp) {
	DBGMSG("[%s - %s - %d] Enter.\n", __FILE__, __func__, __LINE__);
	DBGMSG("[%s - %s - %d] Leave.\n", __FILE__, __func__, __LINE__);
	return 0;
}

struct Qset *scull_follow(struct Scull *dev, int n) {
	struct Qset *qs = dev->data;
	DBGMSG("[%s - %s - %d] Enter.\n", __FILE__, __func__, __LINE__);

	/* Allocate first qset explicitly if need be */
	if (!qs) {
		DBGMSG("[%s - %s - %d] Allocate first qset explicitly.\n", __FILE__, __func__, __LINE__);
		qs = dev->data = kmalloc(sizeof(struct Qset), GFP_KERNEL);
		if (qs == NULL) {
			DBGMSG("[%s - %s - %d] can't kmalloc qset.\n", __FILE__, __func__, __LINE__);
			return NULL;
		}
		memset(qs, 0, sizeof(struct Qset));
	}

	DBGMSG("[%s - %s - %d] Follow the list.\n", __FILE__, __func__, __LINE__);
	while (n--) {
		if (!qs->next) {
			qs->next = kmalloc(sizeof(struct Qset), GFP_KERNEL);
			if (qs->next == NULL) {
				DBGMSG("[%s - %s - %d] can't kmalloc qs->next.\n", __FILE__, __func__, __LINE__);
				return NULL;
			}
			memset(qs, 0, sizeof(struct Qset));
		}
		qs = qs->next;
	}

	DBGMSG("[%s - %s - %d] Leave.\n", __FILE__, __func__, __LINE__);
	return qs;
}

ssize_t scull_read(struct file *filp, char __user *buf, size_t count, loff_t *f_pos) {
	struct Scull *dev = filp->private_data;
	struct Qset *dptr = NULL;
	int quantum = dev->quantum, qset = dev->qset;
	int itemsize = quantum * qset;
	int item, rest, s_pos, q_pos;
	ssize_t res = 0;
	DBGMSG("[%s - %s - %d] Enter.\n", __FILE__, __func__, __LINE__);

	if (mutex_lock_interruptible(&dev->lock)) {
		DBGMSG("[%s - %s - %d] mutex was interruptible.\n", __FILE__, __func__, __LINE__);
		return -ERESTARTSYS;
	}
	if (dev->size <= *f_pos) {
		DBGMSG("[%s - %s - %d] read outside of file.\n", __FILE__, __func__, __LINE__);
		goto out;
	}
	if (dev->size < *f_pos + count)
		count = dev->size - *f_pos;

	DBGMSG("[%s - %s - %d] find listitem, qset index, and offset in the quantum.\n", __FILE__, __func__, __LINE__);
	item = (long)*f_pos / itemsize;
	rest = (long)*f_pos % itemsize;
	s_pos = rest / quantum; q_pos = rest % quantum;

	DBGMSG("[%s - %s - %d] follow the list up to the right position.\n", __FILE__, __func__, __LINE__);
	dptr = scull_follow(dev, item);
	if (dptr == NULL || !dptr->data || !dptr->data[s_pos]) {
		DBGMSG("[%s - %s - %d] scull_follow failed.\n", __FILE__, __func__, __LINE__);
		goto out;
	}

	/* read only up to the end of this quantum */
	if (quantum - q_pos < count)
		count = quantum - q_pos;

	if (copy_to_user(buf, dptr->data[s_pos]+q_pos, count)) {
		DBGMSG("[%s - %s - %d] copy_to_user failed.\n", __FILE__, __func__, __LINE__);
		res = -EFAULT;
		goto out;
	}
	DBGMSG("[%s - %s - %d] update f_pos.\n", __FILE__, __func__, __LINE__);
	*f_pos += count;
	res = count;

out:
	DBGMSG("[%s - %s - %d] out.\n", __FILE__, __func__, __LINE__);
	mutex_unlock(&dev->lock);
	return res;
}

ssize_t scull_write(struct file *filp, const char __user *buf, size_t count, loff_t *f_pos) {
	struct Scull *dev = filp->private_data;
	struct Qset *dptr = NULL;
	int quantum = dev->quantum, qset = dev->qset;
	int itemsize = quantum * qset;
	int item, rest, s_pos, q_pos;
	ssize_t res = -ENOMEM;
	DBGMSG("[%s - %s - %d] Enter.\n", __FILE__, __func__, __LINE__);

	if (mutex_lock_interruptible(&dev->lock)) {
		DBGMSG("[%s - %s - %d] mutex was interruptible.\n", __FILE__, __func__, __LINE__);
		return -ERESTARTSYS;
	}

	DBGMSG("[%s - %s - %d] find listitem, qset index and offset in the quantum.\n", __FILE__, __func__, __LINE__);
	item = (long)*f_pos / itemsize;
	rest = (long)*f_pos % itemsize;
	s_pos = rest / quantum; q_pos = rest % quantum;

	DBGMSG("[%s - %s - %d] follow the list up to the right position.\n", __FILE__, __func__, __LINE__);
	dptr = scull_follow(dev, item);
	if (dptr == NULL) {
		DBGMSG("[%s - %s - %d] dptr is NULL.\n", __FILE__, __func__, __LINE__);
		goto out;
	}
	if (!dptr->data) {
		dptr->data = kmalloc(qset*sizeof(char *), GFP_KERNEL);
		if (!dptr->data) {
			DBGMSG("[%s - %s - %d] can't kmalloc dptr->data.\n", __FILE__, __func__, __LINE__);
			goto out;
		}
		memset(dptr->data, 0, qset*sizeof(char *));
	}
	if (!dptr->data[s_pos]) {
		dptr->data[s_pos] = kmalloc(quantum, GFP_KERNEL);
		if (!dptr->data[s_pos]) {
			DBGMSG("[%s - %s - %d] can't kmalloc dptr->data[s_pos].\n", __FILE__, __func__, __LINE__);
			goto out;
		}
		memset(dptr->data[s_pos], 0, quantum);
	}
	
	/* write only up to the end of this quantum */
	if (quantum - q_pos < count)
		count = quantum - q_pos;

	if (copy_from_user(dptr->data[s_pos]+q_pos, buf, count)) {
		DBGMSG("[%s - %s - %d] copy_from_user failed.\n", __FILE__, __func__, __LINE__);
		res = -EFAULT;
		goto out;
	}
	DBGMSG("[%s - %s - %d] update f_pos.\n", __FILE__, __func__, __LINE__);
	*f_pos += count;
	res = count;

	if (dev->size < *f_pos) {
		DBGMSG("[%s - %s - %d] update device size.\n", __FILE__, __func__, __LINE__);
		dev->size = *f_pos;
	}

out:
	DBGMSG("[%s - %s - %d] out.\n", __FILE__, __func__, __LINE__);
	mutex_unlock(&dev->lock);
	return res;
}

struct file_operations scull_fops = {
	.owner = THIS_MODULE,
	.open = scull_open,
	.release = scull_release,
	.read = scull_read,
	.write = scull_write,
};

void scull_cleanup_module(void) {
	dev_t dev_num = MKDEV(major, minor);
	DBGMSG("[%s - %s - %d] Enter.\n", __FILE__, __func__, __LINE__);
	
	DBGMSG("[%s - %s - %d] free scull memory.\n", __FILE__, __func__, __LINE__);
	if (scull) {
		scull_trim(scull);
		cdev_del(&scull->cdev);
	}
	kfree(scull);
	
	DBGMSG("[%s - %s - %d] free device number.\n", __FILE__, __func__, __LINE__);
	unregister_chrdev_region(dev_num, dev_amt);

	DBGMSG("[%s - %s - %d] Leave.\n", __FILE__, __func__, __LINE__);
}

static int init_func(void) {
	int res = 0;
	dev_t dev_num = 0;
	DBGMSG("[%s - %s - %d] Enter.\n", __FILE__, __func__, __LINE__);
	
	DBGMSG("[%s - %s - %d] get device number dynamically.\n", __FILE__, __func__, __LINE__);
	res = alloc_chrdev_region(&dev_num, minor, 1, "scull");
	major = MAJOR(dev_num);
	if (res < 0) {
		DBGMSG("[%s - %s - %d] can't get major.\n", __FILE__, __func__, __LINE__);
		return res;
	}
	
	DBGMSG("[%s - %s - %d] allocate char device memory.\n", __FILE__, __func__, __LINE__);
	scull = kmalloc(dev_amt * sizeof(struct Scull), GFP_KERNEL);
	if (!scull) {
		DBGMSG("[%s - %s - %d] can't kmalloc scull.\n", __FILE__, __func__, __LINE__);
		res = -ENOMEM;
		goto fail;
	}
	memset(scull, 0, dev_amt * sizeof(struct Scull));

	DBGMSG("[%s - %s - %d] initialize scull.\n", __FILE__, __func__, __LINE__);
	scull->quantum = quantum_size;
	scull->qset = qset_size;
	mutex_init(&scull->lock);
	cdev_init(&scull->cdev, &scull_fops);
	scull->cdev.owner = THIS_MODULE;
	res = cdev_add(&scull->cdev, dev_num, 1);
	if (res) {
		DBGMSG("[%s - %s - %d] Error %d adding scull.\n", __FILE__, __func__, __LINE__, res);
		goto fail;
	}

	return 0;
	
fail:
	scull_cleanup_module();
	return res;
}

module_init(init_func);
module_exit(scull_cleanup_module);

MODULE_LICENSE("GPL v2");

```

## scull.h  
``` c
#ifndef __SCULL_H__
#define __SCULL_H__

/*
 * Macros to help debugging 
 */
#define SCULL_DEBUG

#undef DBGMSG
#ifdef SCULL_DEBUG
#  ifdef __KERNEL__
     /* debug message in kernel space */
#    define DBGMSG(fmt, args...) printk(KERN_DEBUG "DBGMSG: " fmt, ## args)
#  else
	 /* debug message in user space */
#    define DBGMSG(fmt, args...) fprintf(stderr, fmt, ## args)
#  endif
#else
#  define DBGMSG(fmt, args...)
#endif

#ifndef SCULL_QUANTUM
#define SCULL_QUANTUM 4000
#endif

#ifndef SCULL_QSET
#define SCULL_QSET 1000
#endif

struct Qset {
	void **data;
	struct Qset *next;
};

struct Scull {
	struct Qset *data;	/* Pointer to first quantum set */
	int quantum;		/* the current quantum size */
	int qset;			/* the current array size */
	unsigned long size;	/* amount of data stored here */
	struct mutex lock;	/* mutual exclusion semaphore */
	struct cdev cdev;	/* Char device structure */
};

#endif /* __SCULL_H__ */

```

## Makefile  
``` make
# if KERNELRELEASE is defined, we've been invoked from the kernel buils system and can use its language.
ifneq ($(KERNELRELEASE),)

	obj-m := scull.o

else

	KERNELDIR ?= /lib/modules/$(shell uname -r)/build
	PWD := $(shell pwd)

default:
	$(MAKE) -C $(KERNELDIR) M=$(PWD) modules

endif

clean:
	rm -f *.mod.c *.o *.mod *.ko *.order *.symvers

```

## scull_load.sh  
``` sh
#!/bin/sh

# Group: since distributions do it differently, look for wheel or use staff
if grep -q '^staff:' /etc/group; then
	group="staff"
else
	group="wheel"
fi

insmod ./scull.ko $* || exit 1

major=$(awk "\$2==\"scull\" {print \$1}" /proc/devices)

rm -f /dev/scull
mknod /dev/scull c $major 0
chgrp $group /dev/scull
chmod 644 /dev/scull

```

## scull_unload.sh  
``` sh
#!/bin/sh

rmmod scull $* || exit 1

rm -f /dev/scull

```