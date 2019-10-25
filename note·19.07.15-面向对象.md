# 面向对象

Python从设计之初就已经是一门面向对象的语言，正因为如此，在Python中创建一个类和对象是很容易的。本章节我们将详细介绍Python的面向对象编程。

如果你以前没有接触过面向对象的编程语言，那你可能需要先了解一些面向对象语言的一些基本特征，在头脑里头形成一个基本的面向对象的概念，这样有助于你更容易的学习Python的面向对象编程。

## 类和对象

#### 万物皆对象

分类是人们认识世界的-一个很自然的过程，在日常生活中会不自觉地将对象进行进行分类

**对象归类**

- 类是抽象的概念，仅仅是模板比如说:“人”
- 对象是一个你能够看得到、摸得着的具体实体:赵本山，刘德华，赵丽颖

```
user1 = 'zhangsan'
print(type(user1))
user2 = 'lisi'
print(type(user2))
>>><class 'str'>
>>><class 'str'>
```

以上str是类( python中的字符串类型)，user1和user2是对象(以前我们叫变量)

**研究对象**

顾客类型

```
属性:
姓名张浩
年龄-20
体重-60kg
行为: 
购买商品
```

收银员类型

```
属性:
员工号-10001
姓名-王淑华
部门财务部
行为:
收款
打印账单
```

#### 对象的特征一一属性

属性一一对象具有的各种特征。每个对象的每个属性都拥有特定值。例如:顾客张浩和李明的年龄、姓名不一样。

#### 对象的特征——方法(操作,行为)

方法——对象执行的操作(通常会改变属性的值)。顾客对象的方法---购买商品。收银员对象的方法----收款.

对象:用来描述客观事物的一个实体，由一组属性和方法构成

例子

```
类型:狗
对象名: doudou
属性:
颜色:白色
方法:
叫，跑，吃
```

对象同时具有属性和方法两项特性。对象的属性和方法通常被封装在一起，共同体现事物的特性，二者相辅相承，不能分割。

#### 从对象抽象出“类”

类是模子， 定义对象将会拥有的特征(属性)和行为(方法)。

**再次强调**

- 类是抽象的概念，仅仅是模板。比如说:“人”，类定义了人这种类型属性(name, age..) 和方法(study,work...).
- 对象是一个你能够看得到、摸得着的具体实体:赵本山，刘德华，赵丽颖，这些具体的人都具有人类型中定义的属性和方法，不同的是他们各自的属性不同。

根据类来创建对象被称为实例化。

## 类的定义

#### 定义只包含方法的类

在Python中要定义一个只包含方法的类，语法格式如下:

```
class 类名:
    def 方法1(self,参数列表):
        pass
    def 方法2(self,参数列表):
        pass
```

方法的定义格式和之前学习过的函数几乎-样。 区别在于第一 一个参数必须是self,大家暂时先记住，稍后介绍self。

#### 创建对象

当一个类定义完成之后，要使用这个类来创建对象，语法格式如下:

```
对象变量 = 类名()
```

第一个面向对象程序

需求:小猫爱吃鱼，小猫要喝水。

分析:

1. 定义一个猫类cat 。
2. 定义两个方法eat和drink 。

```
class Cat:
    """这是一个类:猫"""
    def eat(self):
        print('小猫爱吃鱼')
    def drink(self):
        print('小猫在喝水')
Tom = Cat()
Tom.drink()
Tom.eat()
>>>小猫在喝水
>>>小猫爱吃鱼
```

使用Cat类再创造一个对象

```
lazy_Cat = Cat()
lazy_Cat.eat()
lazy_Cat.drink()
>>>小猫爱吃鱼
>>>小猫在喝水
```

## self参数

和我们以往的经验不同，我们在调用对象的方法是不需要传递self参数，这个self参数是系统自动传递到方法里的。我们需要知道这个self到底是什么?

#### 给对象增加属性

在Python中，要给对象设置属性，非常的容易，但是不推荐使用。因为:对象属性的封装应该封装在类的内部。要给对象设置属性，只需要在类的外部的代码中直接通过.设置一个属性即可

