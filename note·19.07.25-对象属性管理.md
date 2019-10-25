## 对象属性管理

Python下一切皆对象，每个对象都有多个属性(attribute), Python对属性有一 套统一 -的管理方案。 dict是 用来存储对象属性的一个字典，其键为属性名，值为属性的值。

### __ dict __

```
class Spring(object):
    # season 为类的属性
    season = 'the spring of class'


print(Spring.__dict__)
>>>{'__module__': '__main__', 'season': 'the spring of class', '__dict__': <attribute '__dict__' of 'Spring' objects>, '__weakref__': <attribute '__weakref__' of 'Spring' objects>, '__doc__': None}
print(Spring.__dict__['season'])
>>>the spring of class
print(Spring.season)
>>>the spring of class
```

Spring.__ dict __ ['season']就是访问类属性，同时通过.号也可以访问该类属性

```
class Spring(object):
    # season 为类的属性
    season = 'the spring of class'


s = Spring()
print(s.__dict__)
>>>{}
```

实例属性的__ dict __是空的，**因为season是属于类属性**

```
class Spring(object):
    # season 为类的属性
    season = 'the spring of class'


s = Spring()
print(s.season)
>>>the spring of class
```

**s.season是指向了类属性中Spring.season**

```
class Spring(object):
    # season 为类的属性
    season = 'the spring of class'


# 类实例化
s = Spring()
# 建立实例对象
s.season = 'the spring of instance'
print(s.season)
print(s.__dict__)
>>>the spring of instance
>>>{'season': 'the spring of instance'}
```

这样实例属性里面就不空了，这时候建立的s.season属性与上面s.season(类属性)重名，并且把原来的“遮盖了”                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          

```
class Spring(object):
    # season 为类的属性
    season = 'the spring of class'


# 类实例化
s = Spring()
# 建立实例对象
s.season = 'the spring of instance'
print(Spring.season)
print(Spring.__dict__['season'])
the spring of class
the spring of class
>>>the spring of class
>>>the spring of class
```

**由上我们看到Spring类season属性并没有受到实例影响，其原因是实例s对象建立时s.season未初始化则会自动指向类属性，如果实例属性被修改那么就不指向类属性，同时类属性也不会受到影响**

```
class Spring(object):
    # season 为类的属性
    season = 'the spring of class'


# 类实例化
s = Spring()
# 建立实例对象
s.lang = 'python'
print(Spring.lang)
print(Spring.season)
print(Spring.__dict__['season'])
>>>Traceback (most recent call last):
  	 File "F:/ch07-25/Demo02·19.07.25.py", line 10, in <module>
        print(Spring.lang)
   AttributeError: type object 'Spring' has no attribute 'lang'
```

上明错误表面实例对象添加内容，不是类属性

```
class Spring:
    def tree(self, x):
        self.x = x
        print(self.x)

print(Spring.__dict__['tree'])
>>><function Spring.tree at 0x00000000021DF7B8>
```

在类属性是存在tree方法

```
# 定义一个类
class Spring:
    def tree(self, x):
        self.x = x
        print(self.x)


s = Spring()
print(Spring.__dict__['tree'])
print(s.__dict__['tree'])
>>><function Spring.tree at 0x000000000271F7B8>
>>>Traceback (most recent call last):
     File "F:/ch07-25/Demo02·19.07.25.py", line 29, in <module>
       print(s.__dict__['tree'])
   KeyError: 'tree'
```

但是实例对象sdict方法里不存在tree方法

```
# 定义一个类
class Spring:
    def tree(self, x):
        self.x = x
        print(self.x)


s = Spring()
s.tree('123')
>>>123
```

但是s能调用tree方法，其原因是s.tree指向了Spring.tree方法。实例s与self新建 了对应关系，两者是一个外一个内，在方法中self.x=x.将x值赋给了self.x,也就是实例应该拥有这么一个属性。self相当于java中this指针

```
# 定义一个类
class Spring:
    def tree(self, x):
        self.x = x
        print(self.x)


s = Spring()
s.tree('123')
print(s.__dict__)
>>>123
>>>{'x': '123'}
```

即实例方法(s.tree('123'))的第一个参数 (self, 但没有写出来)绑定实例s，透过self.x来设定值，给s.dict添加属性值

换一个角度来看

