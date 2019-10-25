# 常用模块

## 时间处理模块

### time.time()

time time()返回当前时间的时间戳(1970纪元后经过的浮点秒数)。

```
import time
print(time . time())
```

输出:

```
1556846505.9781783
```

在Python的时间处理模块中，time 这个模块主要侧重于时间戳格式的处理，而datetime 则相当于time模块的高级封装，提供了更多关于日期处理的方法。

并且datetime的接口使用起来更加的直观，方便。

datetime主要由五个模块组成:

- **datetime.date**: 表示日期的类。常用的属性有year, month, day。
- **datetime.time**: 表示时间的类。常用的属性有hour, minute, second, microsecond.
- **datetime.datetime**: 表示日期+时间。
- **datetime.timedelta**: 表示时间间隔，即两个时间点之间的长度，常常用来做时间的加减。
- **datetime.tzinfo**: 与时区有 关的相关信息。

在datetime中，使用的最多的就是datetime .datetime模块，而datetime. timedelta常常被用来修改时间。

### datetime. datetime

```
class datetime.datetime(year, month, day, hour=0, minute=0, second=0, microsecond=0, tzinfo=None)
```

- MINYEAR <= year <= MAXYEAR
- 1<=month<=12
- 1 <= day <= number of days in the given month and year
- 0<=hour<24
- 0<= minute < 60
- 0<= second < 60
- 0<= microsecond < 1000000

这是datetime . datetime参数的取值范围，如果设定的值超过这个范围，那么就会抛出ValueError异常。其中year，month， day 是必须参数。

```
import datetime

datetime.datetime(year=2000, month=1, day=1, hour=12)
print(datetime.datetime(2000, 1, 1, 12, 0))
```

### datetime类方法

这些方法大多数用来生成一个datetime对象。

- classmethod datetime.**today()**

  获取今天的时间。

  ```
  import datetime
  print(datetime.datetime.today())
  ```

- classmethod datetime.now(tz=None)

  获取当前的时间。

  ```
  import datetime
  print(datetime.datetime.now())
  ```

- classmethod datetime fromtimestamp(timestamp, tz=None)

  用一个时间戳来生成datetime对象。

  **注:时间戳需要为10位的**

  ```
  import datetime
  print(datetime.datetime.fromtimestamp())
  ```

### datetime实例方法

这些方法大多是一个datetime 对象能进行的操作。

- datetime.**date()**和datetime.**time()**

  获取datetime对象的日期或者时间部分。

  ```
  import datetime
  print(datetime.datetime.now().date())
  print(datetime.datetime.now().time())
  >>>2019-07-19
  >>>09:46:44.237000
  ```

- datetime.**replace(year=self.year,  month=self.month,  day=self.day,  hour=self.hour, minute=self.minute,  second=self.second,  microsecond=self.microsecond, tzinfo=self.tzinfo,  * fold=o)**

  替换datetime对象的指定数据。

  ```
  import datetime
  now = datetime.datetime.now()
  >>>2019-07-19 09:46:44.237000
  print(now)
  print(now.replace(year=2000))
  >>>2000-07-19 09:46:44.237000
  ```

- datetime. timestamp()

  转换成时间戳。

  ```
  import datetime
  print(datetime.datetime.now().timestamp())
  >>>1563501104.95
  ```

- datetime.**weekday()**

  返回一个值，表示日期为星期几。0为星期一，6为星期天。

  ```
  import datetime
  print(datetime.datetime.now().weekday())
  >>>4
  ```

### datetime.timedelta

在实际的使用中，常常会遇到这样的需求:需要给某个时间增加或减少一天，甚至是增加或减少一天三小时二十分钟。

那么在遇到这样的需求时，去计算时间戳是非常的麻烦的，所以datetime. timedelta这个模块使能够非常方便的对时间做加减。

datetime是对某些运算符进行了重载的，所以可以如下操作。