```
tom.name = "Tom"
```

```
lazy_Cat.name = "大懒猫"
```

#### 理解self到底是什么

```
class Cat:
    """这是一个类:猫"""
    def eat(self):
        print(f'小猫爱吃鱼,我是{self.name},self的地址是{id(self)}')
    def drink(self):
        print('小猫在喝水')
Tom = Cat()
print(f'Tom的对象的id是{id(Tom)}')
Tom.name = 'Tom'
Tom.eat()
print('-'*60)
lazy_Cat = Cat()
print(f'lazy_Cat对象的id是{id(lazy_Cat)}')
lazy_Cat.name = '大懒猫'
lazy_Cat.eat()
```

```
>>>Tom的对象的id是41998544
>>>小猫爱吃鱼,我是Tom,self的地址是41998544
>>>------------------------------------------------------------
>>>lazy_Cat对象的id是41999888
>>>小猫爱吃鱼,我是大懒猫,self的地址是41999888
```

由输出可见,当我们使用

```
x对象.x方法()
```

的时候,Python会自动将x对象做为实参传给x方法的self参数.也可以这样记忆,谁点(.)的方法,self就是谁

类中的每个实例方法的第一个参数都是self

## 初始化方法init()

**之前代码存在的问题——在类的外部给对象增加属性**

- 将案例代码进行调整，先调用方法再设置属性，观察一下执行效果

```
class Cat:
    """这是一个类:猫"""
    def eat(self):
        print(f'小猫爱吃鱼,我是{self.name},self的地址是{id(self)}')
    def drink(self):
        print('小猫在喝水')
tom = Cat()
tom.drink()
tom.eat()
tom.name = 'tom'
print(tom)
```

- 程序执行报错如下:

```
AttributeError: 'Cat' object has no attribute 'name'
属性错误:'Cat'对象没有'name'属性
```

**提示**

- 在日常开发中，不推荐在**类的外部**给对象增加属性。
- 如果**在运行时，没有找到属性，程序会报错**。
- 对象应该包含有哪些属性，应该**封装在类的内部**。

**初始化方法**

- 当使用类名()创建对象时，会**自助**执行以下操作:

1. 为对象在内存中**分配空间**——创建对象(调用_ new _，以后说)
2. 为对象的属性**设置初始值**——初始化方法(调用_ init _ 并且将第一 步创建的对象，通过self参数传给     _ init _)

- 这个**初始化方法**就是 init_ 方法，一 init_ 是对象的**内置方法**(有的书也叫**魔法方法**，**特殊方法**)

_ init _ 方法是**专门**用来定义一个类**具有哪些属性并且给出这些属性的初始值的方法**!

在Cat中增加_ init _方法， 验证该方法在创建对象时会被自动调用

```
class Cat:
	"""这是一个类:猫"""
    def __init__(self):
        print('初始化方法')
```

**在初始化方法内部定义属性**

在_ init__ 方法内部使用self.属性名=属性的初始值就可以**定义属性**

定义属性之后，再使用Cat类创建的对象，都会拥有该属性

```
class Cat:
    """这是一个类:猫"""
    def __init__(self):
        print('初始化方法')
        self.name = 'tom'
    def eat(self):
        print("%s爱吃鱼"% self.name)
#使用类名()创建对象的时候,会自动调用初始化方法__init__
tom = Cat()
tom.eat()
```

**改造初始化方法——初始化的同时设置初始值**

- 在开发中，如果希望在**创建对象的同时，就设置对象的属性**，可以对_ init _ 方法进行**改造**

1. 把希望设置的属性值，定义成init_ 方法的参 数
2. 在方法内部使用self.属性 =形参接收外部传递的参数
3. 在创建对象时，使用类名(属性1， 属性2...) 调用

