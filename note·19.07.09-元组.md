# 元组

#### 创建

使用“=”将一个元组赋值给变量

```
x = (1,2,3)
print(x)
>>>(1, 2, 3)
```

创建一个只有一个元素的元组

```
x = (3)
print(type(x))
x = (3,)
print(type(x))
>>><class 'int'>
>>><class 'tuple'>
```

创建空元组的方法

```
x = ()
print(x)
x= tuple()
print(x)
>>>()
>>>()
```

使用tuple函数将其他序列转换成元组

```
print(tuple(range(5)))
print(tuple('asdfghjkl'))
alist = [1,2,3,4,5,6,7,8,9]
print(tuple(alist))
>>>(0, 1, 2, 3, 4)
>>>('a', 's', 'd', 'f', 'g', 'h', 'j', 'k', 'l')
>>>(1, 2, 3, 4, 5, 6, 7, 8, 9)
```

#### 删除

使用del可以删除元组对象,不能删除元组中的元素