# 深拷贝和浅拷贝

Python赋值操作或函数参数传递，传递的永远是对象引用(即内存地址)，而不是对象内容。在Python中一切皆对象，对象又分为可变(mutable)和不可变(immutable)两种类型。对象拷贝是指在内存中创建新的对象，产生新的内存地址。当顶层对象和它的子元素对象全都是immutable不可变对象时，不存在被拷贝，因为没有产生新对象。浅拷贝(Shallow Copy),拷贝顶层对象，但不会拷贝内部的子元素对象。深拷贝(Deep Copy),递归拷贝顶层对象，以及它内部的子元素对象

## 可变对象与不可变对象

Python中一切皆对象，对象就像一个塑料盒子，里面装的是数据。对象有不同类型，例如布尔型和整型，类型决定了可以对它进行的操作。现实生活中的"陶器"会暗含一些信息(例如它可能很重且易碎，注意不要掉到地上)。

对象的类型还决定了它装着的数据是允许被修改的变量(可变的mutable )还是不可被修改的常量(不可变的immutable )。你可以把不可变对象想象成-一个透明但封闭的盒子:你可以看到里面装的数据，但是无法改变它。类似地，可变对象就像一一个开着口的盒子，你不仅可以看到里面的数据，还可以拿出来修改它，但你无法改变这个盒子本身，即你无法改变对象的类型。

- mutable :可变对象，如List、Dict
- immutable :不可变对象，如Number、String 、Tuple 、Frozenset

注意: Python赋 值操作或函数参数传递，传递的永远是对象引用(即内存地址)，而不是对象内容。

```
a = 1
b = a
print(id(a))
>>>499411984
print(id(b))
>>>499411984
b += 1
print(a)
>>>1
print(b)
>>>2
print(id(a))
>>>499411984
print(id(b))
>>>499412016
```

Python会缓存使用非常频繁的小整数-5至256、ISO/IEC  8859-1单字符、只包含大小写英文字母的字符
串，以对其复用，不会创建新的对象:

```
a = 10
b = 10
print(id(a))
print(id(b))
>>>496397616
>>>496397616
a = '@'
b = '@'
print(id(a))
print(id(b))
>>>31179584
>>>31179584
a = 'HELLOWORLDhelloworld'
b = 'HELLOWORLDhelloworld'
print(id(a))
print(id(b))
>>>40738296
>>>40738296
```

## copy模块

对象拷贝是指在内存中创建新的对象，产生新的内存地址。

- 浅拷贝只拷贝最外层对象，深拷贝还会递归拷贝内层对象
- 无论是浅拷贝还是深拷贝，只拷贝mutable可变对象成为一个新对象，而immutable不可变对象还是原来的那个
- 当顶层对象和它的子素对象全都是immutable不可变对象时，因为没有产生新对象，所以不存在被拷贝

### 浅拷贝

浅拷贝(Shallow Copy)，拷贝顶层对象，但不会拷贝内部的子元素对象。

#### 顶层是mutable,子元素全是inmutable

当顶层对象是mutable可变对象，但是它的子元素对象全都是immutable不可变对象时，如[1, 'world', 2]

**创建列表对象并赋值给变量a**

```
a = [1, 'world', 2]
print([id(item) for item in a])
print(id(a))
>>>[495021072, 31245120, 495021104]
>>>42242312
```

导入copy模块，使用copy.copy()函数浅拷贝a，并赋值给变量b

```
import copy
b = copy.copy(a)
print(b)
print([id(item) for item in b])
print(id(b))
>>>[1, 'world', 2]
>>>[495021072, 31245120, 495021104]
>>>42242504
```

修改变量a的子元素a[0]=3,由于整数是不可变对象,所有并不是修改1变成3,而是更改a[0]指向对象3

```
a[0] = 3
print(a)
print(b)
print([id(item) for item in a])
print([id(item) for item in b])
>>>[3, 'world', 2]
>>>[1, 'world', 2]
>>>[491613264, 31245120, 491613232]
>>>[491613200, 31245120, 491613232]
```

#### 顶层是mutable,子元素部分immutable