```
class Cat:
    """这是一个类:猫"""
    def __init__(self,name,age,color):
        print('初始化方法')
        self.name = name
        self.age = age
        self.color = color
    def eat(self):
        print("%s爱吃鱼,它%d岁了,它是一只%s的猫"% (self.name,self.age,self.color))
#使用类名()创建对象的时候,会自动调用初始化方法__init__
tom = Cat('tom',1,'blue')
tom.eat()
```

## __ str __方法

在Python中,使用print输出**对象变量**,默认情况下,会输出这个变量的类型,以及在**内存中的地址(十六进制表示)**

```
class Cat:
    """这是一个类:猫"""
    def __init__(self,new_name):
		self.name = new_name
		print("%s来了"% self.name)
tom = Cat('tom')
print(tom)
>>>tom来了
>>><__main__.Cat object at 0x00000000021CD748>
```

如果在开发中,希望使用print输出对象变量时,能够打印自定义的内容,就可以利用__ str __这个内置方法了

注意:__ str __方法必须返回一个字符串

```
class Cat:
    """这是一个类:猫"""
    def __init__(self,new_name):
		self.name = new_name
		print("%s来了"% self.name)
	def __str__(self):
		return "我是小猫: %s"% self.name
tom = Cat('tom')
print(tom)
>>>tom来了
>>>我是小猫: tom
```

## 面向对象vs面向过程

```
def CarInfo(type,price):
    print("the car's type %s,price:%d"%(type,price))
print('函数方式(面向过程)')
CarInfo('passat',250000)
CarInfo('ford',280000)

class Car:
    def __init__(self,type,price):
        self.type = type
        self.price = price

    def printCarInfo(self):
        print("the car's Info in class:type %s,price:%d"%(self.type,self.price))

print('面向对象')
carOne = Car('passat',250000)
carTwo = Car('ford',250000)
carOne.printCarInfo()
carTwo.printCarInfo()
```

输出

```
函数方式(面向过程)
the car's type passat,price:250000
the car's type ford,price:280000
面向对象
the car's Info in class:type passat,price:250000
the car's Info in class:type ford,price:250000
```

类能实现的功能,用函数也可以实现,那么类的存在还有什么特殊的意义呢?**新需求---加一个行驶里程功能**

面向过程实现

```
def CarInfo(type,price):
    print("the car's type %s,price:%d"%(type,price))

def driveDistance(oldDistance,distance):
    newDistance = oldDistance + distance
    return newDistance

print('函数方式(面向过程)')
CarInfo('passat',250000)
distance = 0
distance = driveDistance(distance,100)
distance = driveDistance(distance,200)
print(f'passat已经行驶了{distance}公里')
```

输出

```
面向过程
the car's type passat,price:250000
passat已经行驶了300公里
```

面向对象实现

```
class Car:
    def __init__(self,type,price):
        self.type = type
        self.price = price
        self.distance = 0

    def printCarInfo(self):
        print("the car's Info in class:type %s,price:%d"%(self.type,self.price))

    def driveDistance(self,distance):
        self.distance += distance

print(f'面向对象')
carOne = Car('passat',250000)
carOne.printCarInfo()
carOne.driveDistance(100)
carOne.driveDistance(200)
print(f'passat已经行驶了{carOne.distance}公里')
print(f'passat的价格是{carOne.price}')
```

输出

```
面向对象
the car's Info in class:type passat,price:250000
passat已经行驶了300公里
passat的价格是250000
```

通过对比我们可以发现:

面向对象的实现方式封装性更好，已经行驶的公里数是对象内部的属性，对象自身负责管理，外部调用
代码无需管理。我们随时可以调用对象的方法和属性得知对象当前的各种信息。而面向过程的方式而
言，外部调用代码会“手忙脚乱”
**再加一个需求:**车每行驶1公里， 车的价值贬值10元面向对象的实现方式，只需添加一 行代码:

```
def driveDistance(self,distance):
    self.distance += distance
    self.price -= distance*10
```

全部代码

