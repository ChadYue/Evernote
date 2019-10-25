# 魔法方法

在Python中，所有以双下划线包起来的方法，都统称为"魔术方法"。比如我们接触最多的init_ _。魔法方
法帮助我们定义更加符合Python风格的对象。

### 构造和初始化

__ new __ 是在实例创建之前被调用的，因为它的任务就是创建实例然后返回该实例，是个静态方法。

__ init __ 是当实例对象创建完成后被调用的，然后设置对象属性的一些初始值。

故而“本质上”来说，__ new __ () 方法负责创建实例，而 __ init __ 0仅仅是负责实例属性相关的初始化而已，执行顺序是，先new后init。

```
class Student(object):
    def __new__(cls, *args, **kwargs):
        print('我是new函数!')  # 这是为了追踪new的执行过程
        print(type(cls))      # 这是为了追踪new的执行过程
        return object.__new__(cls)

    def __init__(self, name, age):
        self.name = name
        self.age = age
        print('我是init')

    def study(self):
        print('我爱学习')


if __name__ == '__main__':
    s = Student('张三', 25)
    print(s.name)
    print(s.age)
    s.study()
```

运行结果为:

```
我是new函数!
<class 'type'>
我是init
张三
25
我爱学习
```

### 属性访问控制

通常情况下，我们在访问类或者实例对象的时候，会牵扯到一些属性访问的魔法方法，主要包括:

①**getattr** (self, name):访问不存在的属性时调用

②**getattribute**(self, name):访问存在的属性时调用(先调用该方法，查看是否存在该属性,若不存在,接着去调用①)

③**setattr** (self, name, value):设置实例对象的一个新的属性时调用

④**delattr** (self, name):删除一个实例对象的 属性时调用一个例子

```
class Foo:
    x = 1
    def __init__(self, y):
        self.y = y

    def __getattr__(self, item):
        print('-----> from grtattr : 你找到属性不存在')

    def __setattr__(self, key, value):
        print('-----> from setattr')
        # self.key = value  # 无限递归
        self.__dict__[key] = value

    def __delattr__(self, item):
        print('-----> from delattr')
        # del self.item  # 无限递归
        self.__dict__.pop(item)

    def __getattribute__(self, item):
        print('-----> __getattribute__')
        return super().__getattribute__(item)


f1 = Foo(10)
print(f1.__dict__)
f1.z = 3
print(f1.__dict__)

f1.__dict__['a'] = 3
del f1.a
print(f1.__dict__)

f1.xxxxxx
```

输出

```
-----> from setattr
-----> __getattribute__
-----> __getattribute__
{'y': 10}
-----> from setattr
-----> __getattribute__
-----> __getattribute__
{'y': 10, 'z': 3}
-----> __getattribute__
-----> from delattr
-----> __getattribute__
-----> __getattribute__
{'y': 10, 'z': 3}
-----> __getattribute__
-----> from grtattr : 你找到属性不存在
```

注意,调用

```
self.__ dict __[key] = value
```

会触发

```
def __getattribute__(self, item):
    print('-----> __getattribute__')
    return super().__getattribute__(item)
```

因为虽然是要给字典self.__ dict __ 添加键值对， 其中隐含着首先获得self. __ dict  __ 。 另外 __ getattribute __ 需 要返回super(). __ getattribute __(item) ，否则函数默认返回None,报错。

### 上下文管理

with这个关键字，我们已经很熟悉了。

操作文本对象的时候，我们要用with open，这就是一个上下文管理的例子。

```
with open('test,txt') as f:
	print f.readlines()
```

### 什么是上下文管理器

基本语法

```
with EXPR as VAR:
	BLOCK
```

先理清几个概念

```
1.上下文表达式:with open('test.txt') as f:
2.上下文管理器:open('test.txt')
3.f不是上下文管理器,应该是资源对象
```

**如何写上下文管理器?**

要自己实现这样一个上下文管理，要先知道上下文管理协议。

