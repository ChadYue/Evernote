# 闭包和装饰器

### 闭包

Python中函数也是对象，允许把函数本身作为参数传入另一个函数，还可以把函数作为结果值返回在函数内部再定义一个函数，并且内部函数用到了外部数作用域里的变量(enclosing) ，那么将**这个内部函数以及用到的外部函数内的变量**一起称为闭包(Closure) :

```
def line(a, b):
    def get_y_axis(x):
        return a * x + b  # 内部函数使用了外部函数的变量a和b
    return get_y_axis     # 返回值是闭包函数名,注意不是函数调用没有小括号


L1 = line(1, 1)  # 创建一条直线: y = x + 1
print(L1)
>>><function line.<locals>.get_y_axis at 0x000000000271F7B8>
print(L1(3))     # 获取第一条直线中,横坐标为3时,纵坐标的值
>>>4
L2 = line(2, 3)  # 创建一条直线: y = 2x + 3
print(L2)
>>><function line.<locals>.get_y_axis at 0x000000000271F840>
print(L2(3))     # 获取第一条直线中,横坐标为3时,纵坐标的值
>>>9
L3 = line(2, 3)  # 创建一条直线: y = 2x + 3
print(L3)
>>><function line.<locals>.get_y_axis at 0x000000000271F8C8>
print(L2 == L3)
>>>False
print(L2 is L3)
>>>False
```

### 装饰器

装饰器(decorator)接受一 个callable对象( 可以是函数或者实现了**call**方法的类)作为参数，并返回一个callable对象

它经常用于有切面需求的场景，比如:插入日志、性能测试(函数执行时间统计)、事务处理、缓存、权限校验等场景。装饰器是解决这类问题的绝佳设计，有了装饰器，我们就可以抽离出大量与函数功能本身无关的雷同代码并继续重用。

举个实例，假设你写好了100个Flask中的路由函数，现在要在访问这些路由函数前，先判断用户是否有权限，你不可能去这100个路由函数中都添加一遍权限判断的代码(如果权限判断代码为5行，你得加500行)。那么，你可能想把权限认证的代码抽离为一个函数，然后去那100个路由函数中调用这个权限认证函数，这样只要加100行。但是，根据开放封闭原则，对于已经实现的功能代码建议不能修改，但可以扩展，因为可能你在这些路由函数中直接添加代码会导致原函数出现问题，那么最佳实践是使用装饰器

#### 被装饰的函数无参数

如果原来是调用f1()、f2()...，我们只要让用户还是调用f1()、f2()...，即他们调用的函数名还是保持不变，但实际执行的函数体代码已经变了(Python中函数也是对象， 函数名只是变量，可能改变它引用的函数体对象) :

没有使用装饰器之前:

```
def f1():
    print('function f1...')


def f2():
    print('function f2...')


f1()
>>>function f1...
f2()
>>>function f2...
```

创建装饰器，接收函数参数，返回一个闭包函数inner:

```
def login_required(func):
    def inner():  # inner是个闭包,它使用了外部函数的变量func,即传入的原函数引用f1、f2...
        if func.__name__ == 'f1':  # 这里是权限验证的逻辑判断,此处简化为只能调用f1
            print(func.__name__, '权限验证成功')
            func()  # 执行原函数,相当于f1()或f2()...
        else:
            print(func.__name__, '权限验证失败')
    return inner


def f1():
    print('function f1...')


def f2():
    print('function f2...')


new_f1 = login_required(f1)  # 将f1传入装饰器,返回inner引用,并赋值给新的变量new_f1
new_f1()  # 执行函数,即执行inner(),这个闭包中使用的func变量指向原f1函数体
>>>f1 权限验证成功
>>>function f1...
new_f2 = login_required(f2)  # 将f2传入装饰器,返回inner引用,并赋值给新的变量new_f2
new_f2()  # 执行函数,即执行inner(),func变量指向原f2,所有它不会通过权限验证,即不会执行func()
>>>f2 权限验证失败
```

上面使用装饰器有个问题,就是用户原来是调用f1()、f2()...，现在你让他们调用new_f1()、new_f2()...，这样肯定不行，所有需要修改如下：

```
f1 = login_required(f1)  # 将f1传入装饰器,此时func指向了原f1函数体.返回inner引用,并赋值给f1
f1()  # 执行函数,即执行inner(),这个闭包中使用的func变量指向原f1函数体
```

上述两个步骤可以用@Python语法糖简写为:

```
def login_required(func):
    def inner():  # inner是个闭包,它使用了外部函数的变量func,即传入的原函数引用f1、f2...
        if func.__name__ == 'f1':  # 这里是权限验证的逻辑判断,此处简化为只能调用f1
            print(func.__name__, '权限验证成功')
            func()  # 执行原函数,相当于f1()或f2()...
        else:
            print(func.__name__, '权限验证失败')
    return inner


# 1. 定义时
@login_required
def f1():
    print('function f1...')


# 调用时
f1()
>>>f1 权限验证成功
>>>function f1...
```

