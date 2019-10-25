# 迭代器和生成器

Python中内置的序列，如list、 tuple、 str、 bytes、 dict、 set、collections.deque等都是 可迭代对象，但它们不是选代器。迭代器可以被next()函数调用，并不断返回下一个值。Python从 可迭代的对象中获取迭代器。迭代器和生成器都是为了惰性求值( lazy evaluation)，避免浪费内存空间，实现高效处理大量数据。在Python3中，生成器有广泛的用途，所有生成器都是迭代器，因为生成器完全实现了选代器接口。迭代器用于从集合中取出元素，而生成器用于"凭空"生成元素。PEP 342给生成器增加了send0方法，实现了"基于生成器的协程"。PEP 380允许生成器中可以return返回值，并新增了yield from语法结构，打开了调用方和子生成器的双向通道。

## 可迭代的对象

**可迭代的对象(Iterable)是指使用iter()内置函数可以获取迭代器(Iterator) 的对象**。Python解释器需要迭代对象x时，会自动调用iter(x) ，内置的iter()函数有以下作用:

1. 检查对象x是否实现了_ iter_ () 方法，如果实现了该方法就调用它，并尝试获取一个迭代器
2. 如果没有实现_ iter _ () 方法，但是实现了_ getitem _ (index) 方法，尝试按顺序(从索引o开始)获取元素，即参数index是从o开始的整数(int) 。之所以会检查是否实现__ getitem(index)__ 方法，为了向后兼容
3. 如果前面都尝试失败，Python会抛出TypeError 异常，通常会提示'X' object is not iterable (X类型的对象不可迭代)，其中X是目标对象所属的类

具体来说，哪些是可迭代对象呢?

- 如果对象实现了能返回迭代器的__ iter __()方法，那么对象就是可迭代的
- 如果对象实现了__ getitem __ (index) 方法，而且index参数是从o开始的整数(索引)，这种对象也可以迭代的。Python中内置的序列类型，如list、 tuple、 str、 bytes、 dict、 set、 collections deque等都可以迭代，原因是它们都实现了getitem () 方法(**注意:**其实标准的序列还都实现了 __ iter __ ()方法)

### 判断对象是否可迭代

从Python 3.4开始，检查对象x能否迭代，最准确的方法是:调用iter(x) 函数，如果不可迭代，会抛出TypeError异常。这比使用isinstance(x, abc.Iterable) 更准确，因为iter(x) 函数会考虑到遗留的__ getitem __(index) 方法，而abc. Iterable类则不会考虑

### __ getitem __()

下面构造一个类，它实现了__ getitem __() 方法。可以给类的构造方法传入包含一些文本的字符串，然后可以逐个单词进行迭代:

```
import re
import reprlib
from collections import abc

RE_WORD = re.compile('\w+')


class Sentance:
    def __init__(self, text):
        self.text = text
        self.words = RE_WORD.findall(text)

    def __getitem__(self, index):
        return self.words[index]

    def __len__(self):
        return len(self.words)

    def __repr__(self):
        return "Sentence({})".format(reprlib.repr(self. text))
```

测试Sentence实例能否迭代:

```
s = Sentance('I love Python')
print(s)
>>>Sentence('I love Python')
print(s[0])
>>>I
print(s.__getitem__(0))
>>>I
for word in s:
    print(word)
>>>I
>>>love
>>>Python
print(list(s))
>>>['I', 'love', 'Python']
print(isinstance(s, abc.Iterable))
>>>False
print(iter(s))
>>><iterator object at 0x00000000021A89E8>
```

### __ iter __()

如果实现了__ iter __()方法,但该方法没有返回迭代器时:

```
class Foo:
    def __iter__(self):
        pass


from collections import abc

f = Foo()

print(isinstance(f, abc.Iterable))
>>>True
print(iter(f))
>>>Traceback (most recent call last):
  		File "F:/python实训-岳才智/19-07/19-07-第四周/ch07-29/Demo01·19.07.29.py", line 50, in <module>
   print(iter(f))TypeError: iter() returned non-iterator of type 'NoneType'
```

**Python迭代协议要求iterO必须返回特殊的迭代器对象。**下一节会讲迭代器，迭代器对象必须实现__ next __() 方法，并使用StopIteration 异常来通知迭代结束