简单点说，就是在一个类里，如果实现了_ enter_ 和_ exit_ 方法， 这个类的实例就是一个上下文管理器。

例如这个示例:

```
class Resource():
    def __enter__(self):
        print('===connect to resource===')
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        print('===close resource connection===')

    def operate(self):
        print('===in operation===')


with Resource() as res:
    res.operate()
>>>===connect to resource===
>>>===in operation===
>>>===close resource connection===
```

从这个示例可以很明显的看出，在编写代码时，可以将资源的连接或者获取放在__ enter __ 中， 而将资源的关闭写在 __ exit __ 中。 __ enter __ 中需要返回当前实例对象。

**为什么要用上下文管理器?**

和Python崇尚的优雅风格有关。

1. 可以以一种更加优雅的方式，操作(创建/获取/释放)资源，如文件操作、数据库连接
2. 可以以一种更加优雅的方式，处理异常

处理异常，通常都是使用try...execept... 来捕获处理的。这样做一个不好的地方是，在代码的主逻辑里，会有大量的异常处理代理，这会很大的影响我们的可读性。

好一点的做法呢，可以使用with 将异常的处理隐藏起来。

仍然是以上面的代码为例，我们将1/0 这个一定会批出异常的代码写在operate里

```
class Resource():
    def __enter__(self):
        print('===connect to resource===')
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        print('===close resource connection===')
        print(exc_type)
        print(exc_val)
        print(exc_tb)
        return True

    def operate(self):
        1/0

with Resource() as res:
    res.operate()
```

运行一下，惊奇地发现，居然不会报错。

这就是上下文管理协议的一个强大之处，异常可以在_ _exit_ 进行捕获并由你自己决定如何处理，是抛出呢还是在这里就解决了。在_ . exit__里返回 True (没有return就默认为return False)，就相当于告诉Python解释器， 这个异常我们已经捕获了，不需要再往外抛了。

在写_ exit_ _ 函数时，需要注意的事，它必须要有这三个参数:

- exc. type:异常类型
- exe _val: 异常值
- exc_ tb:异常的错误栈信息

当主逻辑代码没有报异常时，这三个参数将都为None。

**理解并使用contextib**

在上面的例子中，我们只是为了构建一个上下文管理器，却写了一个类。如果只是要实现一个简单的功能，写一个类未免有点过于繁杂。这时候，我们就想，如果只写一个函数就可以实现上下文管理器就好了。

这个点Python早就想到了。它给我们提供了一个装饰器，你只要按照它的代码协议来实现函数内容，就可以将这个函数对象变成一个上下文管理器。

我们按照contextlib的协议来自己实现一个打开文件(with open)的上下文管理器。

```
import contextlib

@contextlib.contextmanager
def open_func(file_name):
    # __enter__方法
    print('open file:', file_name, 'in__enter__')
    file_handler = open(file_name, 'r')

    yield file_handler

    print(('close file:', file_name, 'in__exit__'))
    file_handler.close()
    return

with open_func('a.txt') as file_in:
    for line in file_in:
        print(line)
```

在被装饰函数里，必须是一个生成器(带有yield) ，而yield之前的代码， 就相当于__ enter __ 里的内容。yield之后的代码，就相当于__ exit __ 里的内容。

上面这段代码只能实现上下文管理器的第一 个目的(管理资源)，并不能实现第二个目的(处理异常)。果要处理异常，可以改成下面这个样子。

```
import contextlib

@contextlib.contextmanager
def open_func(file_name):
    # __enter__方法
    print('open file:', file_name, 'in__enter__')
    file_handler = open(file_name, 'r')

    try:
        yield file_handler
    except Exception as exc:
        print('the exception was thrown')
    finally:
        print(('close file:', file_name, 'in__exit__'))
        file_handler.close()
        return


with open_func('a.txt') as file_in:
    for line in file_in:
        1/0
        print(line)
```

总结起来，使用上下文管理器有三个好处:

