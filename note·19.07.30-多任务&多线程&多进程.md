# 多任务&多线程&多进程

## 多任务

### 什么是多任务

什么叫“多任务”呢?简单地说,就是操作系统可以同时运行多个任务。打个比方，你一边在用浏览器上网，一边在听MP3， 一边在用Word赶作业，这就是多任务，至少同时有3个任务正在运行。还有很多任务悄悄地在后台同时运行着，只是桌面上没有显示而已。

现在，多核CPU已经非常普及了，但是，即使过去的单核CPU,也可以执行多任务。由于CPU执行代码都是顺序执行的，那么，单核CPU是怎么执行多任务的呢?

答案就是操作系统控制CPU轮流让各个任务交替执行，任务1执行0.01秒，切换到任务2,任务2执行0.01秒，再切换到任务3，执行0.01秒...这样反复执行下去。表面上看，每个任务都是交替执行的，但是，由于CPU的执行速度实在是太快了，我们感觉就像所有任务都在同时执行一样。

真正的并行执行多任务只能在多核CPU上实现，但是，由于任务数量远远多于CPU的核心数量，所以，操作系统也会自动把很多任务轮流调度到每个核心上执行。

### 并发与并行

- 并发:指的是任务数多余cpu核数，通过操作系统的各种任务调度算法，实现用多个任务“一起”执行(实际上总有一些任务不在执行，因为切换任务的速度相当快，看上去一起执行而已)
- 并行:指的是任务数小于等于cpu核数， 即任务真的是一起执行的

### CPU执行程序的原理

**相关术语**

RAM:指内存，断电后内容无法保存，因此叫做易失性存储;另一个相关的概念是ROM, - 般指外存，例如硬盘。RAM的速度远快于ROM, CPU与内存直接进行数据交换.

CPU:计算机的所有计算操作都由它执行，只要先记住它是一块有输入 和输出的集成电路就行了。

Instruction:指令，是CPU进行操作的基本单元，大致包含操作对象、操作对象的地址、对操作对象进行何种操作。

RAM相关结构

程序要想被CPU执行，首先要被编译成CPU可以执行的指令操作，这里就不详细介绍，本文就假设程序已经被编译好了，放在了内存中。内存中存放的数据分为两类，一类是指令;另-类是数据，不管是指令还是数据都有其对应的地址。

CPU相关结构

这里只放出CPU的执行指令时涉及的基本结构，真实的情况还会复杂很多。

这里涉及到的结构有Program Counter (程序计数器)、Instruction Register (指令寄存器)、DataRegister (数据寄存器)、ALU (算数逻辑单元)，可以将计数器.寄存器都可以简单理解为存放数据的器件。上述程序计数器用来存放指令的地址;指令寄存器用来存放指令(初学者可能会搞混数据和地址的区别，稍加区分就可以分辨) ;数据寄存器存放参与计算的数据.

执行过程
为便于理解，仅涉及到CPU和内存间的数据交换。

在了解了RAM和CPU相关结构之后，接下来就可以正式开始说明执行的过程，其实就是对以上叙述内容的一个组合。

1. 程序计数器初始内容为100，指向内存中的某一项指令， 注意100指的是地址; 
2. 指令寄存 器根据程序计算器的指向地址，将内存中地址为100的指令抓取到自身，此时存放LOAD A, 2000; 
3. CPU按照指令内容，将内存地址为2000的数据， 上载到数据寄存器A中:

以上3步已完成一个指令的基本操作步骤。接下来程序计数器依次指向104指令地址、108指令地址、112指令地址,分别完成将2004地址的数据赋值给B数据寄存器，ALU将A、B内的数据相乘赋值给C数据寄存器，将C数据寄存器数据写入内容地址2008中。

### 程序、进程与线程

- 程序是含有指令和数据的文件，被存储在磁盘或其他的数据存储设备中，也就是说程序是静态的代码。

- 进程是程序的一次执行过程，是系统运行程序的基本单位，因此进程是动态的。系统运行一一个程序即是一个进程从创建，运行到消亡的过程。简单来说，一个进程就是-一个执行中的程序，它在计算机中一个指令接着一一个指令地执行着，同时， 每个进程还占有某些系统资源如CPU时间，内存空间，文件，输入输出设备的使用权等等。换句话说，当程序在执行时，将会被操作系统载入内存中。