```
class Car:
    def __init__(self,type,price):
        self.type = type
        self.price = price
        self.distance = 0

    def printCarInfo(self):
        print("the car's Info in class:type %s,price:%d"%(self.type,self.price))

    def driveDistance(self,distance):
        self.distance += distance
        self.price -= distance * 10

print(f'面向对象')
carOne = Car('passat',250000)
carOne.printCarInfo()
carOne.driveDistance(100)
carOne.driveDistance(200)
print(f'passat已经行驶了{carOne.distance}公里')
print(f'passat的价格是{carOne.price}')
```

输出

```
面向对象
the car's Info in class:type passat,price:250000
passat已经行驶了300公里
passat的价格是247000
```

面向过程实现

```
def CarInfo(type,price):
    print("the car's type %s,price:%d"%(type,price))
    return price

def driveDistance(oldDistance,distance):
    newDistance = oldDistance + distance
    return newDistance

def oldprice(price,distance):
    price -= distance*10
    return price

print('函数方式(面向过程)')
price = CarInfo('passat',250000)
distance = 0
distance = driveDistance(distance,100)
distance = driveDistance(distance,200)
price = oldprice(price,distance)
print(f'passat已经行驶了{distance}公里')
print(f'passat的价格是{price}')
```

输出

```
面向过程
the car's type passat,price:250000
passat已经行驶了300公里
passat的价格是247000
```

**小结可以拿公司运营作为比喻来说明面向对象开发方式的优点**
	外部调用代码好比老板面向过程中函数好比员工，让员工完成一个任务，需要老板不断的干涉,大大影
响了老板的工作效率。面向对象中对象好比员工，让员工完成-一个任务，老板只要下命令即可，员工可
以独挡一面，大大节省了老板的时间。
**还有一一种说法**
世界上本没有类， 代码写多了，也就有了类
面向对象开发方式是晚于面向过程方式出现的，几十年前，面向对象还没有出现以前，很多软件系统的代码量就已经达到几十上百万行，科学家为了组织这些代码，将各种关系密切的数据，和相关的方法分门别类，放到一起管理，就形成了面向对象的开发思想和编程语言语法。

## 私有属性---封装

在实际开发中，对象的某些属性或方法可能只希望在对象的内部被使用，而不希望在外部被访问到

**定义方式**

在定义属性或方法时，在属性名或者方法名前增加两个下划线__实际开发中私有属性也不是一层不变
的。所以要给私有属性提供外部能够操作的方法。

**通过自定义get,set方法提供私有属性的访问**

```
class Person:
    def __init__(self,name,age):
        self.name = name
        self.__age = age
    #定义对私有属性的get方法,获取私有属性
    def getAge(self):
        return self.__age
    #定义对私有属性的重新赋值的set方法,重置私有属性
    def setAge(self,age):
        self.__age = age

person1 = Person('tom',19)
person1.setAge(20)
print(person1.name,person1.getAge())
>>>tom 20
```

**使用property标注提供私有属性的访问**

```
class Teacher:
    def __init__(self,name,age,speak):
        self.name = name
        self.__age = age
        self.__speak = speak

    @property #注意1. @proterty下面默认跟的是get方法,如果设置成set会报错。
    def age(self):
        return self.__age

    @age.setter #注意2.这里是使用的上面函数名. setter,不是property. setter.
    def age(self,age):
        if age > 150 and age <= 0: #还可以在setter方法里增加判断条件
            print('年龄输入有误!')
        else:
            self.__age = age

    @property
    def for_speak(self): #注意3.这个同名函数名可以自定义名称，一般都是默认使用属性名。
        return self.__speak

    @for_speak.setter
    def for_speak(self,speak):
        self.__speak = speak

t1 = Teacher("herry",45,"Chinese")
t1.age = 38 #注意4.有了property后，直接使用t1. age ,而不是t1. age()方法了。
t1.for_speak = 'English'
print(t1.name,t1.age,t1.for_speak) #herry 38 English
>>>herry 38 English
```

## 将实例用作属性---对象组合

使用代码模拟实物时，你可能会发现自己给类添加的细节越来越多:属性和方法清单以及文件都越来越长。
在这种情况下，可能需要将类的一部分属性和方法作为一个独立的类提取出来。你可以将大型类拆分成多
协同工作的小类。