#### 被装饰的函数有参数

```
def login_required(func):
    def inner():  # inner是个闭包,它使用了外部函数的变量func,即传入的原函数引用f1、f2...
        if func.__name__ == 'f1':  # 这里是权限验证的逻辑判断,此处简化为只能调用f1
            print(func.__name__, '权限验证成功')
            func()  # 执行原函数,相当于f1()或f2()...
        else:
            print(func.__name__, '权限验证失败')
    return inner


# 1. 定义时
@login_required
def f1(a):
    print('function f1，args: a=', a)


# 调用时
f1(10)
```

如果被装饰的函数有参数，调用f1(10) 此时实际调用的是inner(10) ，而装饰器中的闭包inner没有定义参数，所以会报错: 

```
Traceback (most recent call last):
  File "F:/ch07-25/Demo03·19.07.25.py", line 42, in <module>
    f1(10)
TypeError: inner() takes 0 positional arguments but 1 was given
```

那么如果我给inner定义一个形参呢?

```
f1 权限验证成功
Traceback (most recent call last):
  File "F:/ch07-25/Demo03·19.07.25.py", line 42, in <module>
    f1(10)
  File "F:/ch07-25/Demo03·19.07.25.py", line 29, in inner
    func()  # 执行原函数,相当于f1()或f2()...
TypeError: f1() missing 1 required positional argument: 'a'
```

所有正确的做法是:

```
def login_required(func):
    def inner(a):  # inner是个闭包,它使用了外部函数的变量func,即传入的原函数引用f1、f2...
        if func.__name__ == 'f1':  # 这里是权限验证的逻辑判断,此处简化为只能调用f1
            print(func.__name__, '权限验证成功')
            func(a)  # 执行原函数,相当于f1()或f2()...
        else:
            print(func.__name__, '权限验证失败')
    return inner


# 1. 定义时
@login_required
def f1(a):
    print('function f1，args: a=', a)


# 调用时
f1(10)
>>>f1 权限验证成功
>>>function f1，args: a= 10
```

现在的装饰器可以正确装饰f1(a)函数，但是假如有一一个f2(a, b, c)有三个参数呢， 肯定报错，所以还要修改装饰器，使用Python中的 *args 和**kwargs 来匹配任意长度的位置参数或关键字参数:

```
def login_required(func):
    def inner(*args, **kwargs):  # inner是个闭包,它使用了外部函数的变量func,即传入的原函数引用f1、f2...
        if func.__name__ == 'f1':  # 这里是权限验证的逻辑判断,此处简化为只能调用f1
            print(func.__name__, '权限验证成功')
            func(*args, **kwargs)  # 执行原函数,相当于f1()或f2()...
        else:
            print(func.__name__, '权限验证失败')
    return inner
```

#### 被装饰的函数有fan

如果使用2.2的装饰器,修改f1()函数定义,它里面有return返回值,将会有问题:

```
def login_required(func):
    def inner(*args, **kwargs):
        if func.__name__ == 'f1':
            print(func.__name__, '权限验证成功')
            func(*args, **kwargs)
        else:
            print(func.__name__, '权限验证失败')
    return inner


@login_required
def f1(a, b, c):
    print('function f1，args: a={}, b={}, c={}'.format(a, b, c))
    return 'hello, world'


res = f1(10, 20, 30)
print(res)

# 输出结果中返回的是None, 而不是hello, world
>>>f1 权限验证成功
>>>function f1，args: a=10, b=20, c=30
>>>None
```

原因是调用f1(10, 20, 30),实际是调用inner(10, 20, 30),然后执行inner闭包的函数体，在执行到func(*args, **kwargs) 后，没有接收原f1函数体的返回值。当inner闭包执行完毕，Python解释器也没有发现有return语句，就默认返回None

在inner中接收func函数的返回值，然后return返回它， 本示例中装饰器的inner执行完func(*args,** kwargs)后没有其它代码了，所以可以直接修改为return func( *args,  ** kwargs) ，如果还有其它逻辑，则用变量保存func的返回值res=func( *args, **kwargs)，inner最后一行返回 return res

```
def login_required(func):
    def inner(*args, **kwargs):
        if func.__name__ == 'f1':
            print(func.__name__, '权限验证成功')
            return func(*args, **kwargs)
        else:
            print(func.__name__, '权限验证失败')
    return inner


@login_required
def f1(a, b, c):
    print('function f1，args: a={}, b={}, c={}'.format(a, b, c))
    return 'hello, world'


res = f1(10, 20, 30)
print(res)
# 输出结果
>>>f1 权限验证成功
>>>function f1，args: a=10, b=20, c=30
>>>hello, world
```

#### 装饰器带参数