```
# 定义一个类
class Spring:
    def tree(self, x):
        print(x)


s = Spring()
s.tree('123')
print(s.__dict__)
>>>123
>>>{}
```

再看一个例子

```
class Person(object):
    name = 'python'
    age = 18

    def __init__(self):
        self.sex = 'boy'
        self.like = 'papapa'

    @staticmethod
    def stat_func():
        print('this is stat_func')

    @classmethod
    def class_func(cls):
        print('class_func')


person = Person()
print('Person.__dict__:', Person.__dict__)
>>>Person.__dict__: {'__module__': '__main__', 'name': 'python', 'age': 18, '__init__': <function Person.__init__ at 0x00000000026DF7B8>, 'stat_func': <staticmethod object at 0x00000000026DDB38>, 'class_func': <classmethod object at 0x00000000026DDB70>, '__dict__': <attribute '__dict__' of 'Person' objects>, '__weakref__': <attribute '__weakref__' of 'Person' objects>, '__doc__': None}
print('person.__dict__:', person.__dict__)
>>>person.__dict__: {'sex': 'boy', 'like': 'papapa'}
```

由此可见，类的普通方法、类方法、静态方法、全局变量以及- -些内置的属性都是放在类对象dict里而实例对象中存储了一些self.xxx的一些东西
在类的继承中，子类有自己的dict,父类也有自己的dict,子类的全局变量和方法放在子类的dict中，父类的放在父类dict中。

```
class Person(object):
    name = 'python'
    age = 18

    def __init__(self):
        self.sex = 'boy'
        self.like = 'papapa'

    @staticmethod
    def stat_func():
        print('this is stat_func')

    @classmethod
    def class_func(cls):
        print('class_func')


class Hero(Person):
    name = 'super man'
    age = 1000

    def __init__(self):
        super(Hero, self).__init__()
        self.is_good = 'yes'
        self.power = 'fly'


person = Person()
print('Person.__dict__:', Person.__dict__)
print('person.__dict__:', person.__dict__)

hero = Hero()
print('Hero.__dict__:', Hero.__dict__)
print('hero.__dict__:', hero.__dict__)
```

运行结果

```
Person.__dict__: {'__module__': '__main__', 'name': 'python', 'age': 18, '__init__': <function 					Person.__init__ at 0x000000000220F840>, 'stat_func': <staticmethod object at 				 0x000000000220DD68>, 'class_func': <classmethod object at 0x000000000220DDA0>, 				'__dict__': <attribute '__dict__' of 'Person' objects>, '__weakref__': 						<attribute '__weakref__' of 'Person' objects>, '__doc__': None}
person.__dict__: {'sex': 'boy', 'like': 'papapa'}
Hero.__dict__: {'__module__': '__main__', 'name': 'super man', 'age': 1000, '__init__': 				  <function Hero.__init__ at 0x000000000220F9D8>, '__doc__': None}
hero.__dict__: {'sex': 'boy', 'like': 'papapa', 'is_good': 'yes', 'power': 'fly'}
```

从运行结果可以看出，类对象的dict虽然没有继承父类的，但是实例对象继承了父类的实例属性

### __ slots __

现在我们终于明白了，动态语言与静态语言的不同

- 动态语言:可以在运行的过程中，修改代码
- 静态语言:编译时已经确定好代码，运行过程中不能修改

如果我们想要限制实例的属性怎么办?比如，只允许对Person实例添加name和age属性。

为了达到限制的目的，Python允许 在定义class的时候，定义一个特殊的__ slots __变量， 来限制该class实例能添加的属性:

```
class Person:
    __slots__ = ('name', 'age')

    def __init__(self, name, age):
        self.name = name
        self.age = age
        

p = Person('老王', 20)
p.score = 100
>>>Traceback (most recent call last):
     File "F:ch07-25/Demo02·19.07.25.py", line 78, in <module>
       p.score = 100
   AttributeError: 'Person' object has no attribute 'score'
```

注意:使用__ slots __ 要注意， __ slots __定义的属性仅对当前类实例起作用，对继承的子类是不起作用的

```
class Person:
    __slots__ = ('name', 'age')

    def __init__(self, name, age):
        self.name = name
        self.age = age


class GoodPerson(Person):
    pass


p = GoodPerson('老王', 20)
p.score = 100
print(p)
>>><__main__.GoodPerson object at 0x0000000002208288>
```

