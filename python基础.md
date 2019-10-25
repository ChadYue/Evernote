# 变量类型

- 数字型:

  ​	整型(int)

  ​	浮点型(float)

  ​	布尔型(bool)

- 非数学型:

  ​	字符串(String)

  ​	列表(List)

  ​	元组(Tuple)

  ​	字典(Dictionary)

### Number（数字）

数字数据类型用于存储数值,数字之间可以直接计算.

- int（有符号整型）
- long（长整型[也可以代表八进制和十六进制]）
- float（浮点型）
- complex（复数）

|  int   |         long          |   float    |  complex   |
| :----: | :-------------------: | :--------: | :--------: |
|   10   |       51924361L       |    0.0     |   3.14j    |
|  100   |       -0x19323L       |   15.20    |    45.j    |
|  -786  |         0122L         |   -21.9    | 9.322e-36j |
|  080   | 0xDEFABCECBDAECBFBAEl |  32.3e+18  |   .876j    |
| -0490  |     535633629843L     |    -90.    | -.6545+0J  |
| -0x260 |    -052318172735L     | -32.54e100 |   3e+26J   |
|  0x69  |    -4721885298529L    |  70.2E-12  |  4.53e-7j  |

### String（字符串）

字符串或串(String)是由数字、字母、下划线组成的一串字符。

##### 字符串取值顺序

- 从左到右索引默认0开始的，最大范围是字符串长度少1
- 从右到左索引默认-1开始的，最大范围是字符串开头 

##### 字符串拼接规则

- 利用+拼接生成新的字符

```
first_name = '三'
last_name = '张'
print(first_name + last_name)
>>>三张
```

- 利用*重复拼接相同字符

```
first_name = '三'
print(first_name * 10)
>>>三三三三三三三三三三
```

若需进行字符串与数字型变量进行其他计算需将数字型变量强制转换成字符串类型

```
first_name = '三'
x = 10
print(str(x) + first_name)
>>>10三
```



# 字符串格式化

- %s,%08d,%d,%06d,%.2f,%%
- {} '含有{}的字符串'.format(参数)（{}内可以加序号，序号由0开始）
- f'字符串{变量的名字}'



# 变量引用

人们经常使用“变量是盒子这样的比喻，但是这有碍于理解面向对象语言中的引用式变量。Python变量类似于Java中的引用式变量，因此最好把它们理解为附加在对象上的标注或便签。

在示例中所示的交互式控制台中，无法使用“变量是盒子’做解释。示意图说明了在Python中为什么不能使用盒子比喻，而便签则指出了变量的正确工作方式。

变量a和b引用同一个列表，而不是那个列表的副本

```
a = [1,2,3]
b = a
a.append(4)
print(b)
[1,2,3,4]
```

如果把变量想象为盒子，那么无法解释Python中的赋值;应该把变量视作便利贴，这样示例中的行为就好解释了



### 随机数

在一个范围里随机取一个数

```
a = random.randint(12,20)
print(a)
>>>18
>>>15
>>>16
```

# 列表与元组

### 列表

列表是python中内置有序可变序列，列表的所有元素放在一对中括号“[]”中，并使用逗号分隔开；

一个列表中的数据类型可以各不相同

```
list1 = [1,2.3,'张三',[1,2,'sss']]
print(list1)
>>>[1, 2.3, '张三', [1, 2, 'sss']]
```

## 添加

#### append

向列表尾部追加一个元素，不改变其内存首地址，属于原地操作。

```
x = [1,2,3]
print(x)
x.append(4)
print(x)
>>>[1, 2, 3]      
>>>[1, 2, 3, 4]
```

#### insert

向列表插入一个元素，不改变其内存首地址，属于原地操作。

```
x = [1,3,4]
print(x)
x.insert(1,2)
print(x)
>>>[1, 3, 4]
>>>[1, 2, 3, 4]
```

#### extend

将另一个迭代对象的所以元素添加至该列表对象尾部，不改变其内容首地址，属于原地操作。

```
x = [1,2,3]
print(x)
x.extend([5,6,7])
print(x)
>>>[1, 2, 3]
>>>[1, 2, 3, 5, 6, 7]
```

## "+","*"

并不是真的为列表添加元素，而是创建一个新列表，不属于原地操作，而是返回新列表。

```
x = [9,6,7,5,2,4,8,3,1]
y = x + [10]
print(y)
a = x * 2
print(a)
print(x)
>>>[9, 6, 7, 5, 2, 4, 8, 3, 1, 10]
>>>[9, 6, 7, 5, 2, 4, 8, 3, 1, 9, 6, 7, 5, 2, 4, 8, 3, 1]
>>>[9, 6, 7, 5, 2, 4, 8, 3, 1]
```

## 删除

#### pop

使用列表的pop()方法删除并返回指定(默认为最后一个)位置上的元素,如果给定的索引超出列表的范围则抛出异常.

```
x = [1,2,3,4]
pos = x.pop(0)
print(x)
print(pos)
>>>[2, 3, 4]
>>>1
```

#### remove

删除首次出现的指定元素,如果列表中不存在要删除的元素,则抛出异常

```
x = [1,2,3,4]
print(x)
x.remove(3)
print(x)
>>>[1, 2, 3, 4]
>>>[1, 2, 4]
```

#### clear

清空列表

```
x = [1,2,3,4]
print(x)
x.clear()
print(x)
>>>[1, 2, 3, 4]
>>>[]
```

#### del

删除列表中的指定位置上的元素

```
x = [1,2,3,4]
print(x)
del x[1]
print(x)
>>>[1, 2, 3, 4]
>>>[1, 3, 4]
```

## 访问与计数

#### count

统计指定元素在列表中出现的次数

```
x = [1,2,3,3,4,5,6,7,3]
a = x.count(3)
print(a)
print(x.count(10))
>>>3
>>>0
```

#### index

获取指定元素首次出现的下标，若列表对象中不存在指定的元素会报错

```
x = [1,2,3,3,4,5,6,7,3]
print(x.index(3))
>>>2
```

#### in

测试列表中是否存在某元素

```
x = [1,2,3,3,4,5,6,7,3]
a = 5 in x
print(a)
>>>True
```

### 顺序排列

#### sort

按照指定规则对所有元素进行排列，默认规则是直接比较元素大小

```
x = [1,2,3,3,4,5,6,7,3]
x.sort()
print(x)
x.sort(reverse=True)
print(x)
>>>[1, 2, 3, 3, 3, 4, 5, 6, 7]
>>>[7, 6, 5, 4, 3, 3, 3, 2, 1]
```

#### reverse

返回一个逆序排列后的迭代对象,不对原列表做任何改变

```
x = [1,2,3,4]
x.reverse()
print(x)
>>>[4, 3, 2, 1]
>>>[1, 2, 3, 4]
```

#### sorted

使用内置函数sorted对列表进行排序并返回新列表,不对原列表做任何改变

```
x = [9,6,7,5,2,4,8,3,1]
print(sorted(x))
print(sorted(x,reverse = True))
print(x)
>>>[1, 2, 3, 4, 5, 6, 7, 8, 9]
>>>[9, 8, 7, 6, 5, 4, 3, 2, 1]
>>>[9, 6, 7, 5, 2, 4, 8, 3, 1]
```

#### reversed

返回一个逆序排列后的迭代对象，不对原列表做任何改变

```
alist = [1,23,55,469,748,25,55,51,21,54]
print(list(reversed(alist)))
print(alist)
>>>[54, 21, 51, 55, 25, 748, 469, 55, 23, 1]
>>>[1, 23, 55, 469, 748, 25, 55, 51, 21, 54]
```

## 常用内置函数

#### len()

返回列表中的元素个数，同样适用于元组、字典、集合、字符串等。

```
alist = [1,23,55,469,748,25,55,51,21,54]
print(len(alist))
>>>10
```

#### max()、min()

返回列表中的最大或最小元素同样适用于元组、字典、集合、字符串等。

```
alist = [1,23,55,469,748,25,55,51,21,54]
print(max(alist))
print(min(alist))
>>>748
>>>1
```

#### sum()

对列表的元素进行求和计算

```
alist = [1,23,55,469,748,25,55,51,21,54]
print(sum(alist))
>>>1502
```

#### zip()

返回可迭代的zip对象

```
a = [1,3,5,7]
b = [2,4,6,8]
c = zip(a,b)
print(c)
print(type(c))
print(list(c))
>>><zip object at 0x000000000286D2C8>
>>><class 'zip'>
>>>[(1, 2), (3, 4), (5, 6), (7, 8)]
```

#### enumerate()

枚举列表元素，返回枚举对象，其中每个元素为包含下标和值的元组。该函数对元组、字符串同样有效。

```
for un in enumerate('@##$$%ERDSf.,'):
    print(un)
>>>(0, '@')
>>>(1, '#')
>>>(2, '#')
>>>(3, '$')
>>>(4, '$')
>>>(5, '%')
>>>(6, 'E')
>>>(7, 'R')
>>>(8, 'D')
>>>(9, 'S')
>>>(10, 'f')
>>>(11, '.')
>>>(12, ',')
```

#### 三种遍历方式

```
a = ('a','s','d','f','g','h','j','k','l')
for i in a:
    print(i)
for i in range(len(a)):
    print(a[i])
for ele,i in enumerate(a):
    print(i)
>>>a s d f g h j k l a s d f g h j k l a s d f g h j k l
```

## 列表推导式

语法形式:[表达式 for 变量 in 序列或迭代对象]

列表推导式在逻辑上相当于一个循环，只是形式更加简洁