- 线程与进程相似，但线程是一 个比进程更小的执行单位。一个进程在其执行的过程中可以产生多个线程。与进程不同的是同类的多个线程共享同一块内存空间和-组系统资源，所以系统在产生一个线程,或是在各个线程之间作切换工作时，负担要比进程小得多，也正因为如此，线程也被称为轻量级进程。

  进程在执行过程中拥有独立的内存单元，而多个线程共享内存，从而极大地提高了程序的运行效率

## 多线程

### 线程的创建

先看下单进程执行的情况

在上面程序中，简单调用两次run方法，该方法会延时2s,输出结果:输出task t1后隔2s，输出taskt2, 2s后
程序结束，一共用了4S。如何让这两个方法同时执行呢，这就需要给每个方法启用一个单独的线程。

#### 启动多个线程(函数方式)

在Python3中，Python提供 了-个内置模块threading.Thread,可以很方便地让我们创建多线程。threading.ThreadO -般接收两个参数:
线程函数名:要放置线程让其后台执行的函数，由我们自已定义，注意不要加O;
线程函数的参数:线程函数名所需的参数，以元组的形式传入。若不需要参数，可以不指定。

```
import time
import threading


def run(n):
    print('task', n)
    time.sleep(2)


t1 = threading.Thread(target=run, args=('t1',))
t2 = threading.Thread(target=run, args=('t2',))
t1.start()
t2.start()
>>>task t1
>>>task t2
```

等待2s后程序结束，程序一共只用了2s。
除了这种简单实现，还可以自己定义类，继承调用。

#### 启动多个线程(类方式)

相比较函数而言，使用类创建线程，会比较麻烦- -点。 首先，我们要自定义一一个类，对于这个类有两点要求，

- 必须继承threading.Thread这个父类:
- 必须覆写run方法。

这里的run方法，和我们上面线程函数的性质是一样的，可以写我们的业务逻辑程序。在start()后将会被自
动调用。

```
import time
import threading


class MyThread(threading.Thread):
    def __init__(self, n, sleep_time):
        super(MyThread, self).__init__()
        self.n = n
        self.sleep_time = sleep_time

    def run(self):
        print('runnint task', self.n)
        time.sleep(self.sleep_time)
        print('task done,', self.n)


t1 = MyThread('t1', 2)
t2 = MyThread('t2', 4)
t1.start()
t2.start()
```

**join()函数**

```
import time
import threading


def run(n):
    print('task', n)
    time.sleep(2)
    print('task done', n)


start_time = time.time()
for i in range(50):
    t = threading.Thread(target=run, args=('t-%s' % i,))
    t.start()

print('----------all threads hsa finished...')
print('cost:',time.time() - start_time)
```

上面的代码在同时启动50个线程后,会直接输出

```
----------all threads hsa finished...
```

发现主线程直接结束，没有等子线程，28后子线程分别task done。代码共有51个线程，-一个主线程与50个子线程，主线程无法计算子线程执行时间。那么，我们如何计算所有线程执行时间?此时需要设置主线程等待子线程执行结束，通过一个临时列表，在线程启动后分别join等待，子线程分别结束后，结束主进程，计算耗时约2.011415958s

```
import time
import threading


def run(n):
    print('task', n)
    time.sleep(2)
    print('task done', n)


start_time = time.time()
t_objs = []
for i in range(50):
    t = threading.Thread(target=run, args=('t-%s' % i,))
    t.start()
    t_objs.append(t)

for t in t_objs:
    print(t.is_alive())

for t in t_objs:
    t.join()

for t in t_objs:
    print(t.is_alive())

print('----------all threads hsa finished...')
print('cost:',time.time() - start_time)
```

is_ alive()方法可以用来判断一一个线程是否结束。
**根据当前线程(Thread)活着的数量来查看线程生命周期**