```
import datetime
now = datetime.datetime.now()
print(now)
>>>2019-07-19 09:59:34.991000
now += datetime.timedelta(days=1)
print(now)
>>>2019-07-20 09:59:34.991000
now += datetime.timedelta(days=-1)
print(now)
>>>2019-07-19 09:59:34.991000
```

### strftime()和strptime()

datetime中提供了两个方法，可以方便的把datetime对象转换成格式化的字符串或者把字符串转换成datetime对象。

- 由datetime转换成字符串: **datetime.strftime()**

  strftime()是datetime对 象的实例方法:

  ```
  print(datetime.datetime.now().strftime('%Y-%m-%d %H:%M:%S'))
  >>>2019-07-19 10:05:51
  ```

- 由字符串转换成datetime : **datetime.datetime.strptime()**

  strptime()则是一个类方法:

  ```
  import datetime
  newsTime = 'Fri, 19 Jul 2019 10:09:32 GMT'
  GMT_FORWAT = '%a, %d %b %Y %H:%M:%S GMT'
  date = datetime.datetime.strptime(newsTime, GMT_FORWAT)
  print(date)
  >>>2019-07-19 10:09:32
  ```

以下是格式化的符号:

- %y	两位数的年份表示(00-99)
	 %Y	四位数的年份表示(000-9999 )
	 %m	月份(01-12)
	 %d	月内中的一天(0-31)
	 %H 	24小时制小时数(0-23)
	 %I 	12小时制小时数(01-12)
	 %M	分钟数(00=59)
	 %S	秒(00-59)
	 %a	本地简化星期名称
	 %A	本地完整星期名称
	 %b	本地简化的月份名称
	 %B	本地完整的月份名称
	 %c	本地相应的日期表示和时间表示
	 %j	年内的一天(001-366)
	 %p	本地A.M.或P.M.的等价符
	 %U	一年中的星期数(00-53) 星期天为星期的开始
	 %w	星期(0-6)，星期天为星期的开始
	 %W	一年中的星期数(00-53) 星期一为星期的开始
	 %x	本地相应的日期表示
	 %X	本地相应的时间表示
	 %Z	当前时区的名称
	 %% 	%号本身

## 目录操作模块

- 获取当前工作目录
- 获取执行命令的位置
- 路径拼接
- 路径拆分
- 文件重命名
- 删除文件
- 复制文件
- 遍历文件夹下的文件
- 判断文件是否存在
- 判断目录是否存在

### 获取当前工作目录

```
import sys
print(sys.path[0])
```

### 获取执行命令的位置

```
import os
print(os.getcwd())
```

### 路径拼接

由于不同的操作系统的路径分隔符不同，因此在做路径拼接时不要直接拼接字符串，而是通过os.path. join()函数，如下:

```
import os
os.path.join('/User/pangao', 'test.txt')
```

#### 路径拆分

同理，使用os.path.split() 函数拆分路径，如下:

```
import os
os.path.split('/User/pangao/test.txt')
```

os. path.splitext()可以直接获取文件扩展名，很方便，如下:

```
import os
os.path.splitext('/User/pangao/test.txt')
```

这些合并、拆分路径的函数并不会检测目录和文件是否真实存在，他们仅仅是对字符串进行操作。

### 文件重命名

假定当前目录下有一个test.txt 文件，如下:

```
import os
os.rename('test.txt', 'test.py')
```

### 删除文件

假定当前目录下有一个test.txt 文件，如下:

```
import os
os.remove('test.txt')
```

### 复制文件

os模块中没有复制图数，幸运的是shutil模头提供了cpynleO的函数，你还可以在shutil模块中找到很多实
用函数，它们可以看做是os模块的补充，如下:

```
import shutil
shutil.copyfile('test.py','test.txt')
```

### 遍历文件夹下的文件

方法1:使用os.listdir 获取当前目录下的文件和文件夹，如下:

```
import os
for filename in os.listdir('./'):
    print(filename)
>>>__init__.py
>>>note·19.07.19-常用模块.md
>>>test.py
>>>Demo01·19.07.19.py
```