```
lis = [i for i in range(10)]
print(lis)
>>>[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

使用列表推导式实现嵌套列表的平铺

```
vec = [[1,2,3],[4,5,6],[7,8,9]]
print([num for elem in vec for num in elem])
>>>[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

相当于：

```
vec = [[1,2,3],[4,5,6],[7,8,9]]
a = []
b = []
for elem in vec:
    a.append(elem)
    for num in elem:
        b.append(num)
print(a)
print(b)
>>>[[1, 2, 3], [4, 5, 6], [7, 8, 9]]
>>>[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## 列表切片操作

​格式： li[start : end : step]

step默认为1

```
a = [1,2,3,4,5]
t = a[0:3]
print(t)
t = a[2: ]
print(t)
t = a[1:3]
print(t)
t = a[0:6:2]
print(t)
>>>[1, 2, 3]
>>>[3, 4, 5]
>>>[2, 3]
>>>[1, 3, 5]

```

#### 使用切片来原地修改列表内容

```
a = [1,2,3,4,5]
print(a)
a[len(a):] =[9]      #在尾部追加元素
print(a)
a[:3] =[5,6,7]		#替换前3个元素
print(a)
a[:3] =[]			#删除前3个元素
print(a)
>>>[1, 2, 3, 4, 5]
>>>[1, 2, 3, 4, 5, 9]
>>>[5, 6, 7, 4, 5, 9]
>>>[4, 5, 9]

```

#### 使用del与切片结合来删除列表元素

```
a = [1,2,3,4,5]
print(a)
del a[:3]				#删除前3个元素
print(a)
a[len(a):] =[6,7,8]
print(a)
del a[::2]				#删除偶数位置上的元素
print(a)
>>>[1, 2, 3, 4, 5]
>>>[4, 5]
>>>[4, 5, 6, 7, 8]
>>>[5, 7]

```

#### 切片返回的是列表元素的浅复制

所谓浅复制，是指生成一个新的列表，并且把原列表中所有元素的引用都复制到新列表中。

```
a = [1,2,3,4,5]
b = a				#b与a指向同一个内存
print(b)
>>>[1, 2, 3, 4, 5]
b[1] = 8			#修改其中一个对象会影响另一个
print(a)
>>>[1, 8, 3, 4, 5]
print(a == b)		#两个列表的元素完全一样
>>>True
print(a is b)		#两个列表是同一个对象
>>>True
print(id(a))		#内存地址相同
>>>40684872
print(id(b))
>>>40684872
a = [1,2,3,4,5]
b = a[::]			#切片，浅复制
print(a == b)		#两个列表的元素完全一样
>>>True
print(a is b)		#但不是同一个对象
>>>False
print(id(a) == id(b))#内存地址不一样
>>>False
b[1] = 8			#修改其中一个不会影响另一个
print(b)
>>>[1, 8, 3, 4, 5]
print(a)
>>>[1, 2, 3, 4, 5]
```



### 随机数

在一个范围里随机取一个数

```
a = random.randint(12,20)
print(a)
>>>18
>>>15
>>>16

```

# 列表与元组

### 列表

列表是python中内置有序可变序列，列表的所有元素放在一对中括号“[]”中，并使用逗号分隔开；

一个列表中的数据类型可以各不相同

```
list1 = [1,2.3,'张三',[1,2,'sss']]
print(list1)
>>>[1, 2.3, '张三', [1, 2, 'sss']]

```

## 添加

#### append

向列表尾部追加一个元素，不改变其内存首地址，属于原地操作。

```
x = [1,2,3]
print(x)
x.append(4)
print(x)
>>>[1, 2, 3]      
>>>[1, 2, 3, 4]

```

#### insert

向列表插入一个元素，不改变其内存首地址，属于原地操作。

```
x = [1,3,4]
print(x)
x.insert(1,2)
print(x)
>>>[1, 3, 4]
>>>[1, 2, 3, 4]

```

#### extend

将另一个迭代对象的所以元素添加至该列表对象尾部，不改变其内容首地址，属于原地操作。

```
x = [1,2,3]
print(x)
x.extend([5,6,7])
print(x)
>>>[1, 2, 3]
>>>[1, 2, 3, 5, 6, 7]

```

## "+","*"

并不是真的为列表添加元素，而是创建一个新列表，不属于原地操作，而是返回新列表。

```
x = [9,6,7,5,2,4,8,3,1]
y = x + [10]
print(y)
a = x * 2
print(a)
print(x)
>>>[9, 6, 7, 5, 2, 4, 8, 3, 1, 10]
>>>[9, 6, 7, 5, 2, 4, 8, 3, 1, 9, 6, 7, 5, 2, 4, 8, 3, 1]
>>>[9, 6, 7, 5, 2, 4, 8, 3, 1]

```

## 删除

#### pop

使用列表的pop()方法删除并返回指定(默认为最后一个)位置上的元素,如果给定的索引超出列表的范围则抛出异常.

```
x = [1,2,3,4]
pos = x.pop(0)
print(x)
print(pos)
>>>[2, 3, 4]
>>>1

```

#### remove

删除首次出现的指定元素,如果列表中不存在要删除的元素,则抛出异常

```
x = [1,2,3,4]
print(x)
x.remove(3)
print(x)
>>>[1, 2, 3, 4]
>>>[1, 2, 4]

```

#### clear

清空列表

```
x = [1,2,3,4]
print(x)
x.clear()
print(x)
>>>[1, 2, 3, 4]
>>>[]

```

#### del

删除列表中的指定位置上的元素

```
x = [1,2,3,4]
print(x)
del x[1]
print(x)
>>>[1, 2, 3, 4]
>>>[1, 3, 4]

```

## 访问与计数

#### count

统计指定元素在列表中出现的次数

```
x = [1,2,3,3,4,5,6,7,3]
a = x.count(3)
print(a)
print(x.count(10))
>>>3
>>>0

```

#### index

获取指定元素首次出现的下标，若列表对象中不存在指定的元素会报错

```
x = [1,2,3,3,4,5,6,7,3]
print(x.index(3))
>>>2

```

#### in

测试列表中是否存在某元素

```
x = [1,2,3,3,4,5,6,7,3]
a = 5 in x
print(a)
>>>True

```

### 顺序排列

#### sort

按照指定规则对所有元素进行排列，默认规则是直接比较元素大小

```
x = [1,2,3,3,4,5,6,7,3]
x.sort()
print(x)
x.sort(reverse=True)
print(x)
>>>[1, 2, 3, 3, 3, 4, 5, 6, 7]
>>>[7, 6, 5, 4, 3, 3, 3, 2, 1]

```

#### reverse

返回一个逆序排列后的迭代对象,不对原列表做任何改变

```
x = [1,2,3,4]
x.reverse()
print(x)
>>>[4, 3, 2, 1]
>>>[1, 2, 3, 4]

```

#### sorted

使用内置函数sorted对列表进行排序并返回新列表,不对原列表做任何改变

```
x = [9,6,7,5,2,4,8,3,1]
print(sorted(x))
print(sorted(x,reverse = True))
print(x)
>>>[1, 2, 3, 4, 5, 6, 7, 8, 9]
>>>[9, 8, 7, 6, 5, 4, 3, 2, 1]
>>>[9, 6, 7, 5, 2, 4, 8, 3, 1]

```

#### reversed

返回一个逆序排列后的迭代对象，不对原列表做任何改变

```
alist = [1,23,55,469,748,25,55,51,21,54]
print(list(reversed(alist)))
print(alist)
>>>[54, 21, 51, 55, 25, 748, 469, 55, 23, 1]
>>>[1, 23, 55, 469, 748, 25, 55, 51, 21, 54]

```

## 常用内置函数

#### len()

返回列表中的元素个数，同样适用于元组、字典、集合、字符串等。

```
alist = [1,23,55,469,748,25,55,51,21,54]
print(len(alist))
>>>10

```

#### max()、min()

返回列表中的最大或最小元素同样适用于元组、字典、集合、字符串等。

```
alist = [1,23,55,469,748,25,55,51,21,54]
print(max(alist))
print(min(alist))
>>>748
>>>1

```

#### sum()

对列表的元素进行求和计算

```
alist = [1,23,55,469,748,25,55,51,21,54]
print(sum(alist))
>>>1502

```

#### zip()

返回可迭代的zip对象

```
a = [1,3,5,7]
b = [2,4,6,8]
c = zip(a,b)
print(c)
print(type(c))
print(list(c))
>>><zip object at 0x000000000286D2C8>
>>><class 'zip'>
>>>[(1, 2), (3, 4), (5, 6), (7, 8)]

```

#### enumerate()

枚举列表元素，返回枚举对象，其中每个元素为包含下标和值的元组。该函数对元组、字符串同样有效。

```
for un in enumerate('@##$$%ERDSf.,'):
    print(un)
>>>(0, '@')
>>>(1, '#')
>>>(2, '#')
>>>(3, '$')
>>>(4, '$')
>>>(5, '%')
>>>(6, 'E')
>>>(7, 'R')
>>>(8, 'D')
>>>(9, 'S')
>>>(10, 'f')
>>>(11, '.')
>>>(12, ',')

```

#### 三种遍历方式

```
a = ('a','s','d','f','g','h','j','k','l')
for i in a:
    print(i)
for i in range(len(a)):
    print(a[i])
for ele,i in enumerate(a):
    print(i)
>>>a s d f g h j k l a s d f g h j k l a s d f g h j k l

```

## 列表推导式

语法形式:[表达式 for 变量 in 序列或迭代对象]

列表推导式在逻辑上相当于一个循环，只是形式更加简洁

```
lis = [i for i in range(10)]
print(lis)
>>>[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

```

使用列表推导式实现嵌套列表的平铺

```
vec = [[1,2,3],[4,5,6],[7,8,9]]
print([num for elem in vec for num in elem])
>>>[1, 2, 3, 4, 5, 6, 7, 8, 9]

```

相当于：

```
vec = [[1,2,3],[4,5,6],[7,8,9]]
a = []
b = []
for elem in vec:
    a.append(elem)
    for num in elem:
        b.append(num)
print(a)
print(b)
>>>[[1, 2, 3], [4, 5, 6], [7, 8, 9]]
>>>[1, 2, 3, 4, 5, 6, 7, 8, 9]

```

## 列表切片操作

​格式： li[start : end : step]

step默认为1

```
a = [1,2,3,4,5]
t = a[0:3]
print(t)
t = a[2: ]
print(t)
t = a[1:3]
print(t)
t = a[0:6:2]
print(t)
>>>[1, 2, 3]
>>>[3, 4, 5]
>>>[2, 3]
>>>[1, 3, 5]

```

#### 使用切片来原地修改列表内容

```
a = [1,2,3,4,5]
print(a)
a[len(a):] =[9]      #在尾部追加元素
print(a)
a[:3] =[5,6,7]		#替换前3个元素
print(a)
a[:3] =[]			#删除前3个元素
print(a)
>>>[1, 2, 3, 4, 5]
>>>[1, 2, 3, 4, 5, 9]
>>>[5, 6, 7, 4, 5, 9]
>>>[4, 5, 9]

```

#### 使用del与切片结合来删除列表元素

```
a = [1,2,3,4,5]
print(a)
del a[:3]				#删除前3个元素
print(a)
a[len(a):] =[6,7,8]
print(a)
del a[::2]				#删除偶数位置上的元素
print(a)
>>>[1, 2, 3, 4, 5]
>>>[4, 5]
>>>[4, 5, 6, 7, 8]
>>>[5, 7]

```

#### 切片返回的是列表元素的浅复制

所谓浅复制，是指生成一个新的列表，并且把原列表中所有元素的引用都复制到新列表中。

```
a = [1,2,3,4,5]
b = a				#b与a指向同一个内存
print(b)
>>>[1, 2, 3, 4, 5]
b[1] = 8			#修改其中一个对象会影响另一个
print(a)
>>>[1, 8, 3, 4, 5]
print(a == b)		#两个列表的元素完全一样
>>>True
print(a is b)		#两个列表是同一个对象
>>>True
print(id(a))		#内存地址相同
>>>40684872
print(id(b))
>>>40684872
a = [1,2,3,4,5]
b = a[::]			#切片，浅复制
print(a == b)		#两个列表的元素完全一样
>>>True
print(a is b)		#但不是同一个对象
>>>False
print(id(a) == id(b))#内存地址不一样
>>>False
b[1] = 8			#修改其中一个不会影响另一个
print(b)
>>>[1, 8, 3, 4, 5]
print(a)
>>>[1, 2, 3, 4, 5]
```



# 字典

### 字典定义

字典(dictionary)是包含若干"键:值"元素的无序可变序列，字典中的每个元素包含"键"和"值"两部分,定义字典时，每个元素的键和值用冒号分隔，元素之间用逗号分隔，所有的元素放在一对大括号"{}"中。字典中的键可以为任意不可变的数据，比如整数、实数、字符串、元组等等。

### 字典的创建

创建:使用"="将一个字典赋值给一个变量

```
a_dict = {'server':'db.neuedu.com','database':'mysql'}
print(a_dict)
x={}
print(x)
>>>{'server': 'db.neuedu.com', 'database': 'mysql'}
>>>{}

```

使用dict()利用已有数据创建字典

```
keys = ['a','b','c','d']
values = [1,2,3,4]
dictionary = dict(zip(keys,values))
print(dictionary)
x = dict()
print(x)
>>>{'a': 1, 'b': 2, 'c': 3, 'd': 4}
>>>{}

```

使用dict()根据给定的键、值创建字典

```
d = dict(name = 'Dong',age = 37)
print(d)
>>>{'name': 'Dong', 'age': 37}

```

以给定内容为键，创建值为空的字典

```
adict = dict.fromkeys(['name','age','sex'])
print(adict)
>>>{'name': None, 'age': None, 'sex': None}

```

### 字典元素的读取

以键作为下标可以读取字典元素,若键不存在则抛出异常

```
adict = {'name': 'Dony', 'age': '37', 'sex': 'male'}
print(adict['name'])
>>>Dony

```

使用字典对象的get方法获取指定键对应的值,并且可以在键不存在的时候返回指定值

```
adict = {'name': 'Dony', 'age': '37', 'sex': 'male'}
print(adict.get('address'))
print(adict.get('name'))
adict['score'] = adict.get('score',[])
adict['score'].append(98)
adict['score'].append(97)
print(adict)
>>>None
>>>Dony
>>>{'name': 'Dony', 'age': '37', 'sex': 'male', 'score': [98, 97]}

```

使用字典对象的items()方法可以返回字典的键、值对列表

```
adict = {'name': 'Dony', 'age': '37', 'sex': 'male'}
for item in adict.items():
    print(item)
for key in adict:
    print(key)
>>>('name', 'Dony')
>>>('age', '37')
>>>('sex', 'male')
>>>name
>>>age
>>>sex

```

使用字典对象的keys()方法可以返回字典的键列表

```
adict = {'name': 'Dony', 'age': '37', 'sex': 'male'}
print(adict.keys())
>>>dict_keys(['name', 'age', 'sex'])

```

使用字典对象的values()方法可以返回字典的值列表

```
adict = {'name': 'Dony', 'age': '37', 'sex': 'male'}
print(adict.values())
>>>dict_values(['Dony', '37', 'male'])

```

使用字典对象的setdefault()方法返回指定"键"对应的"值"，如果字典中不存在该"键"，就添加一个新元素并设置该"键"对应的"值"。

```
adict = {'name': 'Dony', 'age': '37', 'sex': 'male'}
print(adict.setdefault('address','SDIBT'))
print(adict)
>>>SDIBT
>>>{'name': 'Dony', 'age': '37', 'sex': 'male', 'address': 'SDIBT'}

```

### 字典元素的添加

当以指定键为下标为字典赋值时,若键存在,则可以修改该键的值;若不存在,这表示添加一个键、值对

```
adict = {'name': 'Dony', 'age': '37', 'sex': 'male'}
adict['age'] = 38
print(adict)
adict['address'] = 'SDIBT'
print(adict)
>>>{'name': 'Dony', 'age': 38, 'sex': 'male'}
>>>{'name': 'Dony', 'age': 38, 'sex': 'male', 'address': 'SDIBT'}

```

使用字典对象的update方法将另一个字典的键、值对添加到当前字典对象

```
adict = {'age': 37, 'score':[98,97], 'name': 'Dony', 'sex': 'male'}
print(adict.items())
adict.update({'a':'a','b':'b'})
print(adict)
>>>dict_items([('age', 37), ('score', [98, 97]), ('name', 'Dony'), ('sex', 'male')])
>>>{'age': 37, 'score': [98, 97], 'name': 'Dony', 'sex': 'male', 'a': 'a', 'b': 'b'}

```

### 字典删除

- 使用del删除整个字典，或者字典中的指定元素
- 使用pop()和popitem()方法弹出并删除指定元素
- 使用clear()方法清空字典中所有元素

#### clear()

clear()方法是用来清除字典中的所有数据，因为是原地操作，所以返回None (也可以理解为没有返回值)

```
adict = {'age': 37, 'score':[98,97], 'name': 'Dony', 'sex': 'male'}
adict.clear()
print(adict)
>>>{}

```

#### pop()

移除字典数据pop()方法的作用是:删除指定给定键所对应的值，返回这个值并从字典中把它移除。注意字典pop()方法与列表pop()方法作用完全不同。

```
adict = {'age': 37, 'score':[98,97], 'name': 'Dony', 'sex': 'male'}
print(adict.pop('sex'))
print(adict)
>>>male
>>>{'age': 37, 'score': [98, 97], 'name': 'Dony'}

```

#### popitem()

字典popitem()方法作用是:随机返回并删除字典中的一对键和值(项)。为什么是随机删除呢?因为字典是无序的，没有所谓的''最后一项''或是其它顺序。在工作时如果遇到需要逐一删除项的工作， 用popitem()方法效率很高

```
adict = {'age': 37, 'score':[98,97],'sex': 'male', 'name': 'Dony'}
print(adict.popitem())
print(adict)
>>>('name', 'Dony')
>>>{'age': 37, 'score': [98, 97], 'sex': 'male'}

```

### 判断一个key是否在字典中

使用in方法:

```
adict = {'age': 37, 'score':[98,97],'sex': 'male', 'name': 'Dony'}
print('name' in adict.keys())
print('name' in adict)
>>>True
>>>True

```

### 遍历字典

##### 遍历key值

```
adict = {'age': 37, 'score':[98,97],'sex': 'male', 'name': 'Dony'}
for key in adict:
    print(key+':'+str(adict[key]),end=" ")
>>>age:37 score:[98, 97] sex:male name:Dony
adict = {'age': 37, 'score':[98,97],'sex': 'male', 'name': 'Dony'}
for key in adict.keys():
    print(key+':'+str(adict[key]),end=" ")
>>>age:37 score:[98, 97] sex:male name:Dony

```

在使用上,for key in a和for key in a.keys():完全等价。

##### 遍历value值

```
adict = {'age': 37, 'score':[98,97],'sex': 'male', 'name': 'Dony'}
for value in adict.values():
    print(value,end=" ")
>>>37 [98, 97] male Dony

```

##### 遍历字典项

```
adict = {'age': 37, 'score':[98,97],'sex': 'male', 'name': 'Dony'}
for kv in adict.items():
    print(kv,end=" ")
>>>('age', 37) ('score', [98, 97]) ('sex', 'male') ('name', 'Dony') 

```

##### 遍历字典键值

```
adict = {'age': 37, 'score':[98,97],'sex': 'male', 'name': 'Dony'}
for key,value in adict.items():
    print(key+':'+str(value),end=" ")
>>>age:37 score:[98, 97] sex:male name:Dony
adict = {'age': 37, 'score':[98,97],'sex': 'male', 'name': 'Dony'}
for (key,value) in adict.items():
    print(key+':'+str(value),end=" ")
>>>age:37 score:[98, 97] sex:male name:Dony 

```

在使用for key,value in a.items()与for (key,value) in a.items()完全等价

### 有序字典

Python内置字典是无序的，如果需要一个可以记住元素插入顺序的字典，可以使用collections.OrderedDict。

```
x = dict()
x['a'] = 3
x['b'] = 5
x['c'] = 8
print(x)
>>>{'a': 3, 'b': 5, 'c': 8}
import collections
x = collections.OrderedDict()
x['a'] = 3
x['b'] = 6
x['c'] = 9
print(x)
>>>OrderedDict([('a', 3), ('b', 6), ('c', 9)])

```

### 字典推导式

##### 前言

可以对比列表推导式的思路,与字典推导式的进行对比,训练自己的学习迁移能力

##### 表达式

```
{ key_expr: value_expr for value in collection if condition }

```

##### 实例

```
strings = ['import','is','with','if','file','exception','liuhu']
d = {key: val for val,key in enumerate(strings)}
s = {strings[i]:len(strings[i]) for i in range(len(strings))}
k = {k:len(k)for k in strings}
print(d)
>>>{'import': 0, 'is': 1, 'with': 2, 'if': 3, 'file': 4, 'exception': 5, 'liuhu': 6}
print(s)
>>>{'import': 6, 'is': 2, 'with': 4, 'if': 2, 'file': 4, 'exception': 9, 'liuhu': 5}
print(k)
>>>{'import': 6, 'is': 2, 'with': 4, 'if': 2, 'file': 4, 'exception': 9, 'liuhu': 5}

```

同一个字母但不同大小写的值合并起来了

```
mc = {'a':10,'b':34,'A':7,'Z':3}
mca = {k.lower():mc.get(k.lower(),0) + mc.get(k.upper(),0) for k in mc.keys()}
print(mca)
>>>{'a': 17, 'b': 34, 'z': 3}

```

### 字典排序

```
d= {'d1':2, 'd2':4,'d4':1,'d3' :3}
# 利用key排序默认升序
for k in sorted(d):
    print(k,d[k])
>>>d1 2
>>>d2 4
>>>d3 3
>>>d4 1
# 利用key排序,降序
for k in sorted(d, reverse = True):
    print(k,d[k])
>>>d4 1
>>>d3 3
>>>d2 4
>>>d1 2
# 利用value排序升序:__getitem__
for k in sorted(d,key=d.__getitem__):
    print(k,d[k])
>>>d4 1
>>>d1 2
>>>d3 3
>>>d2 4
# 利用value排序降序
for k in sorted(d,key=d.__getitem__,reverse = True):
    print(k,d[k])
>>>d2 4
>>>d3 3
>>>d1 2
>>>d4 1

```



# 集合

### 集合定义

集合是无序可变序列，使用一对大括号界定，元素不可重复，同一个集合中每个元素都是唯一的。集合中只能包含数字、字符串、元组等不可变类型的数据，而不能包含列表、字典、集合等可变类型的数据。

### 集合的创建

直接将集合赋值给变量

```
a = {3,5}
a.add(7)
print(a)
>>>{3, 5, 7}

```

使用set将其他类型数据转换为集合

```
a_set = set(range(8,14))
print(a_set)
>>>{8, 9, 10, 11, 12, 13}
b_set = set([0,1,2,3,4,5,6,8,7,2,5,2,3,1])
print(b_set)
>>>{0, 1, 2, 3, 4, 5, 6, 7, 8}
c_set = set()
print(c_set)
>>>set()

```

### 集合的删除

使用del删除整个集合

### 集合元素的增加与删除

#### 增加元素

使用add()方法为集合添加新元素，如果该元素已存在于集合中则忽略该操作。

```
s = {1,2,3}
s.add(3)
print(s)
>>>{1, 2, 3}

```

使用update()方法合并另外一个集合中的元素到当前集合中

```
s = {1,2,3}
s.update(3,4,5)
print(s)
>>>{1, 2, 3, 4, 5}

```

#### 删除元素

当不再使用某个集合时，可以使用del命令删除整个集合。集合对象的pop()方法弹出并删除其中一个元素，remove()方法直接删除指定元素，clear()方法清空集合。

```
s = {1,2,3,4,5}
print(s.pop())
>>>1
print(s.pop())
>>>2
print(s)
>>>{3, 4, 5}
s.add(2)
print(s)
>>>{2, 3, 4, 5}
s.remove(3)
print(s)
>>>{2, 4, 5}
s.clear()
print(s)
>>>set()

```

### 集合操作

Python集合支持交集、并集、差集等运算

```
a_set = set([7,8,9,10,11,12,13,14])
b_set = {0,1,2,3,4,5,6,7}
print(a_set | b_set)
>>>{0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14}
print(a_set.union(b_set))
>>>{0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14}
print(a_set & b_set)
>>>{7}
print(a_set.intersection(b_set))
>>>{7}
print(a_set.difference(b_set))
>>>{8, 9, 10, 11, 12, 13, 14}
print(a_set - b_set)
>>>{8, 9, 10, 11, 12, 13, 14}
x = {1,2,3}
y = {1,2,5}
z = {1,2,3,4}
print(x.issubset(y))
>>>False
print(x < y)
>>>False
print(x.issubset(z))
>>>True
print(x < z)
>>>True

```

使用集合快速提取序列中单一元素

```
import random
listRandom = [random.choice(range(500)) for i in range(100)]
noRepeat = []
for i in listRandom:
    if i not in noRepeat:
        noRepeat.append(i)
print(len(listRandom))
>>>100
print(len(noRepeat))
>>>94
newSet = set(listRandom)
print(len(newSet))
>>>94

```

### 集合推导式

Python也支持集合推导式

```
s = {x.strip() for x in ('   he  ','   she','   I')}
print(s)
>>>{'he', 'she', 'I'}
```



# if语句

### 单判断语句格式

```
if 判断条件：
    执行语句......（满足条件）
else:
    执行语句......（不满足条件）
```

### 多判断语句格式

```
if 判断条件1：
    执行语句......（满足条件1）
elif 判断条件2:
    执行语句......（满足条件2）
elif 判断条件3：
	执行语句......（满足条件3）
...
else:
	执行语句......（以上条件均不满足）	
```

##### 单判断案例

```
name1 = '小明'
name2 = '小红'
a = 20
b = 20
if a > b:
    print('%s大'% name1)
else:# a <= b 就是else隐藏条件
    print('%s大'% name2)
>>>小红大
```

##### 多判断案例

```
score = int(input('请输入该学生分数：'))
if score < 60:
    print('不及格')
elif score < 75:#el有隐藏条件score >= 60
    print('及格')
elif score < 90:
    print('良好')
else:
    print('优秀')
>>>请输入该学生分数：92
>>>优秀
```

##### 等值判断案例

```
x = 10
if x == 5:
    print('进入一班')
elif x == 10:
    print('进入二班')
else:
    print('进入三班')
>>>进入二班
```



# 循环语句

- while循环：在给定的判断条件为 true 时执行循环体，否则退出循环体
- for循环：重复执行语句
- 嵌套循环：你可以在while循环体中嵌套for循环

循环基本四大要素：条件、循环体(语句块)、改变循环变量(使循环不是死循环)、循环变量初始化

### while循环

while 条件:
    语句块(条件满足就执行，
        执行完就又回到while后面的条件继续判断，
        如果条件还满足就继续执行此语句块，
        如果条件不满足就结束while循环)

```
count = 1
sum = 0
while count <= 100:
    sum += count
    count += 1
print(sum)
>>>5050
```

循环变量初始化
while 条件：
    循环体
    改变循环变量的值(使循环正常退出)

### for循环

for item in items:

​	取出item里面的数据

```
for item in "www.neuedu.com":
    print(item)
>>>w
>>>w
>>>w
>>>.
>>>n
>>>e
>>>u
>>>e
>>>d
>>>u
>>>.
>>>c
>>>o
>>>m
```

### 嵌套循环

```
for num in range(10,21):                # 迭代10 到 20之间的数字
    for i in range(2,num):              # 根据因子迭代
        if num %i == 0:                 # 确定第一个因子
            j = num/i                   # 计算第二个因子
            print('%d 是一个合数'% num)
            break                       # 跳出当前循环
    	else:                               # 循环的else部分
        print('%d 是一个质数'% num)
>>>10 是一个合数
>>>11 是一个质数
>>>12 是一个合数
>>>13 是一个质数
>>>14 是一个合数
>>>15 是一个合数
>>>16 是一个合数
>>>17 是一个质数
>>>18 是一个合数
>>>19 是一个质数
>>>20 是一个合数
```

## 循环控制语句

- break：在语句块执行过程中终止循环，并且跳出整个循环（只能存在与循环体内）
- continue：在语句块执行过程中终止当前循环，跳出该次循环，执行下一次循环
- pass：pass是空语句，是为了保持程序结构的完整性

### break语句

当循环遇到break就停止循环，继续循环下面的语句块（只能存在与循环体内）

```
count = 1
sum = 0
while count <= 100:
    sum += count
    if sum > 1000: # 当sum大于1000时结束循环
        break
    count += 1
print(sum)
print(count)
>>>1035
>>>45
```

### continue

结束本层的本次循环，继续执行下一次的循环

```
count = 1
sum = 0
while count <= 100:
    if count %2 == 0:  # 偶数时跳过输出
        count += 1
        continue
    sum = sum + count1
    count += 1
print(sum)
print(count)
>>>2500
>>>101
```



# 运算符

- 算术运算符
- 比较运算符
- 逻辑运算符
- 赋值运算符

### 算术运算符

|  **加**  | **+**  |
| :------: | :----: |
|  **减**  | **-**  |
|  **乘**  | *****  |
|  **除**  | **/**  |
| **取整** | **//** |
| **取余** | **%**  |
|  **幂**  | ****** |

```
>>> a = 1
>>> b = 2
>>> a + b
3
>>> a - b
-1
>>> a * b
2
>>> a / b
0.5
>>> a // b
0
>>> a % b
1
>>> b ** a
2
```

### 比较运算符

|   **等于**   | **==** |
| :----------: | :----: |
|  **不等于**  | **!=** |
|   **大于**   | **>**  |
|   **小于**   | **<**  |
| **大于等于** | **>=** |
| **小于等于** | **<=** |

```
>>> a = 10
>>> b = 20
>>> a == b
False
>>> a != b
True
>>> a > b
False
>>> a < b
True
>>> a >= b
False
>>> a <= b
True
```

### 逻辑运算符

| **与** | **and** |
| :----: | :-----: |
| **或** | **or**  |
| **非** | **not** |

```
>>> a = True
>>> b = False
>>> a and b
False
>>> a or b
True
>>> not a
False
>>> not 0
True
>>> not -1
False
```

### 赋值运算符

|     **加法**     |   **+=**    |    `c+=a`  等同于  `c=c+a`    |
| :--------------: | :---------: | :---------------------------: |
|     **减法**     |   **-=**    |  **`c-=a`  等同于  `c=c-a`**  |
|     **乘法**     |   ***=**    |  `c*=a`  **等同于**  `c=c*a`  |
|     **除法**     |   **/=**    |  `c/=a` **等同于**  `c=c/a`   |
|    **取整数**    |   **//=**   | `c//=a`  **等同于**  `c=c//a` |
| **取模(取余数)** |   **%=**    |  `c%=a`  **等同于**  `c=c%a`  |
|      **幂**      | ********=** | `c**=a`  **等同于**  `c=c**a` |

# 运算符优先级

|                  **                  |           幂           |
| :----------------------------------: | :--------------------: |
|           ***  /  %  //**            | **乘、除、取整、取余** |
|               **+  -**               |       **加、减**       |
|           **<=  <  >  >=**           |     **大于、小于**     |
|              **==  !=**              |    **等于、不等于**    |
| ********=  *=  /=  %=  //=  -=  +=** |     **赋值运算符**     |
|           **not  and  or**           |     **逻辑运算符**     |



# 函数

### 定义一个函数

Python定义函数用def关键字,一般格式如下

```
def 函数名(参数列表):
    函数体

```

函数名的命名规则

函数名必须以下划线或字母开头，可以包含任意字母、数字或下划线的组合。不能使用任何的标点符号，函数名是区分大小写的。函数名不能是保留字。

```
def hello():
    print('Hello neuedu')
hello()
>>>Hello neuedu

```

形参和实参

形参:形式参数，不是实际存在，是虚拟变量。在定义函数和函数体的时候使用形参，目的是在函数调用时接收实参(实参个数，类型应与实参一一对应)

实参:实际参数，调用函数时传给函数的参数，可以是常量，变量，表达式，函数，传给形参

区别:形参是虚拟的，不占用内存空间，形参变量只有在被调用时才分配内存单元，实参是一个变量，占用内存空间，数据传送单向，实参传给形参，不能形参传给实参

```
def area(width,height):
    return width * height
w = 4
h = 5
print(area(w,h))
>>>20

```

width和height是形参,w=4和h=5是实参

### 使用函数的好处

1. 代码重用
2. 便于修改,易拓展

例:

```
msg = 'abcdefg'
msg = msg[:2] + 'z' + msg[3:]
print(msg)
msg = '1234567'
msg = msg[:2] + '9' + msg[3:]
print(msg)
>>>abzdefg
>>>1294567

```

改进

```
def setstr(msg,index,char):
    return msg[:index] + char + msg[index+1:]
msg = 'abcdefg'
print(setstr(msg,2,'z'))
msg = '1234567'
print(setstr(msg,2,'9'))
>>>abzdefg
>>>1294567

```

### 函数的参数

必需参数

关键字参数

默认参数

不定长参数

##### 必需参数

必需参数须以正确的顺序传入函数.调用时的数量必须和声明时的一样

```
def f(name,age):
    print('I am %s,I am %d'%(name,age))
f('alex',18)
f('alvin',16)
>>>I am alex,I am 18
>>>I am alvin,I am 16

```

##### 关键字参数

关键字参数和函数调用关系紧密，函数调用使用关键字参数来确定传入的参数值。使用关键字参数允许函数调用时参数的顺序与声明时不一致，因为 Python 解释器能够用参数名匹配参数值。

```
def f(name,age):
    print('I am %s,I am %d'%(name,age))
# f(18,'alex')      报错
f(age=16,name='alvin')
>>>I am alvin,I am 16

```

##### 默认参数

调用函数时,缺省参数的值如果没有传入,则被认为是默认值.下例会打印默认的age,如果age没有被传入:

```
def print_info(name,age,sex='male'):
    print('Name:%s'%name)
    print('age:%s'%age)
    print('Sex:%s'%sex)
    return
print_info('alex',18)
print_info('铁锤',40,'female')
>>>Name:alex
>>>age:18
>>>Sex:male
>>>Name:铁锤
>>>age:40
>>>Sex:female

```

不定长参数

你可能需要一个函数能处理比当初声明时更多的参数.这些参数叫做不定长参数,和上述2种参数不同,声明时不会命名.

```
def add(*tuples):
    sum = 0
    for v in tuples:
        sum += v
    return sum
print(add(1,4,6,9))
print(add(1,4,6,9,5))
>>>20
>>>25

```

加了星号(*)的变量名会存放所有未命名的变量参数。而加(**)的变量名会存放命名的变量参数

```
def print_info(**kwargs):
    print(kwargs)
    for i in kwargs:
        print('%s:%s'%(i,kwargs[i]))
    return
print_info(name='alex',age=18,sex='female',hobby='girl',nationality='Chinese',ability='Python')
>>>{'name': 'alex', 'age': 18, 'sex': 'female', 'hobby': 'girl', 'nationality': 'Chinese', 'ability': 'Python'}
>>>name:alex
>>>age:18
>>>sex:female
>>>hobby:girl
>>>nationality:Chinese
>>>ability:Python
def print_info(name,*args,**kwargs):
    print('Name:%s'% name)
    print('args:',args)
    print('kwargs:',kwargs)
    return
print_info('alex',18,hobby='girl',nationality='Chinese',ability='Python')
>>>Name:alex
>>>args: (18,)
>>>kwargs: {'hobby': 'girl', 'nationality': 'Chinese', 'ability': 'Python'}

```

注意,还可以这样传参:

```
def f(*args):
    print(args)
f(*[1,2,5])
def x(**kargs):
    print(kargs)
x(**{'name':'alex'})
>>>(1,2,5)
>>>{'name': 'alex'}

```

PyCharm的调试工具

F8 Step Over 可以单步执行代码,会把函数调用看作是一行代码直接执行

F7 Step Into 可以单步执行代码,如果是函数,会进入函数内部

### 函数的返回值

要想获取函数的执行结果，就可以用return语句把结果返回

注意:

函数在执行过程中只要遇到return语句,就会停止执行并返回结果,所以也可以理解为return语句代表着函数的结束

如果未在函数中指定return,那这个函数的返回值为None

return多个对象,解释器会把这多个对象组装成一个元组作为一个一个整体结果输出。

```
def sum_and_avg(list):
    sum = 0
    count = 0
    for e in list:
        if isinstance(e,int) or isinstance(e,float):
            count += 1
            sum += e
    return sum,sum/count
my_list = [20,15,2.8,'a',35,5.9,-1.8]
tp = sum_and_avg(my_list)
print(tp)
>>>(76.9, 12.816666666666668)

```

### 高阶函数

高阶函数是至少满足下列一个条件的函数:

接受一个或多个函数作为输入输出一个函数

```
def add(x,y,f):
    return f(x)+f(y)
res = add(3,-6,abs)
print(res)
>>>9
def method():
    x = 2
    def double(n):
        return n * x
    return double
fun = method()
num = fun(20)
print(num)
>>>40

```

### 函数作用域

##### 作用域介绍

python中的作用域分4种情况:

L: local,局部作用域，即函数中定义的变量;E: enclosing, 嵌套的父级函数的局部作用域，即包含此函数的_上级函数的局部作用域，但不是全局的;G: global, 全局变量，就是模块级别定义的变量;B: built-in,系统固定模块里面的变量，比如int, bytearray等。搜索变量的优先级顺序依次是:作用域局部>外层作用域>当前模块中的全局>python内置作用域，也就是LEGB。



当然，local和enclosing是相对的，enclosing变量相对上层来说也是local.

```
x = str(100) # int bulit-in
print('hello' + x)
g_count = 0 # global
def outer():
    o_count = 1 # enclosing
    def inner():
        i_count = 2 # local
        print(o_count)
    # print(i_count) 找不到
    inner()
outer()
# print(o_count) 找不到
>>>hello100
>>>1

```

##### 作用域产生

在Python中，只有模块（module），类（class）以及函数（def、lambda）才会引入新的作用域，其它的代码块（如if、try、for等）是不会引入新的作用域的

```
if 2>1:
    x = 1
print(x)
>>>1

```

这个是没有问题的，if并没有引入一个新的作用域，x仍处在当前作用域中，后面代码可以使用。

```
def test():
    x = 2
print(x) # NameError: name 'x2' is not defined

```

def、class、lambda是可以引入新作用域的。

##### 变量的修改

```
x=6
def f2():
    print(x)
    x=5
f2()

# 变量是先声明，再引用的
# 错误的原因在于 print(x)，解释器会在局部作用域找，会找到x=5(函数已经加载到内存),但x使用在声明前了,所以报错:
# local variable 'x' referenced before assignment.如何证明找到了x=5呢?简单:注释掉x=5,x=6
# 报错为:name 'x' is not defined
#同理

x=6
def f2():
    x+=1 #local variable 'x' referenced before assignment.  x 使用之前已经被声明了
#x+=1：x = x + 1；x 已经被声明了，x=6，这里等于 6 = 6 + 1，发生报错
f2()

```

要修改:

```
x=6

def f2():
    global x # 默认找 local 里的 x，加上 global关键字让他去找外面 global 的 x
    print(x)
    x=5  # 对 global 的 x 进行修改
    
f2()      # 6
print(x)  # 5global关键字

```

##### global关键字

当内部作用域想修改外部作用域的变量时，就要用到global和nonlocal关键字了，当修改的变量是在全局作用域（global作用域）上的，就要使用global先声明一下

```
total = 0 # 定义全局变量
def sum(arg1,arg2):
    total = arg1 +arg2 # 这里的total是局部变量
    print('函数内是局部变量:',total)
    return total
sum(10,20)
print('函数外是全局变量:',total)
num = 1
def fun():
    global num # 加了global后,在函数内部是可以改变外面的全局变量
    num = 123
    print('函数内是局部变量:',num)
fun()
print('函数外是全局变量:',num)
>>>函数内是局部变量: 30
>>>函数外是全局变量: 0
>>>函数内是局部变量: 123
>>>函数外是全局变量: 123

```

##### nonlocal关键字

global关键字声明的变量必须在全局作用域上，不能嵌套作用域上，当要修改嵌套作用域（enclosing作用域，外层非全局作用域）中的变量怎么办呢，这时就需要nonlocal关键字了

```
def outer():
    count = 1
    def inner():
        count = 12
    inner()
    print(count)
outer()
>>>1
def outer():
    count = 1
    def inner():
        # 使用nonlocal关键字可以在一个嵌套的函数中修改嵌套作用域中的变量
        nonlocal count
        count = 12
    inner()
    print(count)
outer()
>>>12

```

##### 小结

1. 变量查找顺序: LEGB，作用域局部>外层作用域>当前模块中的全局>python内置作用域;
2. 只有模块、类、及函数才能引入新作用域;
3. 对于一一个变量，内部作用域先声明就会覆盖外部变量，不声明直接使用，就会使用外部作用域的变量;
4. 内部作用域要修改外部作用域变量的值时，全局变量要使用global关键字，嵌套作用域变量要使用nonlocal关键字。nonlocal是 python3新增的关键字，有了这个关键字，就能完美的实现闭包了。

### 递归函数

定义:在函数内部,可以调用其他函数.如果一个函数在内部调用自身本身,这个函数就是递归函数

```
def factorial(n):
    result = n
    for i in range(1,n):
        result *= i
    return result
print(factorial(4))
>>>24

#**********递归**********
def factorial_new(n):
    if n == 1:
        return 1
    return n*factorial_new(n-1)
print(factorial_new(3))
>>>6

```

```
def fibo(n):
    before = 0
    after = 1
    for i in range(n-1):
        ret = before + after
        before = after
        after = ret
    return ret
print(fibo(3))
>>>2

#**********递归**********
def fibo_new(n):
    if n <= 1:
        return n
    return(fibo_new(n-1) + fibo_new(n-2))
print(fibo_new(3))
>>>2

```

1 print(fibo_ new(30000))# maximum recursion depth exceeded in comparison递归函数的优点:是定义简单，逻辑清晰。理论上，所有的递归函数都可以写成循环的方式，但循环的逻辑不如递归清晰。

##### 递归特性

1. 必须有一个明确的结束条件
2. 每次进入更深一层递归时，问题规模相比上次递归都应有所减少
3. 递归效率不高，递归层次过多会导致栈溢出(在计算机中，函数调用是通过栈(stack) 这种数据结构实现的，每当进入一个函数调用，栈就会加一层栈帧，每当函数返回，栈就会减- -层栈帧。由于栈不是无限的，所以，递归调用的次数过多，会导致栈溢出。)

### 匿名函数

匿名函数就是不需要显式的指定函数名。

```
calc = lambda n : n**n
print(calc(10))

```

关键字lambda表示匿名函数，冒号前面的n表示函数参数，可以有多个参数;

匿名函数有个限制，就是只能有一个表达式，不用写return，返回值就是该表达式的结果;

用匿名函数有个好处，因为函数没有名字，不必担心函数名冲突。此外，匿名函数也是-一个函数对象，也可以把匿名函数赋值给一一个变量， 再利用变量来调用该函数;

有些函数在代码中只用一次，而且函数体比较简单，使用匿名函数可以减少代码量，看起来比较”优雅“

```
def calc(x,y):
    return x**y
#换成匿名函数
calc = lambda x,y:x**y
print(calc(2,5))
>>>32
>>>32
def calc(x,y):
    if x>y:
        return x*y
    else:
        return x/y
#换成匿名函数
calc = lambda x,y:x * y if x > y else x / y
print(calc(2,5))
>>>0.4
>>>0.4

```

匿名函数主要与其他函数联合使用

### 内置函数

```
abs()	dict()	help()	min()	setattr()
all()	dir()	hex()	next( )	slice()
any()	divmod()	id()	object()	sorted()
ascii()	enumerate()	input()	oct()	staticmethod()
bin()	eval()	int()	open()	str()
bool()	exec()	isinstance()	ord()	sum()
bytearray()	filter()	issubclass()	pow()	super( )
bytes()	float()	iter()	print()	tuple()
callable()	format()	len()	property()	type()
chr()	frozenset()	list()	range()	vars()
classmethod( )	getattr()	locals()	repr()	zip()
compile()	globals()	map()	reversed()	_import_()
complex()	hasattr()	max( )	round()	
delattr()	hash()	memoryview( )	set()

```

##### map函数

map()函数接收两个参数，-一个是函数，-个是Iterable ，map 将传入的函数依次作用到序列的每个元素

并把结果作为新的Iterator返回

遍历序列，对序列中每个元素进行函数操作，最终获取新的序列。

```
# 一般解决方案
li = [1,2,3,4,5,6,7,8,9]
for ind,val in enumerate(li):
    li[ind] = val *val
print(li)
>>>[1, 4, 9, 16, 25, 36, 49, 64, 81]
# 高级解决方案
li = [1,2,3,4,5,6,7,8,9]
print(list(map(lambda x:x*x,li)))
>>>[1, 4, 9, 16, 25, 36, 49, 64, 81]

```

##### reduce函数

reduce把一一个函数作用在一个序列[x1, x2, x3, ...上，这个函数必须接收两个参数，reduce 把结果继续和

序列的下一个元素做累积计算，其效果就是:

​					reduce(func,[1,2,3])等同于func(func(1,2),3)

对于序列内所有元素进行累计操作

```
# 接受一个list并利用reduce()求积
from functools import reduce
li = [1,2,3,4,5,6,7,8,9]
print(reduce(lambda x,y:x * y,li))
>>>362880

```

##### filter函数

filter()也接收一一个函数和- -个序列。和map()不同的是，filter() 把传入的函数依次作用于每个元素，然后

根据返回值是True还是False 决定保留还是丢弃该元素。

对于序列中的元素进行筛选，最终获取符合条件的序列

```
# 在一个list中,删除偶数,只保留奇数
li = [1,2,4,5,6,9,10,15]
print(list(filter(lambda x:x % 2==1,li)))
>>>[1, 5, 9, 15]
# 回数是指从左向右读和从右向左读都是一样的数,例如12321,909.请利用filter()筛选出回数
li = list(range(1,200))
print(list(filter(lambda x:int(str(x))==int(str(x)[::-1]),li)))
>>>[1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 22, 33, 44, 55, 66, 77, 88, 99, 101, 111, 121, 131, 141, 151, 161, 171, 181, 191]

```

##### sorted函数

```
sorted(iterable, /, *，key=None, reverse=False)

```

接收一个key函数来实现对可迭代对象进行自定义的排序

可迭代对象:主要与列表，字符串，元祖，集合和字典

key:接受-一个函数，根据此函数返回的结果，进行排序

 reverse:排序方向，默认为从小到大，reverse=True为逆向

```
li = [-21,-12,5,9,36]
print(sorted(li,key = lambda x:abs(x)))
>>>[5, 9, -12, -21, 36]
"""""""""""""""""""""""
sorted( )函数按照keys进行排序，并按照对应关系返回1 ist相应的元素:
keys排序结果 => [5，9， 12， 21，36]
			   |  |   |    |   |
最终结果	 => [5，9，-12，-21，36]
"""""""""""""""""""""""

```

```
# 把下面单词以首字母排序
li = ['bad','about','Zoo','Credit']
print(sorted(li,key = lambda x : x[0]))、
>>>['Credit', 'Zoo', 'about', 'bad']
"""""""""""""""""""""""
对字符串排序,是按照ASCII的大小比较的,由于'Z' < 'a',结果,大写字母Z会排在小写字母a的前面。
"""""""""""""""""""""""
# 假设我们用一组tuple表示学生名字和成绩
L = [('Bob',75),('Adam',92),('Bart',66),('Lisa',88)]
# 请用sorted()对上述列表分别按名字排序
print(sorted(L,key = lambda x : x[0]))
>>>[('Adam', 92), ('Bart', 66), ('Bob', 75), ('Lisa', 88)]
# 再按照成绩从高到低排序
print(sorted(L,key = lambda x : x[1], reverse = True))
>>>[('Adam', 92), ('Lisa', 88), ('Bob', 75), ('Bart', 66)]


```

### 函数式编程

学会了上面几个重要的函数后，我们就可以来聊一聊函数式编程了。

##### 概念(函数式编程)

函数式编程是一种编程范式， 我们常见的编程范式有命令式编程(Imperativeprogramming)，函数式编程，常见的面向对象编程是也是一种命令式编程。

命令式编程是面向计算机硬件的抽象，有变量(对应着存储单元)，赋值语句(获取，存储指令)，表达式(内存引用和算术运算)和控制语句(跳转指令)，一句话，命令式程序就是-个冯诺依曼机的指令序列。

而函数式编程是面向数学的抽象，将计算描述为一种表达式求值，一句话，函数式程序就是一个表达式。

##### 函数式编程的本质

函数式编程中的函数这个术语不是指计算机中的函数，而是指数学中的函数，即自变量的映射。也就是说一个函数的值仅决定于函数参数的值，不依赖其他状态。比如y=x* x函数计算x的平方根，只要x的平方，不论什么时候调用，调用几次，值都是不变的。

纯函数式编程语言中的变量也不是命令式编程语言中的变量，即存储状态的单元，而是代数中的变量，即一个值的名称。变量的值是不可变的(immutable) ，也就是说不允许像命令式编程语言中那样多次给- -个变量赋值。比如说在命令式编程语言我们写“x=x+1”，这依赖可变状态的事实，拿给程序员看说是对的，但拿给数学家看，却被认为这个等式为假。

函数式语言的如条件语句，循环语句也不是命令式编程语言中的控制语句，而是函数的语法糖。

严格意义 上的函数式编程意味着不使用可变的变量，赋值，循环和其他命令式控制结构进行编程。

函数式编程关心数据的映射，命令式编程关心解决问题的步骤，这也是为什么“函数式编程叫做函数式编程”。

##### 函数式编程的好处

1. 代码简洁，易懂。

2. 无副作用

   ​	由于命令式编程语言也可以通过类似函数指针的方式来实现高阶函数，函数式的最主要的好处主要是不可变性带来的。没有可变的状态，函数就是引|用透明( Referential transparency) 的和没有副作用(No SideEffect) 。

### 将函数存储在模块中

函数的优点之一是，使用它们可将代码块与主程序分离。通过给函数指定描述性名称，可让主程序容易理解得多。你还可以更进一步，将函数存储在被称为**模块**的独立文件中，再将模块**导入**到主程序中。import 语句允许在当前运行的程序文件中使用模块中的代码。

通过将函数存储在独立的文件中，可隐藏程序代码的细节，将重点放在程序的高层逻辑上。这还能让你在众多不同的程序中重用函数。将函数存储在独立文件中后，可与其他程序员共享这些文件而不是整个程序。知道如何导入函数还能让你使用其他程序员编写的函数库。

导入模块的方法有多种，下面对每种都作简要的介绍。

##### 导入整个模块

要让函数是可导入的，得先创建模块。模块是扩展名为.py的文件，包含要导入到程序中的代码。下面来创建一个包含函数make_ pizza() 的模块。

**pizza.py**

```
def make_pizza(size,*toppings):
    """描述要制作的披萨"""
    print("\nMaking a"+ str(size)+"-inch pizza with the following toppings:")
    for topping in toppings:
        print("-"+topping)


```

接下来，我们在pizza.py所在的目录中创建另一个名为making_pizzas.py的文件， 这个文件导入刚创建的模块，再调用make_pizza()两次；

**making_pizza.py**

```
import pizza
pizza.make_pizza(16,'pepperoni')
pizza.make_pizza(12,'mushrooms','green peppers','extra cheese')


```

Python读取这个文件时，代码行import pizza 让Python打开文件pizza.py,并将其中的所有函数都复制到这个程序中。你看不到复制的代码，因为这个程序运行时，Python在幕后 复制这些代码。你只需知道，在making_ pizzas.py中 ，可以使用pizza.py中定义的所有函数。

```
Making a16-inch pizza with the following toppings:
-pepperoni

Making a12-inch pizza with the following toppings:
-mushrooms
-green peppers
-extra cheese


```

这就是一种导入方法:只需编写一 条import 语句并在其中指定模块名，就可在程序中使用该模块中的所有函数。如果你使用这种import 语句导入了名为module _name . py的整个模块，就可使用下面的语法来使用其中任何一个函数:

```
_module_name.function_name_()


```

##### 导入特定的函数

你还可以导入模块中的特定函数，这种导入方法的语法如下:

```
from _module_name_ import _function_name_


```

通过用逗号分隔函数名，可根据需要从模块中导入任意数量的函数: 

```
from _module_name_ import _function_0,function_1,function_2_


```

对于前面的making_pizzas.py示例， 如果只想导入要使用的函数，代码将类似于下面这样:

```
from pizza import make_pizza
pizza.make_pizza(16,'pepperoni')
pizza.make_pizza(12,'mushrooms','green peppers','extra cheese')


```

若使用这种语法，调用函数时就无需使用句点。由于我们在import语句中显式地导入了函数make_pizza() ，因此调用它时只需指定其名称。

##### 使用as给函数指定别名

如果要导入的函数的名称可能与程序中现有的名称冲突，或者函数的名称太长，可指定简短而独一无二 的**别名**--函数的另一个名称，类似于外号。要给函数指定这种特殊外号，需要在导入它时这样做。

下面给函数make pizza() 指定了别名mp()。这是在import 语句中使用make. pizza as mp实现的关键字as将函数重命名为你提供的别名:

```
from pizza import make_pizza as mp
mp(16,'pepperoni')
mp(12,'mushrooms','green peppers','extra cheese')
>>>Making a16-inch pizza with the following toppings:
>>>-pepperoni

>>>Making a12-inch pizza with the following toppings:
>>>-mushrooms
>>>-green peppers
>>>-extra cheese


```

上面的import 语句将函数make_pizza()重命名为mp() ;在这个程序中，每当需要调用make_ pizza() 时，都可简写成mp() ，而Python将运行make_ pizza() 中的代码，这可避免与这个程序可能包含的函数make_ pizza() 混淆。

指定别名的通用语法如下:

```
from _module_name_ import _function_name_ as _fn_


```

##### 使用as给模块指定别名

你还可以给模块指定别名。通过给模块指定简短的别名(如给模块pizza 指定别名p )，让你能够更轻松地调用模块中的函数。相比于pizza.make_ pizza()，p.make_ pizza() 更为简洁:

```
import pizza as p
p.make_pizza(16,'pepperoni')
p.make_pizza(12,'mushrooms','green peppers','extra cheese')
>>>Making a16-inch pizza with the following toppings:
>>>-pepperoni

>>>Making a12-inch pizza with the following toppings:
>>>-mushrooms
>>>-green peppers
>>>-extra cheese


```

上述import语句给模块pizza指定了别名p，但该模块中所有函数的名称都没变。调用函数make_pizza()时，可编写代码p.make_pizza()而不是pizza.make_pizza()，这样不仅能使代码更简洁，还可以让你不再关注模块名，而专注于描述性的函数名。这些函数名明确地指出了函数的功能，对理解代码而言，它们比模块名更重要。

给模块指定别名的通用语法如下: 

```
import _module_name as mn_


```

##### 导入模块中的所有函数

使用星号( * )运算符可让Python导入模块中的所有函数:

```
from pizza import *
make_pizza(16,'pepperoni')
make_pizza(12,'mushrooms','green peppers','extra cheese')
>>>Making a16-inch pizza with the following toppings:
>>>-pepperoni

>>>Making a12-inch pizza with the following toppings:
>>>-mushrooms
>>>-green peppers
>>>-extra cheese


```

import语句中的星号让Python将模块pizza 中的每个函数都复制到这个程序文件中。由于导入了每个函数，可通过名称来调用每个函数，而无需使用句点表示法。然而，使用并非自己编写的大型模块时，最好不要采用这种导入方法.

最佳的做法是，要么只导入你需要使用的函数，要么导入整个模块并使用句点表示法。这能让代码更清晰，更容易阅读和理解。这里之所以介绍这种导入方法，只是想让你在阅读别人编写的代码时，如果遇到类似于下面的import 语句，能够理解它们:

```
from _module_name_ import *


```

### 函数文档字符串

函数文档字符串documentation string (docstring) 是在函数开头，用来解释其接口的字符串。简而言之:帮助文档

- 包含函数的基础信息
- 包含函数的功能简介
- 包含每个形参的类型，使用等信息
- 必须在函数的首行,经过验证前面有注释性说明是可以的，不过最好函数文档出现在首行
- 使用三引号注解的多行字符串(当然，也可以是一行)，因三引号可以实现多行注解（展示） ("' '") 或 ("" "")
- 函数文档的第一行一 般概述函数的主要功能，第二行空，第三行详细描述。

**查看方式**

- 在交互模式下可以使用he l p查看函数，帮助文档，该界面会跳到帮助界面，需要输入q退出界面
- 使用-doc-属性查看，该方法的帮助文档文字直接显示在交互界面上。代码如下:

```
def test(msg):
    print("函数输出成功"+msg)
test('hello')
print(help(test))
print(test.__doc__)
函数输出成功hello
>>>Help on function test in module __main__:

>>>test(msg)

>>>None
>>>None


```



# 面向对象

Python从设计之初就已经是一门面向对象的语言，正因为如此，在Python中创建一个类和对象是很容易的。本章节我们将详细介绍Python的面向对象编程。

如果你以前没有接触过面向对象的编程语言，那你可能需要先了解一些面向对象语言的一些基本特征，在头脑里头形成一个基本的面向对象的概念，这样有助于你更容易的学习Python的面向对象编程。

## 类和对象

#### 万物皆对象

分类是人们认识世界的-一个很自然的过程，在日常生活中会不自觉地将对象进行进行分类

**对象归类**

- 类是抽象的概念，仅仅是模板比如说:“人”
- 对象是一个你能够看得到、摸得着的具体实体:赵本山，刘德华，赵丽颖

```
user1 = 'zhangsan'
print(type(user1))
user2 = 'lisi'
print(type(user2))
>>><class 'str'>
>>><class 'str'>

```

以上str是类( python中的字符串类型)，user1和user2是对象(以前我们叫变量)

**研究对象**

顾客类型

```
属性:
姓名张浩
年龄-20
体重-60kg
行为: 
购买商品

```

收银员类型

```
属性:
员工号-10001
姓名-王淑华
部门财务部
行为:
收款
打印账单

```

#### 对象的特征一一属性

属性一一对象具有的各种特征。每个对象的每个属性都拥有特定值。例如:顾客张浩和李明的年龄、姓名不一样。

#### 对象的特征——方法(操作,行为)

方法——对象执行的操作(通常会改变属性的值)。顾客对象的方法---购买商品。收银员对象的方法----收款.

对象:用来描述客观事物的一个实体，由一组属性和方法构成

例子

```
类型:狗
对象名: doudou
属性:
颜色:白色
方法:
叫，跑，吃

```

对象同时具有属性和方法两项特性。对象的属性和方法通常被封装在一起，共同体现事物的特性，二者相辅相承，不能分割。

#### 从对象抽象出“类”

类是模子， 定义对象将会拥有的特征(属性)和行为(方法)。

**再次强调**

- 类是抽象的概念，仅仅是模板。比如说:“人”，类定义了人这种类型属性(name, age..) 和方法(study,work...).
- 对象是一个你能够看得到、摸得着的具体实体:赵本山，刘德华，赵丽颖，这些具体的人都具有人类型中定义的属性和方法，不同的是他们各自的属性不同。

根据类来创建对象被称为实例化。

## 类的定义

#### 定义只包含方法的类

在Python中要定义一个只包含方法的类，语法格式如下:

```
class 类名:
    def 方法1(self,参数列表):
        pass
    def 方法2(self,参数列表):
        pass

```

方法的定义格式和之前学习过的函数几乎-样。 区别在于第一 一个参数必须是self,大家暂时先记住，稍后介绍self。

#### 创建对象

当一个类定义完成之后，要使用这个类来创建对象，语法格式如下:

```
对象变量 = 类名()

```

第一个面向对象程序

需求:小猫爱吃鱼，小猫要喝水。

分析:

1. 定义一个猫类cat 。
2. 定义两个方法eat和drink 。

```
class Cat:
    """这是一个类:猫"""
    def eat(self):
        print('小猫爱吃鱼')
    def drink(self):
        print('小猫在喝水')
Tom = Cat()
Tom.drink()
Tom.eat()
>>>小猫在喝水
>>>小猫爱吃鱼

```

使用Cat类再创造一个对象

```
lazy_Cat = Cat()
lazy_Cat.eat()
lazy_Cat.drink()
>>>小猫爱吃鱼
>>>小猫在喝水

```

## self参数

和我们以往的经验不同，我们在调用对象的方法是不需要传递self参数，这个self参数是系统自动传递到方法里的。我们需要知道这个self到底是什么?

#### 给对象增加属性

在Python中，要给对象设置属性，非常的容易，但是不推荐使用。因为:对象属性的封装应该封装在类的内部。要给对象设置属性，只需要在类的外部的代码中直接通过.设置一个属性即可

```
tom.name = "Tom"

```

```
lazy_Cat.name = "大懒猫"

```

#### 理解self到底是什么

```
class Cat:
    """这是一个类:猫"""
    def eat(self):
        print(f'小猫爱吃鱼,我是{self.name},self的地址是{id(self)}')
    def drink(self):
        print('小猫在喝水')
Tom = Cat()
print(f'Tom的对象的id是{id(Tom)}')
Tom.name = 'Tom'
Tom.eat()
print('-'*60)
lazy_Cat = Cat()
print(f'lazy_Cat对象的id是{id(lazy_Cat)}')
lazy_Cat.name = '大懒猫'
lazy_Cat.eat()

```

```
>>>Tom的对象的id是41998544
>>>小猫爱吃鱼,我是Tom,self的地址是41998544
>>>------------------------------------------------------------
>>>lazy_Cat对象的id是41999888
>>>小猫爱吃鱼,我是大懒猫,self的地址是41999888

```

由输出可见,当我们使用

```
x对象.x方法()

```

的时候,Python会自动将x对象做为实参传给x方法的self参数.也可以这样记忆,谁点(.)的方法,self就是谁

类中的每个实例方法的第一个参数都是self

## 初始化方法init()

**之前代码存在的问题——在类的外部给对象增加属性**

- 将案例代码进行调整，先调用方法再设置属性，观察一下执行效果

```
class Cat:
    """这是一个类:猫"""
    def eat(self):
        print(f'小猫爱吃鱼,我是{self.name},self的地址是{id(self)}')
    def drink(self):
        print('小猫在喝水')
tom = Cat()
tom.drink()
tom.eat()
tom.name = 'tom'
print(tom)

```

- 程序执行报错如下:

```
AttributeError: 'Cat' object has no attribute 'name'
属性错误:'Cat'对象没有'name'属性

```

**提示**

- 在日常开发中，不推荐在**类的外部**给对象增加属性。
- 如果**在运行时，没有找到属性，程序会报错**。
- 对象应该包含有哪些属性，应该**封装在类的内部**。

**初始化方法**

- 当使用类名()创建对象时，会**自助**执行以下操作:

1. 为对象在内存中**分配空间**——创建对象(调用_ new _，以后说)
2. 为对象的属性**设置初始值**——初始化方法(调用_ init _ 并且将第一 步创建的对象，通过self参数传给     _ init _)

- 这个**初始化方法**就是 init_ 方法，一 init_ 是对象的**内置方法**(有的书也叫**魔法方法**，**特殊方法**)

_ init _ 方法是**专门**用来定义一个类**具有哪些属性并且给出这些属性的初始值的方法**!

在Cat中增加_ init _方法， 验证该方法在创建对象时会被自动调用

```
class Cat:
	"""这是一个类:猫"""
    def __init__(self):
        print('初始化方法')

```

**在初始化方法内部定义属性**

在_ init__ 方法内部使用self.属性名=属性的初始值就可以**定义属性**

定义属性之后，再使用Cat类创建的对象，都会拥有该属性

```
class Cat:
    """这是一个类:猫"""
    def __init__(self):
        print('初始化方法')
        self.name = 'tom'
    def eat(self):
        print("%s爱吃鱼"% self.name)
#使用类名()创建对象的时候,会自动调用初始化方法__init__
tom = Cat()
tom.eat()

```

**改造初始化方法——初始化的同时设置初始值**

- 在开发中，如果希望在**创建对象的同时，就设置对象的属性**，可以对_ init _ 方法进行**改造**

1. 把希望设置的属性值，定义成init_ 方法的参 数
2. 在方法内部使用self.属性 =形参接收外部传递的参数
3. 在创建对象时，使用类名(属性1， 属性2...) 调用

```
class Cat:
    """这是一个类:猫"""
    def __init__(self,name,age,color):
        print('初始化方法')
        self.name = name
        self.age = age
        self.color = color
    def eat(self):
        print("%s爱吃鱼,它%d岁了,它是一只%s的猫"% (self.name,self.age,self.color))
#使用类名()创建对象的时候,会自动调用初始化方法__init__
tom = Cat('tom',1,'blue')
tom.eat()

```

## __ str __方法

在Python中,使用print输出**对象变量**,默认情况下,会输出这个变量的类型,以及在**内存中的地址(十六进制表示)**

```
class Cat:
    """这是一个类:猫"""
    def __init__(self,new_name):
		self.name = new_name
		print("%s来了"% self.name)
tom = Cat('tom')
print(tom)
>>>tom来了
>>><__main__.Cat object at 0x00000000021CD748>

```

如果在开发中,希望使用print输出对象变量时,能够打印自定义的内容,就可以利用__ str __这个内置方法了

注意:__ str __方法必须返回一个字符串

```
class Cat:
    """这是一个类:猫"""
    def __init__(self,new_name):
		self.name = new_name
		print("%s来了"% self.name)
	def __str__(self):
		return "我是小猫: %s"% self.name
tom = Cat('tom')
print(tom)
>>>tom来了
>>>我是小猫: tom

```

## 面向对象vs面向过程

```
def CarInfo(type,price):
    print("the car's type %s,price:%d"%(type,price))
print('函数方式(面向过程)')
CarInfo('passat',250000)
CarInfo('ford',280000)

class Car:
    def __init__(self,type,price):
        self.type = type
        self.price = price

    def printCarInfo(self):
        print("the car's Info in class:type %s,price:%d"%(self.type,self.price))

print('面向对象')
carOne = Car('passat',250000)
carTwo = Car('ford',250000)
carOne.printCarInfo()
carTwo.printCarInfo()

```

输出

```
函数方式(面向过程)
the car's type passat,price:250000
the car's type ford,price:280000
面向对象
the car's Info in class:type passat,price:250000
the car's Info in class:type ford,price:250000

```

类能实现的功能,用函数也可以实现,那么类的存在还有什么特殊的意义呢?**新需求---加一个行驶里程功能**

面向过程实现

```
def CarInfo(type,price):
    print("the car's type %s,price:%d"%(type,price))

def driveDistance(oldDistance,distance):
    newDistance = oldDistance + distance
    return newDistance

print('函数方式(面向过程)')
CarInfo('passat',250000)
distance = 0
distance = driveDistance(distance,100)
distance = driveDistance(distance,200)
print(f'passat已经行驶了{distance}公里')

```

输出

```
面向过程
the car's type passat,price:250000
passat已经行驶了300公里

```

面向对象实现

```
class Car:
    def __init__(self,type,price):
        self.type = type
        self.price = price
        self.distance = 0

    def printCarInfo(self):
        print("the car's Info in class:type %s,price:%d"%(self.type,self.price))

    def driveDistance(self,distance):
        self.distance += distance

print(f'面向对象')
carOne = Car('passat',250000)
carOne.printCarInfo()
carOne.driveDistance(100)
carOne.driveDistance(200)
print(f'passat已经行驶了{carOne.distance}公里')
print(f'passat的价格是{carOne.price}')

```

输出

```
面向对象
the car's Info in class:type passat,price:250000
passat已经行驶了300公里
passat的价格是250000

```

通过对比我们可以发现:

面向对象的实现方式封装性更好，已经行驶的公里数是对象内部的属性，对象自身负责管理，外部调用
代码无需管理。我们随时可以调用对象的方法和属性得知对象当前的各种信息。而面向过程的方式而
言，外部调用代码会“手忙脚乱”
**再加一个需求:**车每行驶1公里， 车的价值贬值10元面向对象的实现方式，只需添加一 行代码:

```
def driveDistance(self,distance):
    self.distance += distance
    self.price -= distance*10

```

全部代码

```
class Car:
    def __init__(self,type,price):
        self.type = type
        self.price = price
        self.distance = 0

    def printCarInfo(self):
        print("the car's Info in class:type %s,price:%d"%(self.type,self.price))

    def driveDistance(self,distance):
        self.distance += distance
        self.price -= distance * 10

print(f'面向对象')
carOne = Car('passat',250000)
carOne.printCarInfo()
carOne.driveDistance(100)
carOne.driveDistance(200)
print(f'passat已经行驶了{carOne.distance}公里')
print(f'passat的价格是{carOne.price}')

```

输出

```
面向对象
the car's Info in class:type passat,price:250000
passat已经行驶了300公里
passat的价格是247000

```

面向过程实现

```
def CarInfo(type,price):
    print("the car's type %s,price:%d"%(type,price))
    return price

def driveDistance(oldDistance,distance):
    newDistance = oldDistance + distance
    return newDistance

def oldprice(price,distance):
    price -= distance*10
    return price

print('函数方式(面向过程)')
price = CarInfo('passat',250000)
distance = 0
distance = driveDistance(distance,100)
distance = driveDistance(distance,200)
price = oldprice(price,distance)
print(f'passat已经行驶了{distance}公里')
print(f'passat的价格是{price}')

```

输出

```
面向过程
the car's type passat,price:250000
passat已经行驶了300公里
passat的价格是247000


```

**小结可以拿公司运营作为比喻来说明面向对象开发方式的优点**
	外部调用代码好比老板面向过程中函数好比员工，让员工完成一个任务，需要老板不断的干涉,大大影
响了老板的工作效率。面向对象中对象好比员工，让员工完成-一个任务，老板只要下命令即可，员工可
以独挡一面，大大节省了老板的时间。
**还有一一种说法**
世界上本没有类， 代码写多了，也就有了类
面向对象开发方式是晚于面向过程方式出现的，几十年前，面向对象还没有出现以前，很多软件系统的代码量就已经达到几十上百万行，科学家为了组织这些代码，将各种关系密切的数据，和相关的方法分门别类，放到一起管理，就形成了面向对象的开发思想和编程语言语法。

## 私有属性---封装

在实际开发中，对象的某些属性或方法可能只希望在对象的内部被使用，而不希望在外部被访问到

**定义方式**

在定义属性或方法时，在属性名或者方法名前增加两个下划线__实际开发中私有属性也不是一层不变
的。所以要给私有属性提供外部能够操作的方法。

**通过自定义get,set方法提供私有属性的访问**

```
class Person:
    def __init__(self,name,age):
        self.name = name
        self.__age = age
    #定义对私有属性的get方法,获取私有属性
    def getAge(self):
        return self.__age
    #定义对私有属性的重新赋值的set方法,重置私有属性
    def setAge(self,age):
        self.__age = age

person1 = Person('tom',19)
person1.setAge(20)
print(person1.name,person1.getAge())
>>>tom 20


```

**使用property标注提供私有属性的访问**

```
class Teacher:
    def __init__(self,name,age,speak):
        self.name = name
        self.__age = age
        self.__speak = speak

    @property #注意1. @proterty下面默认跟的是get方法,如果设置成set会报错。
    def age(self):
        return self.__age

    @age.setter #注意2.这里是使用的上面函数名. setter,不是property. setter.
    def age(self,age):
        if age > 150 and age <= 0: #还可以在setter方法里增加判断条件
            print('年龄输入有误!')
        else:
            self.__age = age

    @property
    def for_speak(self): #注意3.这个同名函数名可以自定义名称，一般都是默认使用属性名。
        return self.__speak

    @for_speak.setter
    def for_speak(self,speak):
        self.__speak = speak

t1 = Teacher("herry",45,"Chinese")
t1.age = 38 #注意4.有了property后，直接使用t1. age ,而不是t1. age()方法了。
t1.for_speak = 'English'
print(t1.name,t1.age,t1.for_speak) #herry 38 English
>>>herry 38 English


```

## 将实例用作属性---对象组合

使用代码模拟实物时，你可能会发现自己给类添加的细节越来越多:属性和方法清单以及文件都越来越长。
在这种情况下，可能需要将类的一部分属性和方法作为一个独立的类提取出来。你可以将大型类拆分成多
协同工作的小类。

#### 实例1摆放家具

**需求**

1. 房子(House)有户型、总面积和家具名称列表

   ​	新房子没有任何家具

2. 家具(HouseItem)有名字和占地面积，其中

   ​	席梦思(bed)占地4平米

   ​	衣柜(chest)占地2平米

   ​	餐桌(table)占地1.5平米

3. 将以上三件家具添加到房子中

4. 打印房子时，要求输出:户型、总面积、剩余面积、家具名称列表

**剩余面积**

1. 在创建房子对象时，定义一个剩余面积的属性，初始值和总面积相等
2. 当调用add_ item方法，向房间添加家具时，让剩余面积-=家具面积

## 类属性类方法静态方法

#### 类对象，实例对象

类对象:类名实例对象:类创建的对象

类属性就是类对像所拥有的属性，它被所有类对象的实例对象所共有，在内存中只存在一一个副本，这个和
C++、Java中类的静态成员变量有点类似。对于公有的类属性，在类外可以通过类对象和实例对象访问

```
# 类属性
class people:
    name = "Tom"    #公有的类属性
    __age = 18      #私有的类属性

p = people
print(p.name)       #实例对象
print(people.name)  #类对象

# print(p.__age)      #错误不能在类外通过实例对象访问私有的类属性
# print(people.__age) #错误不能在类外同过类对象访问私有的类属性


```

实例属性

```
class People:
    name = "Tom"


p = People()
p.age = 18

print(p.name)
print(p.age)         # 实例属性是实例对象特有的.类对象不能拥有

print(People.name)   
# print(People.age)  # 错误:实例属性,不能通过类对象调用


```

我们经常将实例属性放在构造方法中

```
class People:
    name = "Tom"
    
    def __init__(self, age):
        self.age = age


p = People(18)

print(p.name)
print(p.age)         # 实例属性是实例对象特有的.类对象不能拥有

print(People.name)
# print(People.age)  # 错误:实例属性,不能通过类对象调用


```

类属性和实例属性混合

```
class People:
    name = "Tom"     # 类属性:实例对象和类对象可以同时调用

    def __init__(self, age):  # 实例属性
        self.age = age


p = People(18)  # 实例对象
p.sex = '男'    # 实例属性

print(p.name)
print(p.age)         # 实例属性是实例对象特有的.类对象不能拥有
print(p.sex)

print(People.name)   # 类对象
# print(People.age)  # 错误:实例属性,不能通过类对象调用
# print(People.sex)  # 错误:实例属性,不能通过类对象调用


```

如果在类外修改类属性，必须通过类对象去引用然后进行修改。如果通过实例对象去引用，会产生一个同名
的实例属性，这种方式修改的是实例属性，不会影响到类属性，并且如果通过实例对象引用该名称的属性,
实例属性会强制屏蔽掉类属性，即引用的是实例属性，除非删除了该实例属性

```
class Animal:
    name = "Panda"   # 类属性:实例对象和类对象可以同时调用


print(Animal.name)   # 类对象引用类属性
p = Animal()
print(p.name)        # 实例对象引用类属性时,会产生一个同名的实例属性
p.name = 'dog'       # 修改的只是实例属性的,不会影响到类属性
print(p.name)        # dog
print(Animal.name)   # panda

# 删除实例属性
del p.name
print(p.name)


```

#### 类属性的应用场景

比如，我们有一-个班级类，创建班级对象的时候，需要按序号指定班级名称，我们就需要知道当前已经创建
了多少个班级对象，这个数量可以设计成类属性

```
class NeuEduClass:
    class_num = 0

    def __init__(self):
        self.class_name = f'东软睿道Python{NeuEduClass.class_num+1}班'
        NeuEduClass.class_num += 1


classList = [NeuEduClass() for i in range(10)]
for c in classList:
    print(c.class_name)


```

输出

```
东软睿道Python1班
东软睿道Python2班
东软睿道Python3班
东软睿道Python4班
东软睿道Python5班
东软睿道Python6班
东软睿道Python7班
东软睿道Python8班
东软睿道Python9班
东软睿道Python10班


```

#### 类方法

类对象所拥有的方法，需要用修饰器@classmethod 来标识其为类方法，对于类方法，第一个参数必须是类对象，一般以cls作为第一个参数(当然可以用其他名称的变量作为其第一个参数， 但是大部分人都习惯以"cls’作为第一个参数的名字) ，能够通过实例对象和类对象去访问。

```
class People:
    country = "China"

    @classmethod
    def getcountry(cls):
        return cls.country


p = People()
print(p.getcountry())       # 实例对象调用类方法
print(People.getcountry())  # 类对象调用类方法


```

类方法还有一个用途就是可以对类属性进行修改:

```
class People:
    country = "China"

    @classmethod
    def getcountry(cls):
        return cls.country

    @classmethod
    def setcountry(cls, country):
        cls.country = country


p = People()
print(p.getcountry())       # 实例对象调用类方法
print(People.getcountry())  # 类对象调用类方法

p.setcountry('Japan')

print(p.getcountry())
print(People.getcountry())


```

#### 静态方法

需要通过修饰器@staticmethod 来进行修饰，静态方法不需要定义参数

```
class People3:
    country = "China"

    @staticmethod
    def getcountry():
        return People3.country
        

p = People3()
print(p.getcountry())        # 实例对象调用类方法
print(People3.getcountry())  # 类对象调用类方法


```

## 继承

继承的概念:子类自动拥有(继承)父类的所有方法和属性1)继承的语法

```
class类名(父类名):
pass


```

- 子类继承自父类，可以直接享受父类中已经封装好的方法，不需要再次开发
- 子类中应该根据职责，封装子类特有的属性和方法
- 当父类的方法实现不能满足子类需求时，可以对方法进行重写(override)

举一个常见的例子。Circle 和Rectangle，不同的图形，面积(area)计算方式不同。

```
import math
class Circle:
    def __init__(self,color,r):
        self.r = r
        self.color = color

    def area(self):
        return math.pi*self.r*self.r

    def show_color(self):
        print(self.color)

class Rectangle:
    def __init__(self,color,a,b):
        self.color = color
        self.a,self.b = a,b

    def area(self):
        return self.a * self.b

    def show_color(self):
        print(self.color)

circle = Circle('red',3.0)
print(circle.area())
circle.show_color()
rectangle = Rectangle('blue',2.0,3.0)
print(rectangle.area())
rectangle.show_color()
>>>28.274333882308138
>>>red
>>>6.0
>>>blue


```

我们看到Rectangle和Circle有同样的属性color和方法showcolor我们可以定义一个父类Shape, 将Rectangle
和Circle通用的部分提取到Shape类中，然后在子类的init方法中，通过调用super0_ init_ (color). 把color
传给父类的__ init \ ()

```
import math
class Shape:
    def __init__(self,color):
        self.color =color

    def area(self):
        return None

    def show_color(self):
        print(self.color)

class Circle(Shape):
    def __init__(self,color,r):
        super().__init__(color)
        self.r = r

    def area(self):
        return math.pi * self.r * self.r

class Rectangle(Shape):
    def __init__(self,color,a,b):
        super().__init__(color)
        self.a,self.b = a,b

    def area(self):
        return self.a * self.b

circle = Circle('red',3.0)
print(circle.area())
circle.show_color()
rectangle = Rectangle('blue',2.0,3.0)
print(rectangle.area())
rectangle.show_color()
>>>28.274333882308138
>>>red
>>>6.0
>>>blue      
      


```

子类Circle和Rectangle本身并没有定义show_ color方法， 从父类Shape继承了show_ .color方法。 子类Circle和Rectangle改写(Override)了父类的area方法，分别提供了自己不同的实现。

注释掉Circle类中init方法中super(0._ init_ 0这行代码:

```
class Circle(Shape):
    def __init__(self,color,r):
        # super().__init__(color)
        self.r = r


```

再次运行代码，报错:

```
	print(self.color)
AttributeError: 'Circle' object has no attribute 'color'


```

错误输出指定的出错位置在: print(self.color) ，说Circle类 型对象没有color属性

```
class Shape:
	def show_color(self):
    	print(self.color)


```

问题原因是，Circle类型重写了父类Shape的_ init_ 0)方法，导致父类Shape的__ init\0方法没 有被调用到，

所以**一定不要忘记在子类的init方法中调用super().__ init __()**

## _ new _ 方法

python中定义的类在创建实例对象的时候，会自动执行**init()**方法，但是在执行**init()**方法之前，会执行
**new()**方法。

__ new _()_的作用主要有两个。

​	1.在内存中为对象分配空间

​	2.返回对象的引用。(即 对象的内存地址)

python解释器在获得引用的时候会将其传递给**init()**方法中的self。

```
class A:
    def __new__(cls, *args, **kwargs):
        print('__new__')
        #return super().__new__(cls)  # 这里一定要返回,否则__init__()方法不会被执行

    def __init__(self):  # 这里的self就是new方法中的return返回值
        print('__init__')

a = A()


```

输出结果

```
__new__
__init__


```

我们一定要在__ new __方法中最后调用

```
return super().__new__(cls)


```

否则init方法不会被调用

```
class A:
    def __new__(cls, *args, **kwargs):
        print('__new__')
        # return super().__new__(cls)  # 这里一定要返回,否则__init__()方法不会被执行

	def __init__(self):  # 这里的self就是new方法中的return返回值
    	print('__init__')

a = A()


```

输出

```
__new__


```

像以前一样,我们不写_ new _方法试试

```
class A:
    # def __new__(cls, *args, **kwargs):
        # print('__new__')
        # return super().__new__(cls)  # 这里一定要返回,否则__init__()方法不会被执行

	def __init__(self):  # 这里的self就是new方法中的return返回值
    	print('__init__')

a = A()


```

输出

```
__init__


```

## object---所有python类型的父类

在Python中，所有类型有个隐式的父类( object ),上面的代码相当于

```
class A(object):
    # def __new__(cls, *args, **kwargs):
        # print('__new__')
        # return super().__new__(cls)  # 这里一定要返回,否则__init__()方法不会被执行

    def __init__(self):  # 这里的self就是new方法中的return返回值
        print('__init__')


a = A()


```

当我们的类中没有定义_ new _ 方法时,创建对象时,Python会先调用父类(object) 的_ new _ 方法,在内存中创建一个实例,然后传递给我们的init方法.如果我们的自定义类型定义了 _ new _ 方法,就会覆盖父类(object)的 _ new\方法 (父类的 _ new\ 方法不会被自动调用)，所以我们要显式调用父类(object)的 _new\方法， 在内存中创建一个实例。

那么new有什么作用呢?我们可以改写它，举个例子，就比如说单例模式。

## 单例模式

如果我们创建两个实例: 

```
a1 = A()
a2 = A()


```

那么id(a1)和id(a2)的值不一样，也就是说python在内容当中创建了两个实例对象，用了两份内存。同样的东
西创建了两份

如果想不管创建多少个实例对象，我们都让它的id是一样的。

也就是说，先创建一个实例对象， 之后不管创建多少个，返回的永远都是第一个实例对象的内存地址。可以
这样实现:

```
# 重写new方法很固定，返可值必须是这个
# 这样就避免了创建多份。
# 创建第一个实例的时候，_instance是None, 那么会分配空间创建实例。
# 此时的类属性已经被修改，_instance不再为None
# 那么当之后实例属性被创建的时候，由于_instance不为None。
# 则返回第一个实例对象的引用，即内存地址。
# 这样就应用了单例模式。
class A:
    _instance = None
    def __new__(cls, *args, **kwargs):
        if A._instance == None:
            A._instance = super().__new__(cls)
        return A._instance


a1 = A()
print(id(a1))
a2 = A()
print(id(a2))
```