```
import threading
import time


def sing():
    for i in range(3):
        print('正在唱歌......%d'% i)
        time.sleep(1)


def dance():
    for i in range(3):
        print('正在跳舞......%d'% i)
        time.sleep(1)


if __name__ == '__main__':
    print('晚会开始:%s'% time.ctime())
    t1 = threading.Thread(target=sing)
    t2 = threading.Thread(target=dance)
    t1.start()
    t2.start()

    while True:
        length = len(threading.enumerate())
        print('当前运行的线程数为: %d'% length)
        time.sleep(0.7)
        if length <= 1:
            break
```

输出

```
晚会开始:Tue Jul 30 11:49:59 2019
正在唱歌......0
正在跳舞......0
当前运行的线程数为: 3
当前运行的线程数为: 3
正在唱歌......1
正在跳舞......1
当前运行的线程数为: 3
正在唱歌......2
正在跳舞......2
当前运行的线程数为: 3
当前运行的线程数为: 3
当前运行的线程数为: 1
```

### 多线程互斥锁

为什么要加锁?加锁是为了防止不同的线程访问同一共享资源造成混乱。打个比方:人是不同的线程，卫生间是共享资源。你在上洗手间的时候肯定要把门锁上吧，这就是加锁，只要你在里面，这个卫生间就被锁了，只有你出来之后别人才能用。想象一下如果卫生间的门没有锁会是什么样?

一个防止他人进入的简单方法，就是门口加一把锁( lock = threading.Lock() )。先到的人锁上门( lock.acquire() )，进到房间里(访问数据)，后到的人看到上锁，就在门口排队，等锁打开再进去。刚才进去的人结束数据操作后，从门里出来，释放锁(将锁打开，和钥匙一起挂在门上lock.release() ) ,这就叫Lock,防止多个线程同时读写某一块内存区域。

#### 如何使用Lock (锁)

来简单看下代码，学习如何加锁，获取钥匙，释放锁。

```
import threading
lock = threading.Lock  # 生成锁对象,全局唯一
lock.acquire()         # 获得锁。未获取到会阻塞程序，直到获取到锁才会往下执行
lock.release()         # 释放锁，归还锁，其他人可以拿去用了
```

需要注意的是，lock.acquire()和lock.release()必须成对出现。否则就有可能造成死锁。

很多时候，我们虽然知道，他们必须成对出现，但是还是难免会有忘记的时候。为了规避这个问题，可以使
用使用上下文管理器来加锁。

```
import threading
lock = threading.Lock()
with lock:
    # 这里写自己的代码
    pass
```

with语句会在这个代码块执行前自动获取锁，在执行结束后自动释放锁。

#### 为何要使用锁

这么麻烦，不用锁不行吗?有的时候还真不行。那么为了说明锁存在的意义。我们分别来看下，不用锁的情形有怎样的问题。

```
import threading
import time

g_num = 0


def work1(num):
    global g_num
    for i in range(num):
        g_num += 1
    print('----in work1, g_num is %d----'% g_num)


def work2(num):
    global g_num
    for i in range(num):
        g_num += 1
    print('----in work2, g_num is %d----'% g_num)


print('---线程创建之前g_num is %d---'% g_num)

t1 = threading.Thread(target=work1, args=(1000000,))
t1.start()

t2 = threading.Thread(target=work2, args=(1000000,))
t2.start()

while len(threading.enumerate()) != 1:
    time.sleep(1)

print('2个线程对同一个全局变量操作之后的最终结果是: %s'% g_num)
```

运行结果:

```
---线程创建之前g_num is 0---
----in work1, g_num is 1374605----
----in work2, g_num is 1325510----
2个线程对同一个全局变量操作之后的最终结果是: 1325510
```

结论
如果多个线程同时对同一个全局变量操作，会出现资源竞争问题，从而数据结果会不正确
**使用互斥锁完成2个线程对同一个全局变量各加100万次的操作**

```
import threading
import time

g_num = 0


def test1(num):
    global g_num
    for i in range(num):
        mutex.acquire()
        g_num += 1
        mutex.release()

    print('---test1---g_num is %d'% g_num)


def test2(num):
    global g_num
    for i in range(num):
        mutex.acquire()
        g_num += 1
        mutex.release()

    print('---test2---g_num is %d'% g_num)


mutex = threading.Lock()

t1 = threading.Thread(target=test1, args=(1000000,))
t1.start()

t2 = threading.Thread(target=test2, args=(1000000,))
t2.start()

while len(threading.enumerate()) != 1:
    time.sleep(1)

print('2个线程对同一个全局变量操作之后的最终结果是: %s'% g_num)
```