当你定义__ slots __ 后， Python就 会为实例使用-种更加紧凑的内部表示。实例通过一个很小的固定大小的数组来构建，而不是为每个实例定义一个字典。所以 __ slots __ 是创建大量对 象时节省内存的方法。 __ slots __ 的副作用是作为一个封装工具来防止用户给实例增加新的属性。尽管使用slots可以达到这样的目的，但是这个并不是它的初衷。

## 属性管理

### hasattr()函数

hasattr()函数用于判断对象是否包含对应的属性

```
语法:
	hasattr(object, name)

参数:
	object--对象
	name--字符串,属性名
	
返回值:
	如果对象有该属性返回True,否则返回False
```

示例:

```
class People:
    country = 'China'

    def __init__(self, name):
        self.name = name

    def people_info(self):
        print('%s is xxx'% self.name)


obj = People('aaa')

print(hasattr(People, 'country'))
>>>True
print('country' in People.__dict__)
>>>True
print(hasattr(obj, 'people_info'))
>>>True
print(People.__dict__)
>>>{'__module__': '__main__', 'country': 'China', '__init__': <function People.__init__ at 0x00000000021DF7B8>, 'people_info': <function People.people_info at 0x00000000021DF840>, '__dict__': <attribute '__dict__' of 'People' objects>, '__weakref__': <attribute '__weakref__' of 'People' objects>, '__doc__': None}
```

### getattr()函数

```
描述:
	getattr()函数用于返回一个对象属性值

语法:
	getattr(object, name, default)

参数:
	object--对象
	name--字符串, 对象属性
	default--默认返回值,如果不提供该参数,在没有对于属性时,将触发AttributeError.

返回值:
	返回对象属性值
```

```
class People:
    country = 'China'

    def __init__(self, name):
        self.name = name

    def people_info(self):
        print('%s is xxx'% self.name)


obj =getattr(People, 'country')
print(obj)
>>>China
obj =getattr(People, 'countryaaaaaa')
print(obj)
>>>Traceback (most recent call last):
     File "F:/ch07-25/Demo02·19.07.25.py", line 83, in <module>
       obj =getattr(People, 'countryaaaaaa')
   AttributeError: type object 'People' has no attribute 'countryaaaaaa'
obj = getattr(People, 'countryaaaaaa', None)
print(obj)
>>>None
```

### setattr()函数

```
描述:
	setattr函数,用于设置属性值,该属性必须存在

语法:
	setattr(object, name, value)

参数:
	object--对象
	name--字符串, 对象属性
	value--属性值
	
返回值:
	无
```

```
class People:
    country = 'China'

    def __init__(self, name):
        self.name = name

    def people_info(self):
        print('%s is xxx'% self.name)


obj = People('aaa')

setattr(People, 'x', 111)  # 等同于People.x = 111
print(People.x)
>>>111
# obj.age = 18
setattr(obj, 'age', 18)
print(obj.__dict__)
>>>{'name': 'aaa', 'age': 18}
print(People.__dict__)
>>>{'__module__': '__main__', 'country': 'China', '__init__': <function People.__init__ at 0x0000000001EAF7B8>, 'people_info': <function People.people_info at 0x0000000001EAF840>, '__dict__': <attribute '__dict__' of 'People' objects>, '__weakref__': <attribute '__weakref__' of 'People' objects>, '__doc__': None, 'x': 111}
```

### delattr()函数

```
描述:
	setattr函数用于删除属性
	delarrt(x, 'foobar')相当于del x.foobar

语法:
	delattr(object, name)

参数:
	object--对象
	name--必须是对象的属性
	
返回值:
	无
```

```
class People:
    country = 'China'

    def __init__(self, name):
        self.name = name

    def people_info(self):
        print('%s is xxx'% self.name)


delattr(People, 'country')  # 等同于del People.country
print(People.__dict__)
>>>{'__module__': '__main__', '__init__': <function People.__init__ at 0x0000000001E8F7B8>, 'people_info': <function People.people_info at 0x0000000001E8F840>, '__dict__': <attribute '__dict__' of 'People' objects>, '__weakref__': <attribute '__weakref__' of 'People' objects>, '__doc__': None}
```