方法2:使用glob 模块，可以设置文件过滤，如下:

```
import glob
for filename in glob.glob('*.py'):
    print(filename)
>>>__init__.py
>>>test.py
>>>Demo01·19.07.19.py
```

方法3:通过os.walk，可以访问子文件夹，如下:

```
import os
for fpathe, dirs, fs in os.walk('./'):
    print(fpathe)
    print(dirs)
    print(fs)
    for f in fs:
        print(os.path.join(fpathe,f))
>>>./
>>>[]
>>>['__init__.py', 'note·19.07.19-常用模块.md', 'test.py', 'Demo01·19.07.19.py']
>>>./__init__.py
>>>./note·19.07.19-常用模块.md
>>>./test.py
>>>./Demo01·19.07.19.py
```

### 判断文件是否存在

```
import os

print(os.path.isfile('text.txt'))
>>>False  # 不存在
```

### 判断目录是否存在

```
import os

print(os.path.exists('directory'))
>>>False  # 不存在
```

### 随机数模块

- random模块Python中产生随机数需要导入random模块:

```
import random
```

#### 随机数模块常用方法

- random.randint(a, b): 返回a和b之间的随机整数;

```
import random
print(random.randint(0,10))
>>>2
print(random.randint(0,10))
>>>9
print(random.randint(0,10))
>>>1
```

- random.random():返回0到1之间随机数(不包括1);

```
import random
print(random.random())
>>>0.8203933192825534
print(random.random())
>>>0.6182501341799476
print(random.random())
>>>0.9569667618922727
```

- random.choice(seq):在不为空的序列中随机选择一个元素;

```
import random
s = 'helloworld'
print(random.choice(s))
>>>e
print(random.choice(s))
>>>l
```

random.sample(population,k):在一一个序列或者集合中选择k个随机元素()，返回由K个元素组成新的
列表; (k的值 小于population的长度)

```
import random
print(random.sample('12345', 2))
>>>['1', '5']
print(random.sample('12345', 5))
>>>['2', '5', '1', '3', '4']
print(random.sample('12345', 6))
Traceback (most recent call last):
  File "F:/ch07-19/Demo01·19.07.19.py", line 30, in <module>
    print(random.sample('12345', 6))
  File "C:\Users\Administrator\AppData\Local\Programs\Python\Python36\lib\random.py", line 318, in sample
    raise ValueError("Sample larger than population or is negative")
ValueError: Sample larger than population or is negative
```

- random.uniform(a, b):产生一个指定范围内的随机浮点数若a<b,随机数n范围: a<=n<=b;若a>b,随机数n范围: a<=n<=b;

```
import random
print(random.uniform(1, 10))
>>>4.037093273751194
print(random.uniform(10, 1))
>>>2.622363310815394
```

- random.randrange(start, stop=None, step=1,_int=): 在rang(start,stop,step)中选择一个随机数;

```
import random
print(random.randrange(1, 10, 1))
>>>5
print(random.randrange(1, 10, 1))
>>>6
print(random.randrange(1, 100, 2))
>>>97
print(random.randrange(1, 100, 2))
>>>65
```

- random.shuffle(x,random = None):将列表顺序打乱;

```
import random
C = ['C++', 'C', 'Java', 'C#', 'Python']
random.shuffle(C, random=None)
print(C)
>>>['C', 'C++', 'Python', 'C#', 'Java']
random.shuffle(C, random=None)
print(C)
>>>['C#', 'C', 'C++', 'Java', 'Python']
```

### Collections模块

该模块实现了专门的容器数据类型，为Python的通用内置容器提供了替代方案。以下几种类型用的很多:

- **defaultdict**(dict子类调用工厂函数来提供缺失值)
- **counter**(用于计算可哈希对象的dict子类)
- **deque**(类似于列表的容器，可以从两端操作)
- **namedtuple**(用于创建具有命名字段的tuple子类的工厂函数)
- **OrderedDict**(记录输入顺序的dict)

#### defaultdict

**其实就是一个查不到key值时不会报错的dict**

