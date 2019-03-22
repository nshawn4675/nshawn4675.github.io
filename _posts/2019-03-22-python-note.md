---
layout: post
title:  "python note"
date:   2019-03-22 01:51:31 +0800
categories: jekyll update
---
<h3><b>一切都從這裡開始</b></h3>
{% highlight python %}
if __name__ == '__main__':
	# 開始你想做的事, python以縮排當作'{}', 句尾不用加';'
	print("Hello Python")

	# 宣告變數，直接給值即可
	x = 5		# 自動轉型為int
	y = "Shawn"	# 自動轉型為str

	# 也可強制轉型
	z = float("2")	# z = 2.0
	a = str(123)	# a = "123"

{% endhighlight %}

<h3><b>Function相關</b></h3>
{% highlight python %}
# 宣告function
def function_name(arg1, arg2, arg3 = default_value):
	# 做function該做的事
	return (arg1 + arg2)

# lambda，神奇的小玩意兒，可數個arg，但只能做一行的事
def myfunc(n):
	return lambda a : a * n

mydoubler = myfunc(2)	# 將2傳給a, double效果
mytripler = myfunc(3)	# 將3傳給a, triple效果

print(mydoubler(11))	# 會印出 22
print(mytripler(11))	# 會印出 33
{% endhighlight %}

<h3><b>常用的Functions</b></h3>
{% highlight python %}
# Type
type(value)		# 回傳目前value所對應的type

# Ascii
chr(ascii)		# 將ascii轉為相對應的char
ord(char)		# 將char轉為相對應的ascii

# Array (List)
array = [value1, something2, ...]	#索引值由 0 起算
len(array)		# 計算有幾個元素
array.append(value)	# 將value附加入array尾端
array.insert(idx, value)# 將value插入特定位置
array.remove(value)	# 將與value相符的元素刪掉
array.pop()		# 將最後一個元素刪掉且回傳
array.clear()		# 清空array
array.index(value)	# 回傳符合value的索引值, 從頭開始找的第一個
max(array)		# 回傳其中的最大值
range(value)		# 回傳一個 0 ~ value-1 的陣列
# tuple是無法被修改的

# set
a_set = {value1, something2, ...}
a_set.add(value)	# 將value加入set中
a_set.update([value1, value2, ...])	# 將數個值加入set中

# dictionary
a_dict = {key1:value1, key2:value2, ...}
x = a_dict[key1]	# 抓key1的value
x = a_dict.get(key1)	# 抓key1的value
a_dict[key1] = value5 	# 改key1的value為value5
a_dict.values()		# 以array回傳所有的value
a_dict.items()		# 以array回傳所有的item
a_dict[new1] = new_val	# 新增key & value
# 若要修改key的value，也是用相同方法
a_dict.pop(key)		# 將key相符的item刪掉
a_dict.popitem()	# 將最後一個item刪掉

# str
str.lower()		# 將str全轉為小寫
str.strip()		# 將str頭尾多餘的空白刪掉
str.replace(chr1, chr2)	# 將str中的chr1以chr2代替
str.split(chr)		# 以chr為基準, 切分為數個子字串

# char
char.isupper()		# 是否為「大寫」
char.islower()		# 是否為「小寫」
char.isdigit()		# 是否為「數字」
{% endhighlight %}

<h3><b>運算相關</b></h3>
{% highlight python %}
x**y	# x的y次方
a in b	# a是否存在b中
"""
Python沒有++、--，只能+=1、-=1
Python沒有||、&&，只能or、and
(多行註解)
"""
{% endhighlight %}

<h3><b>flow control相關</b></h3>
{% highlight python %}
if condition1:
	pass		# pass有留白的效果
elif condition2:
	pass
else:
	pass

for i in range(10):	# 從 0 ~ 9
	pass

for i in "apple":	#i依序為：a, p, p, l, e
	pass

while condition:
	pass

{% endhighlight %}

<h3><b>Class相關</b></h3>
{% highlight python %}
class Person:
	def __init__(self, name, age):
		# self指的是class它自己，可以用其它名字代替，但一定要是第一個arg
		self.name = name
		self.age = age

	def myfunc(self):
		print("Hello my name is " + self.name)

p1 = Person("John", 36)
p1.myfunc()

# 繼承
class Student(Person):
	pass

x = Student("Mike", 18)
x.myfunc()
{% endhighlight %}

<h3><b>Try Except相關</b></h3>
{% highlight python %}
try:
	# 要做的事情
	print(x)
except NameError:
	# 已知特定意外處理
	print("Variable x is not defined")
except:
	# 未知意外處理
	print("Something else went wrong")
else:
	# 都沒有意外發生的話
	print("Nothing went wrong")
finally:
	# 不管有無意外發生，最後一定會做的事
	print("The 'try except' is finished")
{% endhighlight %}

<h3><b>Module相關</b></h3>
{% highlight python %}
# 相當於library，有一mymodule.py內容如下
def greeting(name):
	print("Hello, " + name)

person1 = {
	"name": "John",
	"age": 36,
	"country": "Norway"
}
{% endhighlight %}
{% highlight python %}
# 則可以引入它來使用
import mymodule

mymodule.greeting("Jonathan")
{% endhighlight %}
{% highlight python %}
# 也可引入後，換個名字使用
import mymodule as mx

a = mx.person1["age"]
print(a)	# 印出 36
{% endhighlight %}
{% highlight python %}
# 若只想引入module中的某部份
from mymodule import person1

print(person1["age"])	# 印出 36
{% endhighlight %}