# 函数

### 定义一个函数

Python定义函数用def关键字,一般格式如下

```
def 函数名(参数列表):
    函数体
```

函数名的命名规则

函数名必须以下划线或字母开头，可以包含任意字母、数字或下划线的组合。不能使用任何的标点符号，函数名是区分大小写的。函数名不能是保留字。

```
def hello():
    print('Hello neuedu')
hello()
>>>Hello neuedu
```

形参和实参

形参:形式参数，不是实际存在，是虚拟变量。在定义函数和函数体的时候使用形参，目的是在函数调用时接收实参(实参个数，类型应与实参一一对应)

实参:实际参数，调用函数时传给函数的参数，可以是常量，变量，表达式，函数，传给形参

区别:形参是虚拟的，不占用内存空间，形参变量只有在被调用时才分配内存单元，实参是一个变量，占用内存空间，数据传送单向，实参传给形参，不能形参传给实参

```
def area(width,height):
    return width * height
w = 4
h = 5
print(area(w,h))
>>>20
```

width和height是形参,w=4和h=5是实参

### 使用函数的好处

1. 代码重用
2. 便于修改,易拓展

例:

```
msg = 'abcdefg'
msg = msg[:2] + 'z' + msg[3:]
print(msg)
msg = '1234567'
msg = msg[:2] + '9' + msg[3:]
print(msg)
>>>abzdefg
>>>1294567
```

改进

```
def setstr(msg,index,char):
    return msg[:index] + char + msg[index+1:]
msg = 'abcdefg'
print(setstr(msg,2,'z'))
msg = '1234567'
print(setstr(msg,2,'9'))
>>>abzdefg
>>>1294567
```

### 函数的参数

必需参数

关键字参数

默认参数

不定长参数

##### 必需参数

必需参数须以正确的顺序传入函数.调用时的数量必须和声明时的一样

```
def f(name,age):
    print('I am %s,I am %d'%(name,age))
f('alex',18)
f('alvin',16)
>>>I am alex,I am 18
>>>I am alvin,I am 16
```

##### 关键字参数

关键字参数和函数调用关系紧密，函数调用使用关键字参数来确定传入的参数值。使用关键字参数允许函数调用时参数的顺序与声明时不一致，因为 Python 解释器能够用参数名匹配参数值。

```
def f(name,age):
    print('I am %s,I am %d'%(name,age))
# f(18,'alex')      报错
f(age=16,name='alvin')
>>>I am alvin,I am 16
```

##### 默认参数

调用函数时,缺省参数的值如果没有传入,则被认为是默认值.下例会打印默认的age,如果age没有被传入:

```
def print_info(name,age,sex='male'):
    print('Name:%s'%name)
    print('age:%s'%age)
    print('Sex:%s'%sex)
    return
print_info('alex',18)
print_info('铁锤',40,'female')
>>>Name:alex
>>>age:18
>>>Sex:male
>>>Name:铁锤
>>>age:40
>>>Sex:female
```

不定长参数

你可能需要一个函数能处理比当初声明时更多的参数.这些参数叫做不定长参数,和上述2种参数不同,声明时不会命名.

```
def add(*tuples):
    sum = 0
    for v in tuples:
        sum += v
    return sum
print(add(1,4,6,9))
print(add(1,4,6,9,5))
>>>20
>>>25
```

加了星号(*)的变量名会存放所有未命名的变量参数。而加(**)的变量名会存放命名的变量参数

```
def print_info(**kwargs):
    print(kwargs)
    for i in kwargs:
        print('%s:%s'%(i,kwargs[i]))
    return
print_info(name='alex',age=18,sex='female',hobby='girl',nationality='Chinese',ability='Python')
>>>{'name': 'alex', 'age': 18, 'sex': 'female', 'hobby': 'girl', 'nationality': 'Chinese', 'ability': 'Python'}
>>>name:alex
>>>age:18
>>>sex:female
>>>hobby:girl
>>>nationality:Chinese
>>>ability:Python
def print_info(name,*args,**kwargs):
    print('Name:%s'% name)
    print('args:',args)
    print('kwargs:',kwargs)
    return
print_info('alex',18,hobby='girl',nationality='Chinese',ability='Python')
>>>Name:alex
>>>args: (18,)
>>>kwargs: {'hobby': 'girl', 'nationality': 'Chinese', 'ability': 'Python'}
```

注意,还可以这样传参:

```
def f(*args):
    print(args)
f(*[1,2,5])
def x(**kargs):
    print(kargs)
x(**{'name':'alex'})
>>>(1,2,5)
>>>{'name': 'alex'}
```

PyCharm的调试工具

F8 Step Over 可以单步执行代码,会把函数调用看作是一行代码直接执行

F7 Step Into 可以单步执行代码,如果是函数,会进入函数内部

### 函数的返回值

要想获取函数的执行结果，就可以用return语句把结果返回

注意:

函数在执行过程中只要遇到return语句,就会停止执行并返回结果,所以也可以理解为return语句代表着函数的结束

如果未在函数中指定return,那这个函数的返回值为None

return多个对象,解释器会把这多个对象组装成一个元组作为一个一个整体结果输出。

```
def sum_and_avg(list):
    sum = 0
    count = 0
    for e in list:
        if isinstance(e,int) or isinstance(e,float):
            count += 1
            sum += e
    return sum,sum/count
my_list = [20,15,2.8,'a',35,5.9,-1.8]
tp = sum_and_avg(my_list)
print(tp)
>>>(76.9, 12.816666666666668)
```

### 高阶函数

高阶函数是至少满足下列一个条件的函数:

接受一个或多个函数作为输入输出一个函数

```
def add(x,y,f):
    return f(x)+f(y)
res = add(3,-6,abs)
print(res)
>>>9
def method():
    x = 2
    def double(n):
        return n * x
    return double
fun = method()
num = fun(20)
print(num)
>>>40
```

### 函数作用域

##### 作用域介绍

python中的作用域分4种情况:

L: local,局部作用域，即函数中定义的变量;E: enclosing, 嵌套的父级函数的局部作用域，即包含此函数的_上级函数的局部作用域，但不是全局的;G: global, 全局变量，就是模块级别定义的变量;B: built-in,系统固定模块里面的变量，比如int, bytearray等。搜索变量的优先级顺序依次是:作用域局部>外层作用域>当前模块中的全局>python内置作用域，也就是LEGB。



当然，local和enclosing是相对的，enclosing变量相对上层来说也是local.

```
x = str(100) # int bulit-in
print('hello' + x)
g_count = 0 # global
def outer():
    o_count = 1 # enclosing
    def inner():
        i_count = 2 # local
        print(o_count)
    # print(i_count) 找不到
    inner()
outer()
# print(o_count) 找不到
>>>hello100
>>>1
```

##### 作用域产生

在Python中，只有模块（module），类（class）以及函数（def、lambda）才会引入新的作用域，其它的代码块（如if、try、for等）是不会引入新的作用域的

```
if 2>1:
    x = 1
print(x)
>>>1
```

这个是没有问题的，if并没有引入一个新的作用域，x仍处在当前作用域中，后面代码可以使用。

```
def test():
    x = 2
print(x) # NameError: name 'x2' is not defined
```

def、class、lambda是可以引入新作用域的。

##### 变量的修改

```
x=6
def f2():
    print(x)
    x=5
f2()

# 变量是先声明，再引用的
# 错误的原因在于 print(x)，解释器会在局部作用域找，会找到x=5(函数已经加载到内存),但x使用在声明前了,所以报错:
# local variable 'x' referenced before assignment.如何证明找到了x=5呢?简单:注释掉x=5,x=6
# 报错为:name 'x' is not defined
#同理

x=6
def f2():
    x+=1 #local variable 'x' referenced before assignment.  x 使用之前已经被声明了
#x+=1：x = x + 1；x 已经被声明了，x=6，这里等于 6 = 6 + 1，发生报错
f2()
```

要修改:

```
x=6

def f2():
    global x # 默认找 local 里的 x，加上 global关键字让他去找外面 global 的 x
    print(x)
    x=5  # 对 global 的 x 进行修改
    
f2()      # 6
print(x)  # 5global关键字
```

##### global关键字

当内部作用域想修改外部作用域的变量时，就要用到global和nonlocal关键字了，当修改的变量是在全局作用域（global作用域）上的，就要使用global先声明一下

```
total = 0 # 定义全局变量
def sum(arg1,arg2):
    total = arg1 +arg2 # 这里的total是局部变量
    print('函数内是局部变量:',total)
    return total
sum(10,20)
print('函数外是全局变量:',total)
num = 1
def fun():
    global num # 加了global后,在函数内部是可以改变外面的全局变量
    num = 123
    print('函数内是局部变量:',num)
fun()
print('函数外是全局变量:',num)
>>>函数内是局部变量: 30
>>>函数外是全局变量: 0
>>>函数内是局部变量: 123
>>>函数外是全局变量: 123
```