运行结果:

```
---test1---g_num is 1598104
---test2---g_num is 2000000
2个线程对同一个全局变量操作之后的最终结果是: 2000000
```

可以看到最后的结果,加入互斥锁后,其结果与预期相符

#### 死锁

在线程间共享多个资源的时候，如果两个线程分别占有一部分资源并 且同时等待对方的资源，就会造成死锁。

尽管死锁很少发生，但一旦发生就会造成应用的停止响应。下面看一个死锁的例子

```
# coding-utf-8
import threading
import time


class MyThread1(threading.Thread):
    def run(self):
        mutexA.acquire()
        print(self.name+'----do1---up----')
        time.sleep(1)
        mutexB.acquire()
        print(self.name+'----dol---down----')
        mutexB.release()
        mutexA.release()


class MyThread2(threading.Thread):
    def run(self):
        mutexB.acquire()
        print(self.name+'----do2---up----')
        time.sleep(1)
        mutexA.acquire()
        print(self.name+'----do2---down----')
        mutexA.release()
        mutexB.release()


mutexA = threading.Lock()
mutexB = threading.Lock()

if __name__ == '__main__':
    t1 = MyThread1()
    t2 = MyThread2()
    t1.start()
    t2.start()
```

### 线程问通信

前面已经向大家介绍了,如何使用创建线程，启动线程。相信大家都会有这样-个想法，线程无非就是创建一下，然后再start()下，实在是太简单了。

可是要知道，在真实的项目中，实际场景可要我们举的例子要复杂的多得多，不同线程的执行可能是有顺序的，或者说他们的执行是有条件的，是要受控制的。如果仅仅依靠前面学的那点浅薄的知识，是远远不够的。

那今天，我们就来探讨一下如何控制线程的触发执行。

要实现对多个线程进行控制，其实本质上就是消息通信机制在起作用，利用这个机制发送指令，告诉线程，什么时候可以执行，什么时候不可以执行，执行什么内容。

#### Queue队列

从一个线程向另一个线程发送数据最安全的方式可能就是使用queue库中的队列了。创建一个被多个线程共享的Queue对象，这些线程通过使用put() 和get() 操作来向队列中添加或者删除元素。

对于Queue,我们只需要掌握几个函数即可。

```
from queue import Queue
q = Queue(maxsize=0)  # maxsize默认为0,不受限,一旦>0,而消息数又达到限制,q.put()也将阻塞
q.get()               # 阻塞程序,等待队列消息
q.get(timeout=5.0)    # 获取消息,设置超时时间
q.put()               # 发送消息
q.join()              # 等待所有的消息都被消费完
# 以下三个方法,知道就好,代码中不要使用
q.qsize()             # 查询当前队列的消息个数
q.empty()             # 队列消息是否都被消费完,True/False
q.full()              # 检测队列里消息是否已满
```

举个生产者消费者的例子

```
import random
import threading
import time
import queue

q = queue.Queue(maxsize=10)


def producer(name):
    count = 1
    while True:
        q.put('骨头%s'% count)
        print('生产了骨头', count)
        count += 1
        time.sleep(random.randrange(3))


def consumer(name):
    while True:
        print('[%s]购买了[%s]...' % (name, q.get()))
        time.sleep(random.randrange(5))


p = threading.Thread(target=producer, args=('Tim',))
c1 = threading.Thread(target=consumer, args=('King',))
c2 = threading.Thread(target=consumer, args=('Wang',))

p.start()
c1.start()
c2.start()
```

运行结果如下

```
生产了骨头 1
生产了骨头 2
[King]购买了[骨头1]...
[Wang]购买了[骨头2]...
生产了骨头 3
[King]购买了[骨头3]...
生产了骨头 4
[King]购买了[骨头4]...
生产了骨头 5
[Wang]购买了[骨头5]...
[King]购买了[骨头6]...
生产了骨头 6
[King]购买了[骨头7]...
生产了骨头 7
生产了骨头 8
[King]购买了[骨头8]...
生产了骨头 9
[King]购买了[骨头9]...
生产了骨头 10
[Wang]购买了[骨头10]...
生产了骨头 11
[King]购买了[骨头11]...
生产了骨头 12
生产了骨头 13
生产了骨头 14
生产了骨头 15
生产了骨头 16
生产了骨头 17
[King]购买了[骨头12]...
```