1. 提高代码的复用率:
2. 提高代码的优雅度:
3. 提高代码的可读性:参考https://juejin.im/post/5c87b165f265da2dac4589cc

### str和repr方法

很多时候我们自己编写一个类，在将它的实例在终端上打印或查看的时候，我们往往会看到-一个不太满意的结果。

```
class Car:
    def __init__(self, color, mileage):
        self.color = color
        self.mileage = mileage


my_car = Car('red', 37281)
print(my_car)
>>><__main__.Car object at 0x000000000220D588>
```

类默认转化的字符串基本没有我们想要的一些东西，仅仅包含了类的名称以及实例的ID (理解为Python对象的内存地址即可)。

所以，我们可能会手动打印对象的一些属性或者是在类里自己实现一一个方法来返回我们需要的信息。

**使用__ str __ 实现类到字符串的转化**

不用自己另外定义一个方法，你可以在类里实现__ str __ 和 __ repr __ 方法， 从而自定义类的字符串描述，这两种都是比较Pythonic的方式去控制对象转化为字符串的方式。

下面我们通过做实验慢慢的来看这两种方式是怎么工作的。首先,我们先加一个__ str __ 方法到前 面的类中看看情况。

```
class Car(object):
    def __init__(self, color, mileage):
        self.color = color
        self.mileage = mileage

    def __str__(self):
        return f'a {self.color} car'
```

当你重新打印和查看这个类的实例的时候,你会看到一个稍微不同的结果

```
my_car = Car('red', 37281)
print(my_car)
>>>a red car
```

查看mycar的时候的输出仍然和之前一样，不过打印mycar的时院返回的内容和新加的__ str __  方法的返回一致。类的'__str'方法会在某些需 要将对象转为字符串的时候被调用。比如下面这些情况

```
my_car = Car('red', 37281)
print(my_car)
print(str(my_car))
print('{}'.format(my_car))
>>>a red car
>>>a red car
>>>a red car
```

有了**str**这个方法，你就不用手动去打印对象的一些信息或者添加额外的方法去达到目的。类到字符串的转化使用str 这种Pythonic的方式实现即可。

**使用__ repr __ 实现类到字符串的转化**

上面我们查看my_car对象的时候，输出的仍是类似这样比较奇怪的结果。这是因为Python3中一共有2中方式控制类到字符串的转化，第一种就是我们前面提到的str方法，另一个就是repr方法。后者的工作方式与前者类似，但是它被调用的时机不同。

这里有个简单的例子，同样是在之前的类上作改动

```
class Car(object):
    def __init__(self, color, mileage):
        self.color = color
        self.mileage = mileage

    def __str__(self):
        return '__str__ for car'
    
    def __str__(self):
        return '__repr__ for car'
```

我们通过下面的操作来感觉下什么时候调用**str**，什么时候调用的**repr**。

```
my_car = Car('red', 37281)
print(my_car)
print('{}'.format(my_car))
>>>__str__ for car
>>>__str__ for car
```

从上面可以看出，当我们查看对象的时候(上面的最后一个操作)调用的是**repr**方法。

另外，列表以及宇典等容器总是会使用**repr**方法。即使你显式的调用str方法，也是如此。

```
print(str([my_car]))
>>>[__repr__ for car]
```

如果我们需要显示的指定以何种方式进行类到字符串的转化，我们可以使用内置的str()或repr()方法，它们会调用类中对应的双下划线方法。(当然， 上面的情况除外)

```
print(str(my_car))
>>>__str__ for car
print(repr(my_car))
>>>__repr__ for car
```

str和repr的差别现在你可能在想，__ str __ 和 __ repr __ 的差别究竟在哪里， 它们的功能都是实现类到字符串的转化，它们的特定并没有体现出用途上的差异。

带着这个这个问题，我们试着去Python的标准库中找找答案。我们就来看看datetime.date 这个类是怎么在使用这两个方法的。