```
class Foo:
    def __iter__(self):
        return iter([1, 2, 3])


from collections import abc

f = Foo()

print(isinstance(f, abc.Iterable))
>>>True
print(iter(f))
>>><list_iterator object at 0x00000000026D7BA8>
for i in f:
    print(i)
>>>1
>>>2
>>>3
```

## 迭代器

迭代是数据处理的基石。当扫描内存中放不下的数据集时，我们要找到一种惰性获取数据项的方式，即按需一次获取一个数据项。这就是迭代器模式(Iterator pattern)

迭代器是这样的对象:实现了无参数的_ next__ () 方法，返回序列中的下一个元素，如果没有元素了，就抛出StopIteration 异常。**即，迭代器可以被next(函数调用，并不断返回下一个值。**

在Python语言内部，迭代器用于支持:

- for循环
- 构建和扩展集合类型
- 逐行遍历文本文件
- 列表推导、字典推导和集合推导
- 元组拆包
- 调用函数时，使用*拆包实参

### 判断对象是否为迭代器

检查对象x是否为迭代器最好的方式是调用isinstance(x, abc. Iterator) :

```
from collections import abc
print(isinstance([1, 3, 5], abc.Iterator))
>>>False
print(isinstance((2, 4, 6), abc.Iterator))
>>>False
print(isinstance({'name': 'wangy', 'age': 18}, abc.Iterator))
>>>False
print(isinstance({1, 3, 5}, abc.Iterator))
>>>False
print(isinstance('abc', abc.Iterator))
>>>False
print(isinstance(100, abc.Iterator))
>>>False
print(isinstance((x*2 for x in range(5)), abc.Iterator))
>>>True
```

**Python中内置的序列类型，如list. tuple、str、 bytes、dict、 set、 collections.deque等 都是可迭代的对象，但不是选代器;生成器定是迭代器**

### __ next __ ()和 __ iter__ ()

标准的迭代器接口:

- __ next __ () : 返回下一个可用的元素，如果没有元素了，抛出StopIteration异常 。调用next(x)相当于调用x.__ next __ ()

- __ iter__ () : 返回迭代器本身(self)，以便在应该使用可迭代的对象的地方能够使用迭代器，比如在for循环list(iterable)函数、sum(iterable, start=0, /)函数等应该使用可迭代的对象地方可以使用迭代器。**说明**:如章节1所述，只要实现了能返回迭代器的__ iter__ () 方法的对象就是可迭代的对象，所以，**迭代器都是可迭代的对象!**

下面的示例中，Sentence 类的对象是可迭代的对象，而SentenceIterator 类实现了典型的迭代器设计模式:

```
import re
import reprlib

RE_WORD = re.compile('\w+')


class Sentance:
    def __init__(self, text):
        self.text = text
        self.words = RE_WORD.findall(text)

    def __repr__(self):
        return "Sentence({})".format(reprlib.repr(self. text))

    def __iter__(self):
        return SentanceIteratot(self.words)


class SentanceIteratot:
    def __init__(self, words):
        self.words = words
        self.index = 0

    def __next__(self):
        try:
            word = self.words[self.index]
        except IndexError:
            raise StopIteration()
        self.index += 1
        return word

    def __iter__(self):
        return self
s = Sentance('pig and pepper')
it = s.__iter__()
print(s)
>>>Sentence('pig and pepper')
print(it)
>>><__main__.SentanceIteratot object at 0x0000000002881E48>
print(next(it))
>>>pig
print(next(it))
>>>and
print(next(it))
>>>pepper
```

### next()函数获取迭代器中下一个元素

除了可以使用for循环处理迭代器中的元素以外，还可以使用next()函数，它实际上是调用iterator. __ next __ ()，每调用一次该函数，就返回迭代器的下一个元素。如果已经是最后一个元素了，再继续调用 next( ) 就会抛出StopIteration异常。一般来说，StopIteration 异常是用来通知我们迭代结束的:

```
with open('a.txt') as fd:
    try:
        while True:
            line = next(fd)
            print(line, end='')
    except StopIteration:
        pass
```

或者，为next()函数指定第二个参数(默认值)，当执行到迭代器末尾后，返回默认值，而不是抛出异常:

```
with open('a.txt') as fd:
        while True:
            line = next(fd, None)
            if line is None:
                break
            print(line, end='')
```

### 可迭代的对象与迭代器的对比

首先，我们要明确可迭代的对象和迭代器之间的关系: **Python从 可迭代的对象中获取选代器**

比如，用for循环迭代一个字符串'ABC'，字符串是可迭代的对象。for 循环的背后会先调用iter(s) 将字符串转换成迭代器，只不过我们看不到:

```
s = 'ABC'
for char in s:
    print(char)
>>>A
>>>B
>>>C
```

如果没有for循环，就不得不使用while循环来模拟

```
s = 'ABC'
it = iter(s)

while True:
    try:
        print(next(it))
    except StopIteration:
        del it
        break
>>>A
>>>B
>>>C
```

**StopIteration异常表明迭代器到头了, Python语言内部会处理for循环和其它迭代上下文(如列表推导、元组拆包等)中的StopIteration异常**

使用章节2.2中定义的Sentence 类，演示如何使用iter() 函数来构建迭代器，并使用next() 函数依次获取迭代器中的元素:

```
import re
import reprlib

RE_WORD = re.compile('\w+')


class Sentance:
    def __init__(self, text):
        self.text = text
        self.words = RE_WORD.findall(text)

    def __repr__(self):
        return "Sentence({})".format(reprlib.repr(self. text))

    def __iter__(self):
        return SentanceIteratot(self.words)


class SentanceIteratot:
    def __init__(self, words):
        self.words = words
        self.index = 0

    def __next__(self):
        try:
            word = self.words[self.index]
        except IndexError:
            raise StopIteration()
        self.index += 1
        return word

    def __iter__(self):
        return self


s = Sentance('Pig and Pepper')
it = iter(s)
print(s)
>>>Sentence('Pig and Pepper')
print(it)
>>><__main__.SentanceIteratot object at 0x00000000022BD278>
print(next(it))
>>>Pig
print(it.__next__())
>>>and
print(next(it))
>>>Pepper
print(next(it))
>>>Traceback (most recent call last):
  	File "F:/python实训-岳才智/19-07/19-07-第四周/ch07-29/Demo01·19.07.29.py", line 46, in <module>
       print(next(it))
    File "F:/python实训-岳才智/19-07/19-07-第四周/ch07-29/Demo01·19.07.29.py", line 28, in __next__
       raise StopIteration()
   StopIteration
print(list(it))
>>>[]
print(list(iter(s)))
>>>['Pig', 'and', 'Pepper']
```

总结:

- 迭代器要实现_next_()方法，返回迭代器中的下一个元素

- 迭代器还要实现_iter_ ()方法，返回迭代器本身，因此，迭代器可以选代。迭代器都是可迭代的对象

- 可迭代的对象一 定不能是自身的迭代器。也就是说， 可迭代的对象必须实现 __ iter __ ()方法，但不能实现 

  __ next __()方法

## 生成器

在Python中，可以使用生成器让我们在迭代的过程中不断计算后续的值，而不必将它们全部存储在内存中:

```
def fib():
    a, b = 0, 1
    while True:
        yield a
        a, b = b, a + b


g = fib()
counter = 1
for i in g:
    print(i, end=' ')
    counter += 1
    if counter > 10:
        break
>>>0 1 1 2 3 5 8 13 21 34 
```

### 生成器函数

只要Python函数的定义体中有yield 关键字，该函数就是生成器函数。调用生成器函数时，会返回一个生成器(generator)对象。也就是说，**生成器函数是生成器工厂**

普通的函数与生成器函数在语法上唯一的区别是， 在后者的定义体中有yield 关键字

```
def gen_AB():
    print('start')
    yield 'A'
    print('continue')
    yield 'B'
    print('end')


print(gen_AB)
>>><function gen_AB at 0x00000000004C1E18>
g = gen_AB()
print(g)
>>><generator object gen_AB at 0x0000000002176830>
print(next(g))
>>>start
>>>A
print(next(g))
>>>continue
>>>B
print(next(g))
>>>end
>>>Traceback (most recent call last):
     File "F:/python实训-岳才智/19-07/19-07-第四周/ch07-29/Demo01·19.07.29.py", line 156, in <module>
       print(next(g))
   StopIteration
```

调用生成器函数后会创建一个新的生成器对象，但是此时还不会执行函数体。

第一次执行next(g)时，会激活生成器，生成器函数会向前**前进到**函数定义体中的**下一个yield语句**，**生成**yield关键字后面的表达式的值，在函数定义体的当前位置暂停，并返回生成的值。具体为:

- 执行print('start')输出start
- 执行yield 'A',此处yield关键字后面的表达式为'A'，即表达式的值为A.所以整条语句会生成值A,在函数定义体的当前位置暂停，并返回值A,我们在控制台上看到输出A

第二次执行next(g)时，生成器函数定义体中的代码由yield 'A' 前进到yield 'B' ，所以会先输出continue,并生成值B,又在函数定义体的当前位置暂停，返回值B

第三次执行next(g)时，由于函数体中没有另一个yield 语句，所以前进到生成器函数的末尾，会先输出end。到达生成器函数定义体的末尾时，生成器对象抛出StopIteration 异常

**注意用词:普通函数返回值，调用胜成器函数返回生成器，生成器产出或生成值**

调用生成器还数后，会构建一个实现了迭代器接口的生成器对象，即，**生成器一定是迭代器!**

```
def gen_AB():
    print('start')
    yield 'A'
    print('continue')
    yield 'B'
    print('end')
    
   
for c in gen_AB():
    print('-->', c)
>>>start
>>>--> A
>>>continue
>>>--> B
>>>end
```

**迭代器和生成器都是为了惰性求值(lazy evaluation)，避免浪费内存空间**。而上面的Sentence 类却不具备惰性，因为RE_WORD.findall(text)会创建所有匹配项的列表，然后将其绑定到self.words 属性上。如果我们传入一个非常大的文本，那么该列表使用的内存量可能与文本本身一样多，而假设我们只需要迭代前几个单词，那么将浪费大量的内存。

re. finditer函数是re . findall函数的惰性版本，返回的不是列表，而是一一个迭代器，按需生成re.Matchobject实例。如果有很多匹配，re.finditer 函数能节省大量内存。我们要使用这个函数让Sentence类变得懒惰，即只在需要时才生成下一个单词: 

```
import re
import reprlib


RE_WORD = re.compile('\w+')


class Sentence:
    def __init__(self, text):
        self.text = text

    def __repr__(self):
        return 'Sentence(%s)'% reprlib.repr(self.text)

    def __iter__(self):
        for match in RE_WORD.finditer(self.text):
            yield match.group()
```

### 生成器表达式

简单的生成器函数(有 yield关键字)，可以替换成生成器表达式(没有 yield 关键字，将列表推导中的[]替换为()即可),让代码变得更简短

生成器表达式可以理解为列表推导的情性版本:不会迫切地构建列表，而是返回一一个生成器，按需惰性生成元素。也就是说，如果列表推导是制造列表的工厂，那么生成器表达式就是制造生成器的工厂: 

```
def gen_AB():
    print('start')
    yield 'A'
    print('continue')
    yield 'B'
    print('end')


res1 = [x*3 for x in gen_AB()]
for i in res1:
    print('-->', i)
>>>start
>>>continue
>>>end
>>>--> AAA
>>>--> BBB
res2 = (x*3 for x in gen_AB())
for i in res2:
    print('-->', i)
>>>start
>>>--> AAA
>>>continue
>>>--> BBB
>>>end
```

可以看出,**生成器表达式会产生生成器**,因此可以使用生成器表达式进一步减少Sentence类的代码:

```
import re
import reprlib


RE_WORD = re.compile('\w+')


class Sentence:
    def __init__(self, text):
        self.text = text

    def __repr__(self):
        return 'Sentence(%s)'% reprlib.repr(self.text)

    def __iter__(self):
        for match in RE_WORD.finditer(self.text):
            yield (match.group() for match in RE_WORD.finditer(self.text))
```

何时使用生成器表达式?

生成器表达式是创建生成器的简洁语法，这样无需先定义函数再调用。不过，生成器习数 灵活得多，可以使用多个语句实现复杂的逻辑，也可以作为协程使用(后续博文介绍)

遇到简单的情况时，可以使用生成器表达式，因为这样扫一眼就知道代码的作用。如果生成器表达式要分成多行写，我倾向于定义生成器函数，以便提高可读性。此外，生成器函数 有名称，因此可以重用

如果将生成器表达式传入只有一个参数的函数时，可以省略生成器表达式外面的() :

```
print(list((x*2 for x in range(5))))
[0, 2, 4, 6, 8]
print(list(x*2 for x in range(5)))
[0, 2, 4, 6, 8]
```

### 嵌套的生成器

可以将多个生成器像管道(pipeline)一样链接起来使用,更高效的处理数据

```
def integers():
    for i in range(1, 9):
        yield i


chain = integers()
print(list(chain))
>>>[1, 2, 3, 4, 5, 6, 7, 8]

def squared(seq):
    for i in seq:
        yield i * i


chain = squared(integers())
print(list(chain))
>>>[1, 4, 9, 16, 25, 36, 49, 64]

def negated(seq):
    for i in seq:
        yield -i


chain = negated(squared(integers()))
print(list(chain))
>>>[-1, -4, -9, -16, -25, -36, -49, -64]
```

由于上面各生成器函数的功能都非常简单，所以可以使用生成器表达式进一步优化链式生成器:

```
integers = range(1, 9)
squared = (i * i for i in integers)
negated = (-i for i in squared)
print(negated)
>>><generator object <genexpr> at 0x0000000001E368E0>
print(list(negated))
>>>[-1, -4, -9, -16, -25, -36, -49, -64]
```

### yield from

yield from是在Python3.3才出现的语法。所以这个特性在Python2中是没有的。

yield from后面需要加的是可迭代对象，它可以是普通的可迭代对象，也可以是迭代器，甚至是生成器。

#### 简单应用:拼接可迭代对象

我们可以用一个使用yield和一一个使用yield from的例子来对比看下。
使用yield

```
astr = 'ABC'
alist = [1, 2, 3]
adict = {'name': ' wangbm', 'age': 18}
agen = (i for i in range(4, 8))


def gen(*args):
    for item in args:
        for i in item:
            yield i


new_list = gen(astr, alist, adict, agen)
print(list(new_list))
>>>['A', 'B', 'C', 1, 2, 3, 'name', 'age', 4, 5, 6, 7]
```

使用yield from

```
astr = 'ABC'
alist = [1, 2, 3]
adict = {'name': ' wangbm', 'age': 18}
agen = (i for i in range(4, 8))


def gen(*args):
    for item in args:
        yield from item


new_list = gen(astr, alist, adict, agen)
print(list(new_list))
>>>['A', 'B', 'C', 1, 2, 3, 'name', 'age', 4, 5, 6, 7]
```

由上面两种方式对比，可以看出，yield from后面加上可迭代对象，他可以把可迭代对象里的每个元素一个一个的yield出来，对比yield来说代码更加简洁，结构更加清晰。

#### 复杂应用:生成器的嵌套

当yield from后面加上一个生成器后，就实现了生成的嵌套。

当然实现生成器的嵌套，并不是-一定必须要使用yield from ，而是使用yield from可以让我们避免让我们自己处理各种料想不到的异常，而让我们专注于业务代码的实现。

讲解之前，首先要知道几个概念:

1. 调用方:调用委派生成器的客户端(调用方)代码
2. 委托生成器 :包含yield from表达式的生成器函数
3. 子生成器 : yield from后面加的生成器函数

你可能不知道他们都是什么意思，没关系，来看下这个例子。

这个例子，是实现实时计算平均值的。比如，第一次传入10,那返回平均数自然是10.第二次传入20,那返回平均数是(10+20)/2=15第三次传入30，那返回平均数(10+20+30)/3=20

```
# 子生成器
def average_gen():
    total = 0
    count = 0
    average = 0
    while True:
        new_num = yield average
        count += 1
        total += new_num
        average = total/count


# 委托生成器
def proxy_gen():
    while True:
        yield from average_gen()


# 调用方
def main():
    calc_average = proxy_gen()
    next(calc_average)              # 预缴下生成器
    print(calc_average.send(10))    # 打印: 10.0
    print(calc_average.send(20))    # 打印: 15.0
    print(calc_average.send(30))    # 打印: 20.0


if __name__ == '__main__':
    main()
>>>10.0
>>>15.0
>>>20.0
```

**委托生成器的作用是**:在调用方与子生成器之间建立-一个双向通道。

所谓的双向通道是什么意思呢?调用方可以通过send()直接发送消息给子生成器，而子生成器yield的值，也是直接返回给调用方。