### 线程池

在使用多线程处理任务时也不是线程越多越好，由于在切换线程的时候，需要切换上下文环境，依然会造成cpu的大量开销。为解决这个问题，线程池的概念被提出来了。预先创建好一个较为优化的数量的线程，放到队列中，让过来的任务立刻能够使用，就形成了线程池。

在Python3中，创建线程池是通过concurrent . futures函数库中的ThreadPoolExecutor 类来实现的。

future对象:在未来的某一时刻完成操 作的对象. submit方法可以返回一个future对象.

```
import threading
import time
from concurrent.futures import ThreadPoolExecutor


def add(n1, n2):
    v = n1 + n2
    print('add:', v, ', tid:',threading.currentThread().ident)
    time.sleep(n1)
    return v


ex = ThreadPoolExecutor(max_workers=3)
f1 = ex.submit(add, 2, 3)
>>>add: 5 , tid: 2664
f2 = ex.submit(add, 2, 2)
>>>add: 4 , tid: 2004
print('main thread running')
>>>main thread running
print(f1.done())
>>>False
print(f1.result())
>>>5
```

map方法,返回是跟你提交序列是一致的,是有序的

```
import threading
import requests
from concurrent.futures import ThreadPoolExecutor
URLS = ['http://www.baidu.com', 'http://www.qq.com', 'http://www.sina.com.cn']


def get_html(url):
    print('thread id:',threading.currentThread().ident, ' 访问了:', url)
    return requests.get(url)


ex = ThreadPoolExecutor(max_workers=3)
res_iter = ex.map(get_html,URLS)
for res in res_iter:
    print('url:%s ,len:%d' % (res.url, len(res.text)))
>>>thread id: 3672  访问了: http://www.baidu.com
>>>thread id: 2652  访问了: http://www.qq.com
>>>thread id: 3580  访问了: http://www.sina.com.cn
>>>url:http://www.baidu.com/ ,len:2381
>>>url:https://www.qq.com/ ,len:231552
>>>url:https://www.sina.com.cn/ ,len:571493
```

接下来,使用as_ completed .这个函数为submit而生。

你总想通过一种办法来解决submit后啥时候完成的吧,而不是一次次调用future.done或者使用future result吧。

concurrent.futures.as_ .completed(fs, timeout=None)返回一个生成器在迭代过程中会阻塞。

直到线程完成或者异常时,产生一个Future对象。

同时注意，map方法返回是有序的，as_ completed 是那个线程先完成/失败就返回。

```
import time
import threading
import requests
from concurrent.futures import ThreadPoolExecutor, as_completed
URLS = ['http://www.baidu.com', 'http://www.qq.com', 'http://www.sina.com.cn']


def get_html(url):
    time.sleep(3)
    print('thread id:',threading.currentThread().ident, ' 访问了:', url)
    return requests.get(url)


ex = ThreadPoolExecutor(max_workers=3)
f = ex.submit(get_html, URLS[0])
print('main thread running')
for future in as_completed([f]):
    print('一个任务完成。')
    print(future.result())
```

```
import time
import threading
import requests
from concurrent.futures import ThreadPoolExecutor, as_completed
URLS = ['http://www.baidu.com', 'http://www.qq.com', 'http://www.sina.com.cn']


def get_html(url):
    time.sleep(1)
    print('thread id:', threading.currentThread().ident, ' 访问了:', url)
    return requests.get(url)


ex = ThreadPoolExecutor(max_workers=3)
future_tasks = [ex.submit(get_html, url) for url in URLS]
for future in as_completed(future_tasks):
    try:
        resp = future.result()
    except Exception as e:
        print('%s' % e)
    else:
        print('%s has %d bytes!'%(resp.url, len(resp.text)))
```

wait是阻塞函数,第一个参数和as_ completed一样, 一个可迭代的future序列,返回一个元组,包含2个set,一个完成的，一个未完成的

