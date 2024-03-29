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