```
import datetime
today = datetime.date.today()
print(today)
>>>2019-07-29
print(str(today))
>>>2019-07-29
print(repr(today))
>>>datetime.date(2019, 7, 29)
```

因此，我们有个初步的答案。
__ str __ 的返回结果可读性强。也就是说，__ str __ 的意义 是得到便于人们阅读的信息，就像上面的2019-07-29'一样。
__ repr __ 的返回结果应更准确。怎么说， __ repr __ 存在的目的在于调试， 便于开发者使用。细心的读者会发现将 __ repr __ 返回的方式直接复制到命令行上, 是可以直接执行的。

但是于个人来说，如果按照通常的原则去编写代码会做很多额外的工作，两个方法的返回结果只需要对开发
者友好就可以了，并不一定需要存储某个对象的完整状态。

**每个类都最好有一一个repr方法**

如果你没有添加str方法，Python 在需要该方法但找不到的时候，它会去调用repr方法。因此，推荐在写自己的类的时候至少添加一个repr方法，这能保证类到字符串始终有一个有效的自定义转换方式。

我们为Car类添加一个repr方法

```
class Car(object):
    def __init__(self, color, mileage):
        self.color = color
        self.mileage = mileage

    def __repr__(self):
        return (f'{self.__class__.__name__}({self.color!r}, {self.mileage!r})')

    def __str__(self):
        return 'a {self.color} car'
```

注意，我们这里用了!r标记，是为了保证self.color与self.mileage在转化为字符串的时候使用repr(self.color)和repr(self.mileage),而不是str(self.color)和str(self. mileage)。

实现了__ repr __ 方法后，当我们查看类的实例或者直接调用repr()方法，就能得到一个比较满意的结果
了。

打印或直接调用str()方法也能得到相同的结果。

```
my_car = Car('red', 37281)
print(my_car)
print(str(my_car))
print(repr(my_car))
>>>a red car
>>>a red car
>>>Car('red', 37281)
```

**小结**

我们可以使用__ str __ 和 __ repr __ 方法定义 类到字符串的转化方式，而不需要手动打印某些属性或是添加額外的方法。一般来说，__ str __ 的返回结果在于强可读性， 而__ repr __ 的返回结果在于准确性。我们至少需要添加一个__ repr__ 方法 来保证类到字符串的自定义转化的有效性，__ str __ 是 可选的。因为默认情况下，在需要却找不到__ str __ 方法的时候，会自动调用__ repr __ 方法。

参考: https://blog.csdn.net/z_feng12489/article/detail/89708907

### 魔法方法之__ call __

在Python中，函数其实是一个对象:

```
f = abs
print(f.__name__)
print(f(-123))
>>>abs
>>>123
```

由于f可以被调用，所以，f被称为可调用对象。

所有的函数都是可调用对象。

一个类实例也可以变成一个可谓用对象，只需要实现一个特殊方法__ call __ .()。

我们把Person类变成一一个可调用对象:

```
class Person(object):
    def __init__(self, name, gender):
        self.name = name
        self.gender = gender

    def __call__(self, friend):
        print('My name is %s ...'% self.name)
        print('My friend is %s ...'% friend)
```

现在可以对Person实例直接调用:

```
p = Person('Bob', 'male')
p('Tim')
>>>My name is Bob ...
>>>My friend is Tim ...
```

单看p('Tim')你无法确定p是一个函数还是一个类实例， 所以，在Python中，函数也是对象，对象和函数的区别并不显著。

可以把实例对象用类似函数的形式表示，进一步模糊了函数和对象之间的概念

```
class Fib(object):
    def __init__(self):
        pass

    def __call__(self, num):
        a,b = 0,1
        self.l = []

        for i in range(num):
            self.l.append(a)
            a, b = b, a+b
        return self.l

    def __str__(self):
        return str(self.l)


f = Fib()
print(f(10))
>>>[0, 1, 1, 2, 3, 5, 8, 13, 21, 34]
```