```
import time
import threading
import requests
from concurrent.futures import ThreadPoolExecutor, wait
URLS = ['http://www.baidu.com', 'http://www.qq.com', 'http://www.sina.com.cn']


def get_html(url):
    time.sleep(1)
    print('thread id:', threading.currentThread().ident, ' 访问了:', url)
    return requests.get(url)


ex = ThreadPoolExecutor(max_workers=3)
future_tasks = [ex.submit(get_html, url) for url in URLS]
try:
    result = wait(future_tasks)
    done_set = result[0]
    for future in done_set:
        resp = future.result()
        print('第一个网页任务完成 url:%s , len:%d bytes! '%(resp.url, len(resp.text)))
except Exception as e:
    print('exception', e)
```

## 多进程

### 进程

程序：例xxx.exe这是程序，是一个静态的

进程：一个程序运行起来后，代码+用到的资源称之为进程，它是操作系统分配资器的基本单元。不仅可以通过线程完成多任务，进程也是可以的

#### 进程的状态

工作中，任务数往往大于cpu的核数。 即一定有一些任务正在执行，而另外一些任务在等件cpu进行执行。因此导致了有了不同的状态

- 就绪态：运行的条件都已经满足，正在等在cpu执行
- 执行态：cpu正在执行其功能
- 等待态：等待某些条件满足，例如一个程序sleep了,此时就处于等待态

#### 进程的创建

python的multiprocessing模块是跨平台版本的多遗程模块,在multiprocessing中,通过创建Process对象生
成进程，然后调用它的start()方法，启动一个任务。

```
import multiprocessing
import time


def run(name):
    time.sleep(2)
    print(name, '进程启动')


if __name__ == '__main__':
    mp = multiprocessing.Process(target=run, args=('LJ',))
    mp.start()
    mp.join()
```

创建子进程时，只需要传入一个执行函数和函数的参数，创建一个Process实例， 用start()方法启动。join()方法可以等待子进程结束后再继续往下运行，通常用于进程间的同步。

Process语法结构如下:

```
Process([group [, target [, name [, args [, kwarg1]]]])
group:指定进程组，大多数情况下用不到
target:如果传递了函数的引用，可以任务这个子进程就执行这里的代码
args:给target指定的函数传递的参数，以元组的方式传递
kwargs:给target指定的函数传递命名参数
name:给进程设定一个名字，可以不设定

Process创建的实例对象的常用方法:
start():启动子进程实例(创建子进程)
is_alive(): 判断进程子进程是否还在活着
join([timeout]):是否等待子进程执行结束，或等待多少秒

Process创建的实列对象的常用属性:
name:当前进程的别名,默认为Process -N, N为从1开始递增的整数
pid:当前进程的pid (进程号)
```

可以同时启动多个进程，进程内部可以再起线程。

```
import multiprocessing
import time
import threading


def thread_run():
    print(threading.get_ident())


def run(name):
    time.sleep(2)
    print(name, '进程启动')
    t = threading.Thread(target=thread_run(), )
    t.start()


if __name__ == '__main__':
    for i in range(10):
        p = multiprocessing.Process(target=run, args=('hello %s' % i,))
        p.start()
```

**进程的pid和ppid**

```
from multiprocessing import Process
import os


def run_proc():
    """
    子进程要执行的代码
    """
    print('子进程运行中，pid=%d...' % os.getpid())    # os.getpid获取当前进程的进程号
    print('子进程将要结束...')
    print('我的父进程是，ppid=%d...' % os.getppid())  # os.getppid获取当前进程的进程号


if __name__ == '__main__':
    print('父进程pid: %d' % os.getpid())  # os.getpid获取当前进程的进程号
    p = Process(target=run_proc())
    p.start()
```

**进程间不同享全局变量**进程间内存是独立的