当顶层对象是mutable可变对象，但子元素也存在mutable可变对象时，如[1, 2, ['hello','world'l]

**浅拷贝copy.copy() 只拷贝了顶层对象，没有拷贝子元素对象['hello' ,'world'],即a[2]和b[2]指向同一个列表对象**

```
import copy
a = [1, 2, ['hello', 'world']]
b = copy.copy(a)
print(id(a))
>>>36917832
print(id(b))
>>>36919112
print([id(item) for item in a])
>>>[499149840, 499149872, 36917640]
print([id(item) for item in b])
>>>[499149840, 499149872, 36917640]
print([id(item) for item in a[2]])
>>>[31179584, 31969496]
print([id(item) for item in b[2]])
>>>[31179584, 31969496]
```

修改(a[2])[1] = 'china' , 则(b[2])[1] = 'china'

```
import copy
a = [1, 2, ['hello', 'world']]
b = copy.copy(a)
a[2][1] = 'china'
print(a)
>>>[1, 2, ['hello', 'china']]
print(b)
>>>[1, 2, ['hello', 'china']]
print([id(item) for item in a[2]])
>>>[31245120, 35705608]
print([id(item) for item in b[2]])
>>>[31245120, 35705608]
```

#### 顶层是immutable,子元素全是inmnutable

当顶层对象是immutable不可变对象，同时它的子元素对象也全都是immutable不可变对象时，如(1, 2, 3)

```
import copy
a = (1, 2, 3)
b = copy.copy(a)
print(id(a))
>>>35159928
print(id(b))
>>>35159928
print([id(item) for item in a])
>>>[502033424, 502033456, 502033488]
print([id(item) for item in b])
>>>[502033424, 502033456, 502033488]
```

变量a与变量b指向的是同一个元组对象，没有拷贝

#### 顶层是immutable,子元素部分mutable

当顶层对象是immutable不可变对象时，但子元素存在mutable可变对象时，如(1, 2, ['hello','world'])

```
import copy
a = (1, 2, ['hello', 'world'])
b = copy.copy(a)
print(id(a))
>>>35553144
print(id(b))
>>>35553144
print([id(item) for item in a])
>>>[494627856, 494627888, 42299784]
print([id(item) for item in b])
>>>[494627856, 494627888, 42299784]
print([id(item) for item in a[2]])
>>>[31310656, 35639512]
print([id(item) for item in b[2]])
>>>[31310656, 35639512]
a[2][1] = 'china'
print(a)
>>>(1, 2, ['hello', 'china'])
print(b)
>>>(1, 2, ['hello', 'china'])
```

变量a与变量b指向的是相同的元组对象，并且a[2] 与b[2]指向同一个列表，所以修改(a[2])[1] 会影
响(b[2])[1]

### 深拷贝

深拷贝(Deep Copy)，递归拷贝顶层对象，以及它内部的子元素对象

#### 顶层是mutable, 子元素全是immutable

当顶层对象是mutable可变对象，但是它的子元素对象全都是immutable不可变对象时，如[1, 'world', 2]

```
import copy
a = [1, 'world', 2]
b = copy.deepcopy(a)
print(id(a))
>>>42094984
print(id(b))
>>>42095176
print([id(item) for item in a])
>>>[505179152, 34718528, 505179184]
print([id(item) for item in b])
>>>[505179152, 34718528, 505179184]
a[0] = 3
print(a)
>>>[3, 'world', 2]
print(b)
>>>[1, 'world', 2]
print([id(item) for item in a])
>>>[505179216, 34718528, 505179184]
print([id(item) for item in b])
>>>[505179152, 34718528, 505179184]
```

变量a与变量b指向不同的列表对象，修改a[e]只是将列表a的第-个元素重新指向新对象，不会影响b[0]

#### 顶层是mutable,子元素部分mutable

当顶层对象是mutable可变对象，但子元素也存在mutable可变对象 时，如[1, 2, ['hello', 'world'l]

```
import copy
a = [1, 2, ['hello', 'world']]
b = copy.deepcopy(a)
print(id(a))
>>>42226248
print(id(b))
>>>42227528
print([id(item) for item in a])
>>>[503475216, 503475248, 42226056]
print([id(item) for item in b])
>>>[503475216, 503475248, 42227464]
print([id(item) for item in a[2]])
>>>[34849600, 40751320]
print([id(item) for item in b[2]])
>>>[34849600, 40751320]
a[2][1] = 'china'
print(a)
>>>[1, 2, ['hello', 'china']]
print(b)
>>>[1, 2, ['hello', 'world']]
print([id(item) for item in a[2]])
>>>[5882688, 32035592]
print([id(item) for item in b[2]])
>>>[5882688, 32035032]
```

深拷贝既拷贝了顶层对象，又递归拷贝了子元素对象，所以a[2]与b[2]指向了两个不同的列表对象(但是列表对象的子元素初始指定的字符串对象一样)，修改(a[2])[1] = 'china'后，它重新指向了新的字符串对象(内存地址为140531581905808 )，不会影响到(b[2])[1]

#### 顶层是immutable,子元素全是inmutable

当顶层对象是immutable不可变对象，同时它的子元素对象也全都是imutable不可变对象时，如(1, 2, 3)

```
import copy
a = (1, 2, 3)
b = copy.deepcopy(a)
print(id(a))
>>>32079736
print(id(b))
>>>32079736
print([id(item) for item in a])
>>>[498035728, 498035760, 498035792]
print([id(item) for item in b])
>>>[498035728, 498035760, 498035792]
```

变量a与变量b指向的是同一个元组对象，不存在拷贝

#### 顶层是immutable, 子元素部分mutable

当顶层对象是immutable不可变对象 时，但子元素存在mutable可变对象 时，如(1, 2, ['hello','world'])

```
import copy
a = (1, 2, ['hello', 'world'])
b = copy.deepcopy(a)
print(id(a))
>>>35618680
print(id(b))
>>>42398848
print([id(item) for item in a])
>>>[502492176, 502492208, 42375368]
print([id(item) for item in b])
>>>[502492176, 502492208, 42376840]
print([id(item) for item in a[2]])
>>>[31245120, 35705048]
print([id(item) for item in b[2]])
>>>[31245120, 35705048]
a[2][1] = 'china'
print(a)
>>>(1, 2, ['hello', 'china'])
print(b)
>>>(1, 2, ['hello', 'world'])
print([id(item) for item in a[2]])
>>>[31245120, 35705608]
print([id(item) for item in b[2]])
>>>[31245120, 35705048]
```

变量a与变量b指向的是不同的元组对象，同时a[2] 与b[2] 指向不同的列表对象，所以修改(a[2])[1]不会影响(b[2])[1]

## 其他拷贝方式

### 列表的复制

```
a = [1, 2, 3]
b = a
print(b)
>>>[1, 2, 3]
a[0] = 'wangy'
print(a)
>>>['wangy', 2, 3]
print(b)
>>>['wangy', 2, 3]
```

使用=是赋值，即将列表对象的引用也赋值给变量b，可以将列表对象想像成一个盒子，变量a相当于这个盒子上的标签，执行b = a后，相当于再在这个盒子上贴上b标签，a 和b实际上指向的是同一个对象。因此，无论我们是通过a还是通过b来修改列表的内容，其结果都会作用于双方。

列表的复制都相当于浅拷贝效果，有以下三种方式:

- 列表的copy()函数
- list()转换函数
- 列表分片[:]

```
a = [1, 2, ['hello', 'world']]
b = a.copy()
c = list(a)
d = a[:]
print(id(a), id(b), id(c), id(d))
>>>35984200 35985288 35986248 35985224
a[0] = 100
a[2][1] = 'wangy'
print(a)
>>>[100, 2, ['hello', 'wangy']]
print(b)
>>>[1, 2, ['hello', 'wangy']]
print(c)
>>>[1, 2, ['hello', 'wangy']]
print(d)
>>>[1, 2, ['hello', 'wangy']]
```
b/c /d都是a的复制，它们都指向了不同的列表对象，但是没有拷贝子元素，a[2] 和b[2]/ c[2] / d[2]指向同-一个列表，**相当于浅拷贝的效果**

### 元组的复制

```
a = (1, 2, ['hello', 'world'])
b = a[:]
print(id(a), id(b))
>>>40861560 40861560
print(a)
>>>(1, 2, ['hello', 'world'])
print(b)
>>>(1, 2, ['hello', 'world'])
a[2][1] = 'wangy'
print(a)
>>>(1, 2, ['hello', 'wangy'])
print(b)
>>>(1, 2, ['hello', 'wangy'])
```

使用分片[:] 操作，a和b其实是指向同一个元组，而且没有拷贝子元素，a[2] 和b[2]也指向同一个列表，**相当于浅拷贝的效果**

### 字典的复制

同列表类似，可以使用字典的copy()函数或者转换函数dict()

```
a = {'name': 'wangy', 'age': 18, 'jobs': ['devops', 'dba']}
b = a.copy()
c = dict(a)
print(id(a), id(b), id(c))
>>>34635208 34635280 40541712
a['age'] = 20
a['jobs'].append('python')
print(a)
>>>{'name': 'wangy', 'age': 20, 'jobs': ['devops', 'dba', 'python']}
print(b)
>>>{'name': 'wangy', 'age': 18, 'jobs': ['devops', 'dba', 'python']}
print(c)
>>>{'name': 'wangy', 'age': 18, 'jobs': ['devops', 'dba', 'python']}
```

变量a与变量b/c指向不同的字典，但是没有拷贝子元素，a['jobs'] 和b['jobs'] / c["jobs']指定同一个列表，**相当于浅拷贝的效果**

### 集合的复制

同列表类似，可以使用集合的copy()函数或者转换函数set()

```
a = {1, 2, 3}
b = a.copy()
c = set(a)
print(id(a), id(b), id(c))
>>>31381320 32154792 32156136
a.add('wangy')
print(a)
>>>{1, 2, 3, 'wangy'}
print(b)
>>>{1, 2, 3}
print(c)
>>>{1, 2, 3}
```

变量a与变量b/c指向不同的集合，而集合的元素必须是hashable，所以修改集合a不会影响到b/c