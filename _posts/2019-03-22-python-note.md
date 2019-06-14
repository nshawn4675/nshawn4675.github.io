---
layout: post
title:  "python note"
date:   2019-03-22 01:51:31 +0800
categories: jekyll update
---
## **一切都從這裡開始**
```python
if __name__ == '__main__':
	# 開始你想做的事, python以縮排當作'{}', 句尾不用加';'
	print("Hello Python")

	# 宣告變數，直接給值即可
	x = 5		# 自動轉型為int
	y = "Shawn"	# 自動轉型為str  

	# 也可強制轉型  
	z = float("2")	# z = 2.0
	a = str(123)	# a = "123"

```

## **Function相關**
```python
# 宣告function
def function_name(arg1, arg2, arg3 = default_value):
	# 做function該做的事
	return (arg1 + arg2)

# lambda
lambda arg1, arg2 : return_value

# map, 批次使用function
def add(a, b):
	return a+b
list(map(add, [1,2,3], [4,5,6])) 
# 使用add數次，傳入參數個別為1, 4 ; 2, 5 ; ,3, 6
# 得到一個map object, 將其轉成list會得到[5, 7, 9]

def myfunc(n):
  return lambda a : a * n

mydoubler = myfunc(2)	# 將 2 傳給 a , 會得到double的效果
mytripler = myfunc(3)	# 將 3 傳給 a , 會得到triple的效果

print(mydoubler(11))	# 會印出 22
print(mytripler(11))	# 會印出 33
```

## **Decorator**
```python
# Decorator用以在原function前後做額外事情，包裝、點綴function

def deco_func(func): # 以欲點綴的func為arg帶入
	def wrapper(*arg): # *arg from origin func
		# do extra things
		res = func(*arg) # origin func return
		# do extra things
		return res
	return wrapper

@deco_func
def function(arg):
	# do something
	return res

function(arg)
```

## **常用的Functions**
```python
# Type
type(value)		# 回傳目前 value 所對應的 type

# Ascii
chr(ascii)		# 將 ascii 轉為相對應的 char
ord(char)		# 將 char 轉為相對應的 ascii

# Array (List)
array = [value1, something2, ...]	#索引值由 0 起算
len(array)		# 計算有幾個元素
array.append(value)	# 將 value 附加入 array 尾端
array.insert(idx, value)# 將 value 插入特定位置
array.remove(value)	# 將與 value 相符的元素刪掉
array.pop()		# 將最後一個元素刪掉且回傳
array.clear()		# 清空 array
array.index(value)	# 回傳符合 value 的索引值, 從頭開始找的第一個
max(array)		# 回傳其中的最大值
range(value)		# 回傳一個 0 ~ value-1 的陣列
# tuple是無法被修改的

# set
a_set = {value1, something2, ...}
a_set.add(value)	# 將 value 加入 set 中
a_set.update([value1, value2, ...])	# 將數個值加入 set 中

# dictionary
a_dict = {key1:value1, key2:value2, ...}
x = a_dict[key1]	# 抓 key1 的 value
x = a_dict.get(key1)	# 抓 key1 的 value
a_dict[key1] = value5 	# 改 key1 的 value 為 value5
a_dict.values()		# 以 array 回傳所有的 value
a_dict.items()		# 以 array 回傳所有的 item
a_dict[new1] = new_val	# 新增 key & value
# 若要修改key的value，也是用相同方法
a_dict.pop(key)		# 將 key 相符的 item 刪掉
a_dict.popitem()	# 將最後一個 item 刪掉

# str
str.lower()		# 將 str 全轉為小寫
str.strip()		# 將 str 頭尾多餘的空白刪掉
str.replace(chr1, chr2)	# 將 str 中的 chr1 以 chr2 代替
str.split(chr)		# 以 chr 為基準, 切分為數個子字串

# char
char.isupper()		# 是否為「大寫」
char.islower()		# 是否為「小寫」
char.isdigit()		# 是否為「數字」
```

## **運算相關**
```python
# 三元運算子
i = j if condition else k
# 相當於
if condition:
	i = j
else:
	i = k

x**y	# x 的 y 次方
a in b	# a 是否存在 b 中
"""
Python沒有++、--，只能 +=1 、 -=1
Python沒有||、&&，只能 or 、 and
(多行註解)
"""
```

## **flow control相關**
```python
if condition1:
	pass		# pass 有留白的效果
elif condition2:
	pass
else:
	pass

for i in range(10):	# 從 0 ~ 9
	pass

for i in "apple":	# i 依序為：a, p, p, l, e
	pass

while condition:
	pass

```

## **Class相關**
```python
class Person:
	def __init__(self, name, age):
		# self 指的是 class 它自己，可以用其它名字代替，但一定要是第一個 arg
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
```

## **Try Except相關**
```python
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
```

## **Module相關**
```python
# 相當於 library , 若有一 mymodule.py 內容如下
def greeting(name):
	print("Hello, " + name)

person1 = {
	"name": "John",
	"age": 36,
	"country": "Norway"
}
```
```python
# 則可以引入它來使用
import mymodule

mymodule.greeting("Jonathan")
```
```python
# 也可引入後，換個名字使用
import mymodule as mx

a = mx.person1["age"]
print(a)	# 印出 36
```
```python
# 若只想引入 module 其中的某部份
from mymodule import person1

print(person1["age"])	# 印出 36
```