```
from multiprocessing import Process
import random
import time
import os

nums = [11, 22]


def work1():
    """
    子进程要执行的代码
    """
    print('in process1 pid=%d, nums=%s' % (os.getpid(), nums))
    for i in 'baidu':
        nums.append(i)
        time.sleep(random.random())
        print('in process1 pid=%d, nums=%s' % (os.getpid(), nums))


def work2():
    """
    子进程要执行的代码
    """
    print('in process2 pid=%d, nums=%s' % (os.getpid(), nums))
    for i in 'neuedu':
        nums.append(i)
        time.sleep(random.random())
        print('in process2 pid=%d, nums=%s' % (os.getpid(), nums))


if __name__ == '__main__':
    p1 = Process(target=work1)
    p1.start()

    p2 = Process(target=work2)
    p2.start()

    p1.join()
    p2.join()
```

输出

```
in process1 pid=5056, nums=[11, 22]
in process2 pid=5744, nums=[11, 22]
in process2 pid=5744, nums=[11, 22, 'n']
in process2 pid=5744, nums=[11, 22, 'n', 'e']
in process2 pid=5744, nums=[11, 22, 'n', 'e', 'u']
in process2 pid=5744, nums=[11, 22, 'n', 'e', 'u', 'e']
in process1 pid=5056, nums=[11, 22, 'b']
in process2 pid=5744, nums=[11, 22, 'n', 'e', 'u', 'e', 'd']
in process2 pid=5744, nums=[11, 22, 'n', 'e', 'u', 'e', 'd', 'u']
in process1 pid=5056, nums=[11, 22, 'b', 'a']
in process1 pid=5056, nums=[11, 22, 'b', 'a', 'i']
in process1 pid=5056, nums=[11, 22, 'b', 'a', 'i', 'd']
in process1 pid=5056, nums=[11, 22, 'b', 'a', 'i', 'd', 'u']
```

#### 进程间通信

Process之间有时需要通信，操作系统提供了很多机制来实现进程间的通信。

**Queue的使用**

可以使用multiprocessing模块的Queue实现多进程之间的数据传递，Queue本身是一 个消息列队程序，首先
用一个小实例来演示一下Queue的工作原理 :

```
from multiprocessing import Queue

q = Queue(3)
q.put('消息1')
q.put('消息2')
print(q.full())  # False
q.put('消息3')
print(q.full())  # True

# 因为消息列队已满下面的try都会抛出异常,第一个try会等待2秒后再抛出异常,第二个Try会立刻抛出异常

try:
    q.put('消息4', True, 2)
except:
    print('消息列队已满,现有消息数量:%s'%q.qsize())

try:
    q.put_nowait('消息4')
except:
    print('消息列队已满,现有消息数量:%s'%q.qsize())

# 推荐的方式,先判断消息列队是否已满,再写入
if not q.full():
    q.put_nowait('消息4')

# 读取消息时,先判断消息列队是否为空,再读取
if not q.empty():
    for i in range(q.qsize()):
        print(q.get_nowait())
```

运行结果:

```
False
True
消息列队已满,现有消息数量:3
消息列队已满,现有消息数量:3
消息1
消息2
消息3
```

**说明**

初始化Queue()对象时(例如: q=Queue() )，若括号中没有指定最大可接收的消息数量，或数量为负值，那么就代表可接受的消息数量没有上限(直到内存的尽头) ;

- Queue.qsize(: 返回当前队列包含的消息数量;
- Queue.empty0: 如果队列为空，返回True,反之False ;
- Queue.full(): 如果队列满了，返回True,反之False;
- Queue get([block[, timeout]): 获取队列中的一条消息, 然后将其从列队中移除，block默认值为True;

1）如果block使用默认值，且没有设置timeout (单位秒)，消息列队如果为空，此时程序将被阻塞(停在读取状态)，直到从消息列队读到消息为止，如果设置了timeout，则会等待timeout秒，若还没读取到任何消息，则抛出"Queue.Empty"异常;

2）如果block值 为False,消息列队如果为空，则会立刻抛出"Queue.Empty"异常;

- Queue.get_ nowait(): 相当Queue.get(False);
- Queue.put(item,[block[, timeut]]): 将item消息写入队列，block默认值为True;

1)如果block使用默认值，且没有设置timeout (单位秒)，消息列队如果已经没有空间可写入，此时程序将被阻塞(停在写入状态)，直到从消息列队腾出空间为止，如果设置了timeout，则会等待timeout秒，若还没空间，则抛出"Queue.Full"异常;

2)如果block值为False,消息列队如果没有空间可写入，则会立刻抛出"Queue.Full"异常;