##### nonlocal关键字

global关键字声明的变量必须在全局作用域上，不能嵌套作用域上，当要修改嵌套作用域（enclosing作用域，外层非全局作用域）中的变量怎么办呢，这时就需要nonlocal关键字了

```
def outer():
    count = 1
    def inner():
        count = 12
    inner()
    print(count)
outer()
>>>1
def outer():
    count = 1
    def inner():
        # 使用nonlocal关键字可以在一个嵌套的函数中修改嵌套作用域中的变量
        nonlocal count
        count = 12
    inner()
    print(count)
outer()
>>>12
```

##### 小结

1. 变量查找顺序: LEGB，作用域局部>外层作用域>当前模块中的全局>python内置作用域;
2. 只有模块、类、及函数才能引入新作用域;
3. 对于一一个变量，内部作用域先声明就会覆盖外部变量，不声明直接使用，就会使用外部作用域的变量;
4. 内部作用域要修改外部作用域变量的值时，全局变量要使用global关键字，嵌套作用域变量要使用nonlocal关键字。nonlocal是 python3新增的关键字，有了这个关键字，就能完美的实现闭包了。

### 递归函数

定义:在函数内部,可以调用其他函数.如果一个函数在内部调用自身本身,这个函数就是递归函数

```
def factorial(n):
    result = n
    for i in range(1,n):
        result *= i
    return result
print(factorial(4))
>>>24

#**********递归**********
def factorial_new(n):
    if n == 1:
        return 1
    return n*factorial_new(n-1)
print(factorial_new(3))
>>>6
```

```
def fibo(n):
    before = 0
    after = 1
    for i in range(n-1):
        ret = before + after
        before = after
        after = ret
    return ret
print(fibo(3))
>>>2

#**********递归**********
def fibo_new(n):
    if n <= 1:
        return n
    return(fibo_new(n-1) + fibo_new(n-2))
print(fibo_new(3))
>>>2
```

1 print(fibo_ new(30000))# maximum recursion depth exceeded in comparison递归函数的优点:是定义简单，逻辑清晰。理论上，所有的递归函数都可以写成循环的方式，但循环的逻辑不如递归清晰。

##### 递归特性

1. 必须有一个明确的结束条件
2. 每次进入更深一层递归时，问题规模相比上次递归都应有所减少
3. 递归效率不高，递归层次过多会导致栈溢出(在计算机中，函数调用是通过栈(stack) 这种数据结构实现的，每当进入一个函数调用，栈就会加一层栈帧，每当函数返回，栈就会减- -层栈帧。由于栈不是无限的，所以，递归调用的次数过多，会导致栈溢出。)

### 匿名函数

匿名函数就是不需要显式的指定函数名。

```
calc = lambda n : n**n
print(calc(10))
```

关键字lambda表示匿名函数，冒号前面的n表示函数参数，可以有多个参数;

匿名函数有个限制，就是只能有一个表达式，不用写return，返回值就是该表达式的结果;

用匿名函数有个好处，因为函数没有名字，不必担心函数名冲突。此外，匿名函数也是-一个函数对象，也可以把匿名函数赋值给一一个变量， 再利用变量来调用该函数;

有些函数在代码中只用一次，而且函数体比较简单，使用匿名函数可以减少代码量，看起来比较”优雅“

```
def calc(x,y):
    return x**y
#换成匿名函数
calc = lambda x,y:x**y
print(calc(2,5))
>>>32
>>>32
def calc(x,y):
    if x>y:
        return x*y
    else:
        return x/y
#换成匿名函数
calc = lambda x,y:x * y if x > y else x / y
print(calc(2,5))
>>>0.4
>>>0.4
```

匿名函数主要与其他函数联合使用

### 内置函数

```
abs()	dict()	help()	min()	setattr()
all()	dir()	hex()	next( )	slice()
any()	divmod()	id()	object()	sorted()
ascii()	enumerate()	input()	oct()	staticmethod()
bin()	eval()	int()	open()	str()
bool()	exec()	isinstance()	ord()	sum()
bytearray()	filter()	issubclass()	pow()	super( )
bytes()	float()	iter()	print()	tuple()
callable()	format()	len()	property()	type()
chr()	frozenset()	list()	range()	vars()
classmethod( )	getattr()	locals()	repr()	zip()
compile()	globals()	map()	reversed()	_import_()
complex()	hasattr()	max( )	round()	
delattr()	hash()	memoryview( )	set()
```