像Flask的@route( /index')就是带参数的，其实route只是一个函数， 它返回真正的装饰器，即在原来的装饰器外面再加一层函数:

```
def logging(level):
    def decorator(func):
        def wrapper(*args, **kwargs):
            print('[日志级别{}]:被修饰的函数名是{}'.format(level, func.__name__))
            return func(*args, **kwargs)
        return wrapper
    return decorator


@logging('DEBUG')  # 等价于 f1 = logging('DEBUG')(f1),即先执行logging('DEBUG'),返回decorator引用
def f1(a, b, c):
    print('function f1, args: a={}, b={}, c={}'.format(a, b, c))
    return 'hello, world'


@logging('INFO')
def f2():
    print('function f2...')


res = f1(10, 20, 30)
print(res)
>>>[日志级别DEBUG]:被修饰的函数名是f1
>>>function f1, args: a=10, b=20, c=30
>>>hello, world
f2()
>>>[日志级别INFO]:被修饰的函数名是f2
>>>function f2...
```

#### 使用@wraps

```
def logging(level):
    def decorator(func):
        def wrapper(*args, **kwargs):
            """print log before a function."""
            print('[日志级别{}]:被修饰的函数名是{}'.format(level, func.__name__))
            return func(*args, **kwargs)
        return wrapper
    return decorator


@logging('DEBUG')
def f1(a, b, c):
    """This is f1 function"""
    print('function f1, args: a={}, b={}, c={}'.format(a, b, c))
    return 'hello, world'


res = f1(10, 20, 30)
print(res)

print('错误的函数签名:', f1.__name__)
print('错误的函数文档:', f1.__doc__)
# 输出结果
>>>[日志级别DEBUG]:被修饰的函数名是f1
>>>function f1, args: a=10, b=20, c=30
>>>hello, world
>>>错误的函数签名: wrapper
>>>错误的函数文档: print log before a function.
```

原因是调用f1(10, 20, 30),实际是调用装饰器中的wrapper(),所以打印出来的函数签名和文档都是wrapper的，可以使用functools 模块的wraps装饰器解决这个问题:

```
from functools import wraps


def logging(level):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            """print log before a function."""
            print('[日志级别{}]:被修饰的函数名是{}'.format(level, func.__name__))
            return func(*args, **kwargs)
        return wrapper
    return decorator


@logging('DEBUG')
def f1(a, b, c):
    """This is f1 function"""
    print('function f1, args: a={}, b={}, c={}'.format(a, b, c))
    return 'hello, world'


res = f1(10, 20, 30)
print(res)

print('错误的函数签名:', f1.__name__)
print('错误的函数文档:', f1.__doc__)
# 输出结果:
>>>[日志级别DEBUG]:被修饰的函数名是f1
>>>function f1, args: a=10, b=20, c=30
>>>hello, world
>>>错误的函数签名: f1
>>>错误的函数文档: This is f1 function
```
### 装饰器实例

更多实例请参考: http://python3-cookbook.readthedocs.io/zh_CN/latest/chapters/po9_meta_programming.html

#### 函数执行时间统计

```
from functools import wraps
import time

def timethis(func):
    """
    Decorator that reports the execution time.
    """
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(func.__name__, end-start)
        return result
    return wrapper

@timethis
def countdown(n):
    """Counts down"""
    while n > 0:
        n -= 1
    return 'done'

res = countdown(100000)
print(res)
# 输出结果:
>>>countdown 0.005000114440917969
>>>done
```

```
@timethis
def countdown(n):
	pass
等价于:
def countdown(n):
	pass
countdown = timethis(countdown)
```

内置的装饰器比如@staticmethod、@classmethod、@property原理也是一样的，下面两个代码片段是等价的:

```
class A:
    @classmethod
    def method(cls):
        pass


class B:
    # Equivalent definition of a class method
    def method(cls):
        pass
    method = classmethod(method)
```

#### 插入日志

```
from functools import wraps
import logging


def logged(level, name=None, message=None):
    """

    Add logging to a function. level is the logging
    level, name is the logger name, and message is the
    log message. If name and message aren't specified,
    they default to the function's module and name.
    """
    def decorate(func):
        logging.basicConfig(level=logging.DEBUG, format='%(asctime)s - %(filename)s[line:%(lineno)s] - %(levelname)s - %(message)s')
        logname = name if name else func.__module__
        log = logging.getLogger(logname)
        logmsg = message if message else func.__name__

        @wraps(func)
        def wrapper(*args, **kwargs):
            log.log(level, logmsg)
            return func(*args, **kwargs)
        return wrapper
    return decorate

# Example use
@logged(logging.DEBUG)
def add(x, y):
    return x + y


@logged(logging.CRITICAL, 'example')
def spam():
    print('Spam!')


print(add(3, 5))
spam()
# 输出结果;
>>>2019-07-26 09:48:33,204 - Demo03·19.07.25.py[line:144] - DEBUG - add
>>>8
>>>2019-07-26 09:48:33,204 - Demo03·19.07.25.py[line:144] - CRITICAL - spam
>>>Spam!
```