#### 实例1摆放家具

**需求**

1. 房子(House)有户型、总面积和家具名称列表

   ​	新房子没有任何家具

2. 家具(HouseItem)有名字和占地面积，其中

   ​	席梦思(bed)占地4平米

   ​	衣柜(chest)占地2平米

   ​	餐桌(table)占地1.5平米

3. 将以上三件家具添加到房子中

4. 打印房子时，要求输出:户型、总面积、剩余面积、家具名称列表

**剩余面积**

1. 在创建房子对象时，定义一个剩余面积的属性，初始值和总面积相等
2. 当调用add_ item方法，向房间添加家具时，让剩余面积-=家具面积

## 类属性类方法静态方法

#### 类对象，实例对象

类对象:类名实例对象:类创建的对象

类属性就是类对像所拥有的属性，它被所有类对象的实例对象所共有，在内存中只存在一一个副本，这个和
C++、Java中类的静态成员变量有点类似。对于公有的类属性，在类外可以通过类对象和实例对象访问

```
# 类属性
class people:
    name = "Tom"    #公有的类属性
    __age = 18      #私有的类属性

p = people
print(p.name)       #实例对象
print(people.name)  #类对象

# print(p.__age)      #错误不能在类外通过实例对象访问私有的类属性
# print(people.__age) #错误不能在类外同过类对象访问私有的类属性
```

实例属性

```
class People:
    name = "Tom"


p = People()
p.age = 18

print(p.name)
print(p.age)         # 实例属性是实例对象特有的.类对象不能拥有

print(People.name)   
# print(People.age)  # 错误:实例属性,不能通过类对象调用
```

我们经常将实例属性放在构造方法中

```
class People:
    name = "Tom"
    
    def __init__(self, age):
        self.age = age


p = People(18)

print(p.name)
print(p.age)         # 实例属性是实例对象特有的.类对象不能拥有

print(People.name)
# print(People.age)  # 错误:实例属性,不能通过类对象调用
```

类属性和实例属性混合

```
class People:
    name = "Tom"     # 类属性:实例对象和类对象可以同时调用

    def __init__(self, age):  # 实例属性
        self.age = age


p = People(18)  # 实例对象
p.sex = '男'    # 实例属性

print(p.name)
print(p.age)         # 实例属性是实例对象特有的.类对象不能拥有
print(p.sex)

print(People.name)   # 类对象
# print(People.age)  # 错误:实例属性,不能通过类对象调用
# print(People.sex)  # 错误:实例属性,不能通过类对象调用
```

如果在类外修改类属性，必须通过类对象去引用然后进行修改。如果通过实例对象去引用，会产生一个同名
的实例属性，这种方式修改的是实例属性，不会影响到类属性，并且如果通过实例对象引用该名称的属性,
实例属性会强制屏蔽掉类属性，即引用的是实例属性，除非删除了该实例属性

```
class Animal:
    name = "Panda"   # 类属性:实例对象和类对象可以同时调用


print(Animal.name)   # 类对象引用类属性
p = Animal()
print(p.name)        # 实例对象引用类属性时,会产生一个同名的实例属性
p.name = 'dog'       # 修改的只是实例属性的,不会影响到类属性
print(p.name)        # dog
print(Animal.name)   # panda

# 删除实例属性
del p.name
print(p.name)
```

#### 类属性的应用场景

比如，我们有一-个班级类，创建班级对象的时候，需要按序号指定班级名称，我们就需要知道当前已经创建
了多少个班级对象，这个数量可以设计成类属性

```
class NeuEduClass:
    class_num = 0

    def __init__(self):
        self.class_name = f'东软睿道Python{NeuEduClass.class_num+1}班'
        NeuEduClass.class_num += 1


classList = [NeuEduClass() for i in range(10)]
for c in classList:
    print(c.class_name)
```

输出