**应用实例**

首先来看一个用正常dict的例子，如果创建了一个叫person的字典，里面存储的key值为name, age, 如果这
时候尝试调用person['city'],会抛出KeyError错误，因为没有city这个键值:

```
person = {'name': 'xiaobai','age': 18}
print("The value of key 'name' is :",person['name'])
>>>The value of key 'name' is : xiaobai
print("The value of key 'city' is :",person['city'])
>>>Traceback (most recent call last):
	 File "F:/ch07-19/Demo01·19.07.19.py", line 35, in <module>
    	print("The value of key 'city' is :",person['city'])
   KeyError: 'city'
```

现在如果用defaultdict再试试呢?

```
from collections import defaultdict
person = defaultdict(lambda : 'Key Not found')

person['name'] = 'xiaobai'
person['age'] = 18

print("The value of key 'name' is :",person['name'])
>>>The value of key 'name' is : xiaobai
print("The value of key 'city' is :",person['city'])
>>>The value of key 'city' is : Key Not found
```

大家可以发现，这次没有问题了，其实最根本的原因在于当创建defaultdict时，首先传递的参数是所有key的默认value值，之后添加name, age进 去的时候才会有所改变，当最终查询时，如果key存在，那就输出对应的value值，如果不存在，就会输出事先规定好的值'Key Not Found'

除此之外外，还可以利用defaultdict创建时，传递参数为所有key默认value值这一特性，实现一些其他的功能,比如: 

```
from collections import defaultdict
d = defaultdict(list)
d['person'].append("xiaobai")
d['city'].append("paris")
d['person'].append("student")

for i in d.items():
    print(i)
>>>('person', ['xiaobai', 'student'])
>>>('city', ['paris'])
```

一个道理，默认所有key对应的是一个list,自然就可以在赋值时使用list的append方法了。再比如下面这个例子:

```
food = (
    ('jack', 'milk'),
    ('Ann', 'fruits'),
    ('Arham', 'ham'),
    ('Ann', 'soda'),
    ('jack', 'dumplings'),
    ('Ahmed','fried chicken')
)
favourite_food = defaultdict(list)

for n, f in food:
    favourite_food[n].append(f)

print(favourite_food)
>>>defaultdict(<class 'list'>, {'jack': ['milk', 'dumplings'], 'Ann': ['fruits', 'soda'], 'Arham': ['ham'], 'Ahmed': ['fried chicken']})
```

道理和上面差不多，这里大家可以自己拓展，展开想象，相信可能在某个时刻可以用的上defaultdict这个容

#### counter

Counter是dict的子类。因此，它是一-个无序集合，其中元素及其各自的计数存储为字典。

就是一个计数器，**一个字典，key就是出现的元素，value 就是该元素出现的次数**

**应用实例**

```
from collections import Counter

count_list = Counter(['B', 'B', 'A', 'B', 'C', 'A', 'B', 'B', 'A', 'C'])
print(count_list)
>>>Counter({'B': 5, 'A': 3, 'C': 2})
count_tuple = Counter((2, 2, 2, 3, 1, 3, 1, 1, 1))
print(count_tuple)
>>>Counter({1: 4, 2: 3, 3: 2})
```

**Counter一般不会用于dict和set的计数，因为dict的key是唯一的， 而set本身就不能有重复元素**现在也可以直接把在defaultdict例子中用过food元组拿来计数:

```
from collections import Counter
food = (
    ('jack', 'milk'),
    ('Ann', 'fruits'),
    ('Arham', 'ham'),
    ('Ann', 'soda'),
    ('jack', 'dumplings'),
    ('Ahmed', 'fried chicken')
)
favourite_food_count = Counter(n for n, f in food) #统计name出 现的饮数
print(favourite_food_count)
>>>Counter({'jack': 2, 'Ann': 2, 'Arham': 1, 'Ahmed': 1})
```

#### deque

在需要在容器两端的更快的添加和移除元素的情况下，可以使用deque.

deque就是一个可以两头操作的容器，类似list但比列表速度更快

