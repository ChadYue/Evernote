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