```
东软睿道Python1班
东软睿道Python2班
东软睿道Python3班
东软睿道Python4班
东软睿道Python5班
东软睿道Python6班
东软睿道Python7班
东软睿道Python8班
东软睿道Python9班
东软睿道Python10班
```

#### 类方法

类对象所拥有的方法，需要用修饰器@classmethod 来标识其为类方法，对于类方法，第一个参数必须是类对象，一般以cls作为第一个参数(当然可以用其他名称的变量作为其第一个参数， 但是大部分人都习惯以"cls’作为第一个参数的名字) ，能够通过实例对象和类对象去访问。

```
class People:
    country = "China"

    @classmethod
    def getcountry(cls):
        return cls.country


p = People()
print(p.getcountry())       # 实例对象调用类方法
print(People.getcountry())  # 类对象调用类方法
```

类方法还有一个用途就是可以对类属性进行修改:

```
class People:
    country = "China"

    @classmethod
    def getcountry(cls):
        return cls.country

    @classmethod
    def setcountry(cls, country):
        cls.country = country


p = People()
print(p.getcountry())       # 实例对象调用类方法
print(People.getcountry())  # 类对象调用类方法

p.setcountry('Japan')

print(p.getcountry())
print(People.getcountry())
```

#### 静态方法

需要通过修饰器@staticmethod 来进行修饰，静态方法不需要定义参数

```
class People3:
    country = "China"

    @staticmethod
    def getcountry():
        return People3.country
        

p = People3()
print(p.getcountry())        # 实例对象调用类方法
print(People3.getcountry())  # 类对象调用类方法
```

## 继承

继承的概念:子类自动拥有(继承)父类的所有方法和属性1)继承的语法

```
class类名(父类名):
pass
```

- 子类继承自父类，可以直接享受父类中已经封装好的方法，不需要再次开发
- 子类中应该根据职责，封装子类特有的属性和方法
- 当父类的方法实现不能满足子类需求时，可以对方法进行重写(override)

举一个常见的例子。Circle 和Rectangle，不同的图形，面积(area)计算方式不同。

```
import math
class Circle:
    def __init__(self,color,r):
        self.r = r
        self.color = color

    def area(self):
        return math.pi*self.r*self.r

    def show_color(self):
        print(self.color)

class Rectangle:
    def __init__(self,color,a,b):
        self.color = color
        self.a,self.b = a,b

    def area(self):
        return self.a * self.b

    def show_color(self):
        print(self.color)

circle = Circle('red',3.0)
print(circle.area())
circle.show_color()
rectangle = Rectangle('blue',2.0,3.0)
print(rectangle.area())
rectangle.show_color()
>>>28.274333882308138
>>>red
>>>6.0
>>>blue
```

我们看到Rectangle和Circle有同样的属性color和方法showcolor我们可以定义一个父类Shape, 将Rectangle
和Circle通用的部分提取到Shape类中，然后在子类的init方法中，通过调用super0_ init_ (color). 把color
传给父类的__ init \ ()

```
import math
class Shape:
    def __init__(self,color):
        self.color =color

    def area(self):
        return None

    def show_color(self):
        print(self.color)

class Circle(Shape):
    def __init__(self,color,r):
        super().__init__(color)
        self.r = r

    def area(self):
        return math.pi * self.r * self.r

class Rectangle(Shape):
    def __init__(self,color,a,b):
        super().__init__(color)
        self.a,self.b = a,b

    def area(self):
        return self.a * self.b

circle = Circle('red',3.0)
print(circle.area())
circle.show_color()
rectangle = Rectangle('blue',2.0,3.0)
print(rectangle.area())
rectangle.show_color()
>>>28.274333882308138
>>>red
>>>6.0
>>>blue      
      
```

子类Circle和Rectangle本身并没有定义show_ color方法， 从父类Shape继承了show_ .color方法。 子类Circle和Rectangle改写(Override)了父类的area方法，分别提供了自己不同的实现。