- Queue.put_ nowait(item): 相当Queue.put(item, False);

**Queue实例**

我们以Queue为例，在父进程中创建两个子进程，一个往Queue里写数据，一个从Queue里读数据:

```
from multiprocessing import Process, Queue
import os, time, random


# 写数据进程执行的代码:
def write(q):
    for value in ['A', 'B', 'C']:
        print('Put %s to queue...' % value)
        q.put(value)
        time.sleep(random.random())


# 读数据进程执行的代码:
def read(q):
    while True:
        if not q.empty():
            value = q.get(True)
            print('Get %s from queue.' % value)
            time.sleep(random.random())
        else:
            break


if __name__ == '__main__':
    # 父进程创建Queue，并传递给各个子进程:
    q = Queue()
    pw = Process(target=write, args=(q,))
    pr = Process(target=read, args=(q,))
    # 启动子进程pw，写入:
    pw.start()
    # 等待pw结束
    pw.join()
    # 启动子进程pr，读取:
    pr.start()
    pr.join()

    print('')
    print('所有数据都写入并且读完')
```

**关于concurrent.futures模块**

Python标准库为我们提供了threading和multiprocessing模块编写相应的异步多线程/多进程代码。从Python3.2开始，标准库为我们提供了concurrent. futures 模块，它提供了ThreadPoolExecutor和ProcessPoolExecutor两个类ThreadPoolExecutor和ProcessPoolExecutor继承了Executor,分别被用来创建线程池和进程池的代码。实现了对threading和multiprocessing的更高级的抽象，对编写线程池/进程池提供了直接的支持。concurrent.futures基 础模块是executor和future。

concurrent. futures模块的基础是**Exectuor**, Executor是一 个抽象类， 它不能被直接使用。但是它提供的两个子类ThreadPoolExecutor和ProcessPoolExecutor却是非常有用，顾名思义两者分别被用来创建线程池和进程池1的代码。我们可以将相应的tasks直接放入线程池/进程池,不需要维护Queue来操心死锁的问题，线程池/进程池会自动帮我们调度。

**Future**这个概念，**你可以把它理解为一个在未来完成的操作**，这是异步编程的基础，传统编程模式下比如我们操作queue.get的时候，在等待返回结果之前会产生阻塞, cpu不能让出来做其他事情，而Future的引入帮助我们在等待的这段时间可以完成其他的操作。

Executor中定义了submit() 方法，这个方法的作用是提交一个可执行的回调task，并返回一个**future实例**。future对象代表的就是给定的调用。

**submit()方法实现进程池/线程池**

#### 进程池

```
from concurrent.futures import ProcessPoolExecutor
import os, time, random


def task(n):
    print('%s is running' % os.getpid())
    time.sleep(2)
    return n**2


if __name__ == '__main__':
    p = ProcessPoolExecutor()      # 不填则默认为cpu的个数
    l = []
    start = time.time()
    for i in range(10):
        obj = p.submit(task, i)    # submit()方法返回的是一个future实例,要得到结果需要用obj.reresult()
        l.append(obj)

    p.shutdown()                   # 类似用from multiprocessing import Pool实现进程池中的close即join一起的作用
    print('='*30)
    # print([obj.result() for obj in l])
    print([obj.result() for obj in l])
    print(time.time()-start)

    # 上面的方法也可写成下面的方法
    # start = time.time()
    # with ProcessPoolExecutor() as p:  # 类似打开文件,可省去.shutdown()
    #     future_tasks = [P.submit(task, i) for i in range(10)]
    # print('=' * 30)
    # print([obj.result() for obj in future_tasks])
    # print(time.time() - start)
```

p. submit(task, i)默认为异步执行，p. submit(task, i).result()即同步执行

```
from concurrent.futures import ProcessPoolExecutor, ThreadPoolExecutor
import os, time, random


def task(n):
    print('%s is running' % os.getpid())
    time.sleep(2)
    return n**2


if __name__ == '__main__':
    p = ProcessPoolExecutor()      # 不填则默认为cpu的个数
    start = time.time()
    for i in range(10):
        res = p.submit(task, i).result()
        print(res)
    print('='*30)
    print(time.time()-start)
```