##### map函数

map()函数接收两个参数，-一个是函数，-个是Iterable ，map 将传入的函数依次作用到序列的每个元素

并把结果作为新的Iterator返回

遍历序列，对序列中每个元素进行函数操作，最终获取新的序列。

```
# 一般解决方案
li = [1,2,3,4,5,6,7,8,9]
for ind,val in enumerate(li):
    li[ind] = val *val
print(li)
>>>[1, 4, 9, 16, 25, 36, 49, 64, 81]
# 高级解决方案
li = [1,2,3,4,5,6,7,8,9]
print(list(map(lambda x:x*x,li)))
>>>[1, 4, 9, 16, 25, 36, 49, 64, 81]
```

##### reduce函数

reduce把一一个函数作用在一个序列[x1, x2, x3, ...上，这个函数必须接收两个参数，reduce 把结果继续和

序列的下一个元素做累积计算，其效果就是:

​					reduce(func,[1,2,3])等同于func(func(1,2),3)

对于序列内所有元素进行累计操作

```
# 接受一个list并利用reduce()求积
from functools import reduce
li = [1,2,3,4,5,6,7,8,9]
print(reduce(lambda x,y:x * y,li))
>>>362880
```

##### filter函数

filter()也接收一一个函数和- -个序列。和map()不同的是，filter() 把传入的函数依次作用于每个元素，然后

根据返回值是True还是False 决定保留还是丢弃该元素。

对于序列中的元素进行筛选，最终获取符合条件的序列

```
# 在一个list中,删除偶数,只保留奇数
li = [1,2,4,5,6,9,10,15]
print(list(filter(lambda x:x % 2==1,li)))
>>>[1, 5, 9, 15]
# 回数是指从左向右读和从右向左读都是一样的数,例如12321,909.请利用filter()筛选出回数
li = list(range(1,200))
print(list(filter(lambda x:int(str(x))==int(str(x)[::-1]),li)))
>>>[1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 22, 33, 44, 55, 66, 77, 88, 99, 101, 111, 121, 131, 141, 151, 161, 171, 181, 191]
```

##### sorted函数

```
sorted(iterable, /, *，key=None, reverse=False)
```

接收一个key函数来实现对可迭代对象进行自定义的排序

可迭代对象:主要与列表，字符串，元祖，集合和字典

key:接受-一个函数，根据此函数返回的结果，进行排序

 reverse:排序方向，默认为从小到大，reverse=True为逆向

```
li = [-21,-12,5,9,36]
print(sorted(li,key = lambda x:abs(x)))
>>>[5, 9, -12, -21, 36]
"""""""""""""""""""""""
sorted( )函数按照keys进行排序，并按照对应关系返回1 ist相应的元素:
keys排序结果 => [5，9， 12， 21，36]
			   |  |   |    |   |
最终结果	 => [5，9，-12，-21，36]
"""""""""""""""""""""""
```
```
# 把下面单词以首字母排序
li = ['bad','about','Zoo','Credit']
print(sorted(li,key = lambda x : x[0]))、
>>>['Credit', 'Zoo', 'about', 'bad']
"""""""""""""""""""""""
对字符串排序,是按照ASCII的大小比较的,由于'Z' < 'a',结果,大写字母Z会排在小写字母a的前面。
"""""""""""""""""""""""
# 假设我们用一组tuple表示学生名字和成绩
L = [('Bob',75),('Adam',92),('Bart',66),('Lisa',88)]
# 请用sorted()对上述列表分别按名字排序
print(sorted(L,key = lambda x : x[0]))
>>>[('Adam', 92), ('Bart', 66), ('Bob', 75), ('Lisa', 88)]
# 再按照成绩从高到低排序
print(sorted(L,key = lambda x : x[1], reverse = True))
>>>[('Adam', 92), ('Lisa', 88), ('Bob', 75), ('Bart', 66)]
```

### 函数式编程

学会了上面几个重要的函数后，我们就可以来聊一聊函数式编程了。

##### 概念(函数式编程)

函数式编程是一种编程范式， 我们常见的编程范式有命令式编程(Imperativeprogramming)，函数式编程，常见的面向对象编程是也是一种命令式编程。

命令式编程是面向计算机硬件的抽象，有变量(对应着存储单元)，赋值语句(获取，存储指令)，表达式(内存引用和算术运算)和控制语句(跳转指令)，一句话，命令式程序就是-个冯诺依曼机的指令序列。

而函数式编程是面向数学的抽象，将计算描述为一种表达式求值，一句话，函数式程序就是一个表达式。

##### 函数式编程的本质

函数式编程中的函数这个术语不是指计算机中的函数，而是指数学中的函数，即自变量的映射。也就是说一个函数的值仅决定于函数参数的值，不依赖其他状态。比如y=x* x函数计算x的平方根，只要x的平方，不论什么时候调用，调用几次，值都是不变的。

纯函数式编程语言中的变量也不是命令式编程语言中的变量，即存储状态的单元，而是代数中的变量，即一个值的名称。变量的值是不可变的(immutable) ，也就是说不允许像命令式编程语言中那样多次给- -个变量赋值。比如说在命令式编程语言我们写“x=x+1”，这依赖可变状态的事实，拿给程序员看说是对的，但拿给数学家看，却被认为这个等式为假。

函数式语言的如条件语句，循环语句也不是命令式编程语言中的控制语句，而是函数的语法糖。

严格意义 上的函数式编程意味着不使用可变的变量，赋值，循环和其他命令式控制结构进行编程。

函数式编程关心数据的映射，命令式编程关心解决问题的步骤，这也是为什么“函数式编程叫做函数式编程”。

##### 函数式编程的好处

1. 代码简洁，易懂。

2. 无副作用

   ​	由于命令式编程语言也可以通过类似函数指针的方式来实现高阶函数，函数式的最主要的好处主要是不可变性带来的。没有可变的状态，函数就是引|用透明( Referential transparency) 的和没有副作用(No SideEffect) 。

### 将函数存储在模块中

函数的优点之一是，使用它们可将代码块与主程序分离。通过给函数指定描述性名称，可让主程序容易理解得多。你还可以更进一步，将函数存储在被称为**模块**的独立文件中，再将模块**导入**到主程序中。import 语句允许在当前运行的程序文件中使用模块中的代码。

通过将函数存储在独立的文件中，可隐藏程序代码的细节，将重点放在程序的高层逻辑上。这还能让你在众多不同的程序中重用函数。将函数存储在独立文件中后，可与其他程序员共享这些文件而不是整个程序。知道如何导入函数还能让你使用其他程序员编写的函数库。

导入模块的方法有多种，下面对每种都作简要的介绍。

##### 导入整个模块

要让函数是可导入的，得先创建模块。模块是扩展名为.py的文件，包含要导入到程序中的代码。下面来创建一个包含函数make_ pizza() 的模块。

**pizza.py**

```
def make_pizza(size,*toppings):
    """描述要制作的披萨"""
    print("\nMaking a"+ str(size)+"-inch pizza with the following toppings:")
    for topping in toppings:
        print("-"+topping)
```

接下来，我们在pizza.py所在的目录中创建另一个名为making_pizzas.py的文件， 这个文件导入刚创建的模块，再调用make_pizza()两次；

**making_pizza.py**

```
import pizza
pizza.make_pizza(16,'pepperoni')
pizza.make_pizza(12,'mushrooms','green peppers','extra cheese')
```

Python读取这个文件时，代码行import pizza 让Python打开文件pizza.py,并将其中的所有函数都复制到这个程序中。你看不到复制的代码，因为这个程序运行时，Python在幕后 复制这些代码。你只需知道，在making_ pizzas.py中 ，可以使用pizza.py中定义的所有函数。

```
Making a16-inch pizza with the following toppings:
-pepperoni

Making a12-inch pizza with the following toppings:
-mushrooms
-green peppers
-extra cheese
```

这就是一种导入方法:只需编写一 条import 语句并在其中指定模块名，就可在程序中使用该模块中的所有函数。如果你使用这种import 语句导入了名为module _name . py的整个模块，就可使用下面的语法来使用其中任何一个函数:

```
_module_name.function_name_()
```

##### 导入特定的函数

你还可以导入模块中的特定函数，这种导入方法的语法如下:

```
from _module_name_ import _function_name_
```

通过用逗号分隔函数名，可根据需要从模块中导入任意数量的函数: 

```
from _module_name_ import _function_0,function_1,function_2_
```

对于前面的making_pizzas.py示例， 如果只想导入要使用的函数，代码将类似于下面这样:

```
from pizza import make_pizza
pizza.make_pizza(16,'pepperoni')
pizza.make_pizza(12,'mushrooms','green peppers','extra cheese')
```

若使用这种语法，调用函数时就无需使用句点。由于我们在import语句中显式地导入了函数make_pizza() ，因此调用它时只需指定其名称。

##### 使用as给函数指定别名

如果要导入的函数的名称可能与程序中现有的名称冲突，或者函数的名称太长，可指定简短而独一无二 的**别名**--函数的另一个名称，类似于外号。要给函数指定这种特殊外号，需要在导入它时这样做。

下面给函数make pizza() 指定了别名mp()。这是在import 语句中使用make. pizza as mp实现的关键字as将函数重命名为你提供的别名:

```
from pizza import make_pizza as mp
mp(16,'pepperoni')
mp(12,'mushrooms','green peppers','extra cheese')
>>>Making a16-inch pizza with the following toppings:
>>>-pepperoni

>>>Making a12-inch pizza with the following toppings:
>>>-mushrooms
>>>-green peppers
>>>-extra cheese
```

上面的import 语句将函数make_pizza()重命名为mp() ;在这个程序中，每当需要调用make_ pizza() 时，都可简写成mp() ，而Python将运行make_ pizza() 中的代码，这可避免与这个程序可能包含的函数make_ pizza() 混淆。

指定别名的通用语法如下:

```
from _module_name_ import _function_name_ as _fn_
```

##### 使用as给模块指定别名

你还可以给模块指定别名。通过给模块指定简短的别名(如给模块pizza 指定别名p )，让你能够更轻松地调用模块中的函数。相比于pizza.make_ pizza()，p.make_ pizza() 更为简洁:

```
import pizza as p
p.make_pizza(16,'pepperoni')
p.make_pizza(12,'mushrooms','green peppers','extra cheese')
>>>Making a16-inch pizza with the following toppings:
>>>-pepperoni

>>>Making a12-inch pizza with the following toppings:
>>>-mushrooms
>>>-green peppers
>>>-extra cheese
```

上述import语句给模块pizza指定了别名p，但该模块中所有函数的名称都没变。调用函数make_pizza()时，可编写代码p.make_pizza()而不是pizza.make_pizza()，这样不仅能使代码更简洁，还可以让你不再关注模块名，而专注于描述性的函数名。这些函数名明确地指出了函数的功能，对理解代码而言，它们比模块名更重要。

给模块指定别名的通用语法如下: 

```
import _module_name as mn_
```

##### 导入模块中的所有函数

使用星号( * )运算符可让Python导入模块中的所有函数:

```
from pizza import *
make_pizza(16,'pepperoni')
make_pizza(12,'mushrooms','green peppers','extra cheese')
>>>Making a16-inch pizza with the following toppings:
>>>-pepperoni

>>>Making a12-inch pizza with the following toppings:
>>>-mushrooms
>>>-green peppers
>>>-extra cheese
```

import语句中的星号让Python将模块pizza 中的每个函数都复制到这个程序文件中。由于导入了每个函数，可通过名称来调用每个函数，而无需使用句点表示法。然而，使用并非自己编写的大型模块时，最好不要采用这种导入方法.

最佳的做法是，要么只导入你需要使用的函数，要么导入整个模块并使用句点表示法。这能让代码更清晰，更容易阅读和理解。这里之所以介绍这种导入方法，只是想让你在阅读别人编写的代码时，如果遇到类似于下面的import 语句，能够理解它们:

```
from _module_name_ import *
```

### 函数文档字符串

函数文档字符串documentation string (docstring) 是在函数开头，用来解释其接口的字符串。简而言之:帮助文档

- 包含函数的基础信息

- 包含函数的功能简介

- 包含每个形参的类型，使用等信息

- 必须在函数的首行,经过验证前面有注释性说明是可以的，不过最好函数文档出现在首行

- 使用三引号注解的多行字符串(当然，也可以是一行)，因三引号可以实现多行注解（展示） ("' '") 或 ("" "")

- 函数文档的第一行一 般概述函数的主要功能，第二行空，第三行详细描述。


**查看方式**

- 在交互模式下可以使用he l p查看函数，帮助文档，该界面会跳到帮助界面，需要输入q退出界面
- 使用-doc-属性查看，该方法的帮助文档文字直接显示在交互界面上。代码如下:

```
def test(msg):
    print("函数输出成功"+msg)
test('hello')
print(help(test))
print(test.__doc__)
函数输出成功hello
>>>Help on function test in module __main__:

>>>test(msg)

>>>None
>>>None
```