**应用实例**

deque的方法有很多，很多操作和list类似，也支持切片

```
from collections import deque
d = deque()
d.append(1)
d.append(2)

print(len(d))
>>>2
print(d[0])
>>>1
print(d[-1])
>>>2
```

deque 最大的特点在于可以从两端操作:

```
from collections import deque
d = deque([i for i in range(5)])
print(len(d))
>>>5
print(d.popleft())
>>>0
print(d.pop())
>>>4
print(d)
>>>deque([1, 2, 3])
d.append(100)
d.append(-100)
print(d)
>>>deque([1, 2, 3, 100, -100])
```

除了这些deque的方法实在太多了，比如再举几个常用的例子，首先定义一个deque时可以规定它的最大长度，deque和list一样也支持extend方法，方便列表拼接，但是deque提供双向操作: 

```
from collections import deque
d = deque([1, 2, 3, 4, 5], maxlen=9)
d.extendleft([0])
d.extend([6, 7, 8])
print(d)
>>>deque([0, 1, 2, 3, 4, 5, 6, 7, 8], maxlen=9)
```

现在d已经有9个元素了，而规定的maxlen=9,这个时候如果从左边添加元素，会自动移除最右边的元素，反之也是一样:

```
d.append(100)
print(d)
d.appendleft(-100)
print(d)
>>>deque([1, 2, 3, 4, 5, 6, 7, 8, 100], maxlen=9)
>>>deque([-100, 1, 2, 3, 4, 5, 6, 7, 8], maxlen=9)
```

#### OrderedDict

**基础概念**

"OrderedDict"本身就是一个dict, 但是它的特别之处在于会记录插入**dict**的**key**和**value**的顺序

**应用实例**

```
from collections import OrderedDict
d = {}
d['a'] = 1
d['b'] = 2
d['c'] = 3
d['d'] = 4
print(d)
>>>{'a': 1, 'b': 2, 'c': 3, 'd': 4}
```

大家可以看到，这是一个普通的dict,因为无序，即使依次添加了a,b,c,d四个键并赋予value,但是输出的顺序并不可控。OrderedDict的出现就是为了解决这个问题:

```
d = OrderedDict()
d['a'] = 1
d['b'] = 2
d['c'] = 3
d['d'] = 4
print(d)
>>>OrderedDict([('a', 1), ('b', 2), ('c', 3), ('d', 4)])
```

这回输出时好多了,因为会自动记录插入顺序,同理,如果删除一个key, OrderedDict的顺序不会发生变化:

```
from collections import OrderedDict

print("Before deleting:\n")
od = OrderedDict()
od['a'] = 1
od['b'] = 2
od['c'] = 3
od['d'] = 4
for key, value in od.items():
    print(key, value)
Before deleting:

a 1
b 2
c 3
d 4
print("\nAfter deleting:\n")
od.pop('c')
for key, value in od.items():
    print(key, value)
After deleting:

a 1
b 2
d 4
print("\nAfter re-inserting:\n")
od['c'] = 3
for key, value in od.items():
    print(key, value)
After re-inserting:

a 1
b 2
d 4
c 3
```

### pickle模块

python对象的序列化与反序列化

特点

1. 只能在python中 使用，只支持python的 基本数据类型。
2. 可以处理复杂的序列化语法。 (例如自定义的类的方法，游戏的存档等)

一、内存中操作: dumps方法将 对象转成字节(序列化) loads方法将字节还原为对象(反序列化)

```
import pickle
# dumps
li = [11, 22, 33]
r = pickle.dumps(li)
print(r)
>>>b'\x80\x03]q\x00(K\x0bK\x16K!e.'
# loads
result = pickle.loads(r)
print(result)
>>>[11, 22, 33]
```

二、文件中操作

```
import pickle
# dumps
li = [11, 22, 33]
pickle.dump(li, open('db', 'wb'))
# load
ret = pickle.load(open('db','rb'))
print(ret)
>>>[11, 22, 33]
```