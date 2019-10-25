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