注释掉Circle类中init方法中super(0._ init_ 0这行代码:

```
class Circle(Shape):
    def __init__(self,color,r):
        # super().__init__(color)
        self.r = r
```

再次运行代码，报错:

```
	print(self.color)
AttributeError: 'Circle' object has no attribute 'color'
```

错误输出指定的出错位置在: print(self.color) ，说Circle类 型对象没有color属性

```
class Shape:
	def show_color(self):
    	print(self.color)
```

问题原因是，Circle类型重写了父类Shape的_ init_ 0)方法，导致父类Shape的__ init\0方法没 有被调用到，

所以**一定不要忘记在子类的init方法中调用super().__ init __()**

## _ new _ 方法

python中定义的类在创建实例对象的时候，会自动执行**init()**方法，但是在执行**init()**方法之前，会执行
**new()**方法。

__ new _()_的作用主要有两个。

​	1.在内存中为对象分配空间

​	2.返回对象的引用。(即 对象的内存地址)

python解释器在获得引用的时候会将其传递给**init()**方法中的self。

```
class A:
    def __new__(cls, *args, **kwargs):
        print('__new__')
        #return super().__new__(cls)  # 这里一定要返回,否则__init__()方法不会被执行

    def __init__(self):  # 这里的self就是new方法中的return返回值
        print('__init__')

a = A()
```

输出结果

```
__new__
__init__
```

我们一定要在__ new __方法中最后调用

```
return super().__new__(cls)
```

否则init方法不会被调用

```
class A:
    def __new__(cls, *args, **kwargs):
        print('__new__')
        # return super().__new__(cls)  # 这里一定要返回,否则__init__()方法不会被执行

	def __init__(self):  # 这里的self就是new方法中的return返回值
    	print('__init__')

a = A()
```

输出

```
__new__
```

像以前一样,我们不写_ new _方法试试

```
class A:
    # def __new__(cls, *args, **kwargs):
        # print('__new__')
        # return super().__new__(cls)  # 这里一定要返回,否则__init__()方法不会被执行

	def __init__(self):  # 这里的self就是new方法中的return返回值
    	print('__init__')

a = A()
```

输出

```
__init__
```

##  object---所有python类型的父类

在Python中，所有类型有个隐式的父类( object ),上面的代码相当于

```
class A(object):
    # def __new__(cls, *args, **kwargs):
        # print('__new__')
        # return super().__new__(cls)  # 这里一定要返回,否则__init__()方法不会被执行

    def __init__(self):  # 这里的self就是new方法中的return返回值
        print('__init__')


a = A()
```

当我们的类中没有定义_ new _ 方法时,创建对象时,Python会先调用父类(object) 的_ new _ 方法,在内存中创建一个实例,然后传递给我们的init方法.如果我们的自定义类型定义了 _ new _ 方法,就会覆盖父类(object)的 _ new\方法 (父类的 _ new\ 方法不会被自动调用)，所以我们要显式调用父类(object)的 _new\方法， 在内存中创建一个实例。

那么new有什么作用呢?我们可以改写它，举个例子，就比如说单例模式。

## 单例模式

如果我们创建两个实例: 

```
a1 = A()
a2 = A()
```

那么id(a1)和id(a2)的值不一样，也就是说python在内容当中创建了两个实例对象，用了两份内存。同样的东
西创建了两份

如果想不管创建多少个实例对象，我们都让它的id是一样的。

也就是说，先创建一个实例对象， 之后不管创建多少个，返回的永远都是第一个实例对象的内存地址。可以
这样实现:

```
# 重写new方法很固定，返可值必须是这个
# 这样就避免了创建多份。
# 创建第一个实例的时候，_instance是None, 那么会分配空间创建实例。
# 此时的类属性已经被修改，_instance不再为None
# 那么当之后实例属性被创建的时候，由于_instance不为None。
# 则返回第一个实例对象的引用，即内存地址。
# 这样就应用了单例模式。
class A:
    _instance = None
    def __new__(cls, *args, **kwargs):
        if A._instance == None:
            A._instance = super().__new__(cls)
        return A._instance


a1 = A()
print(id(a1))
a2 = A()
print(id(a2))
```