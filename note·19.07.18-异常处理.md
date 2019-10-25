# 异常处理

### 异常的概念

- 程序在运行时，如果Python解释器**遇到**到一个错误，**会停止程序的执行**，**并且提示一 些错误信息**，这就是**异常**
- **程序停止执行并且提示错误信息**这个动作，我们通常称之为:**抛出(raise)异常**

*程序开发时，很难将**所有的特殊情况**都处理的面面俱到，通过**异常捕获**可以针对突发事件做集中的处理，从而保证程序的**稳定性和健壮性***

一段代码

```
num = int(input('请输入数字:'))
print('hello')
```

如果我们输入非数字,输出:

```
请输入数字:s
Traceback (most recent call last):
  File "F:/ch07-18/Demo01·19.07.18.py", line 1, in <module>
    num = int(input('请输入数字:'))
ValueError: invalid literal for int() with base 10: 's'
```

1.发生错误 2.程序终止 ---hello没有输出

### 捕获异常

##### 简单的捕获异常语法

- 在程序开发中，如果**对某些代码的执行不能确定是否正确**，可以增加try(尝试) 来**捕获异常**
- 捕获异常最简单的语法格式:

```
try:
尝试执行的代码
except:
出现错误的处理
```

- try**尝试**，下方编写要尝试代码，不确定是否能够正常执行的代码
- except **如果不是**，下方编写尝试失败的代码

**简单异常捕获演练- --要求用户输入整数**

```
try:
    # 提示用户输入一个数字
    num = int(input('请输入数字:'))
except:
    print('请输入正确的数字')

print('hello')
```

输入非数字:

```
请输入数字:s
请输入正确的数字
hello
```

程序没有终止,输出了hello

##### 错误类型捕获

- 在程序执行时，可能会遇到**不同类型的异常**，并且需要**针对不同类型的异常，做出不同的响应**，这个时候，就需要捕获错误类型了
- 语法如下:

```
try:
	# 尝试执行的代码
	pass
except错误类型1:
	# 针对错误类型1,对应的代码处理
	pass
except (错误类型2,错误类型3):
	# 针对错误类型2和3,对应的代码处理
	pass
except Exception as result:
	print(“未知错误%s" % result)
```

- 当python解释器**抛出异常**时，**最后一行错误信息的第一 个单词，就是错误类型**

**异常类型捕获演练-一要求用户输入整数**

**需求**

1. 提示用户输入一个整数
2. 使用8除以用户输入的整数并且输出

```
try:
    num = int(input('请输入整数:'))
    result = 8 / num
    print(result)
except ValueError:
    print('请输入正确的整数!')
except ZeroDivisionError:
    print('除数不能为零!')
```

**捕获未知错误**

- 在开发时，**要预判到所有可能出现的错误**，还是有一 定难度的
- 如果希望程序**无论出现任何错误**，都不会因为Python 解释器**抛出异常而被终止**，可以再增加一一个except

语法如下:

```
except Exception as result:
    print('未知错误 %s' % result)
```

##### 异常捕狄元整语法

- 在实际开发中，为了能够处理复杂的异常情况，完整的异常语法如下:

提示:

- 有关完整语法的应用场景，在后续学习中，**结合实际的案例**会更好理解
- 现在先对这个语法结构有个印象即可

```
try:
	# 尝试执行的代码
	pass
except错误类型1:
	# 针对错误类型1,对应的代码处理
	pass
except错误类型2:
	# 针对错误类型2,对应的代码处理
	pass
except (错误类型3,错误类型4):
	# 针对错误类型3和4,对应的代码处理
	pass
except Exception as result:
	# 打印错误信息
	print(“未知错误%s" % result)
else:
	# 没有异常才会执行的代码
	pass
finally:
	# 无论是否有异常,都会执行的代码
	print('无论是否有异常,都会执行的代码')
```

- else只有在没有异常时才会执行的代码
- finally无论是否有异常，都会执行的代码
- 之前一个演练的**完整捕获异常**的代码如下:

```
try:
    num = int(input('请输入整数:'))
    result = 8 / num
    print(result)
except ValueError:
    print('请输入正确的整数!')
except ZeroDivisionError:
    print('除数不能为零!')
except Exception as result:
    print('未知错误 %s' % result)
else:
    print('正常执行')
finally:
    print('执行完成,但是不保证正确')
```

### 异常的传递

- **异常的传递**--当**函数/方法**执行**出现异常**，会**将异常传递**给函数/方法的**调用一方**
- 如果**传递到主程序**，仍然**没有异常处理**，程序才会被终止

提示

- 在开发中，可以在主函数中增加**异常捕获**
- 而在主函数中调用的其他函数，只要出现异常，都会传递到主函数的**异常捕获**中
- 这样就不需要在代码中，增加大量的**异常捕获**，能够保证代码的整洁

**需求**

1. 定义函数demo1() **提示用户输入一个整数并且返回**
2. 定义函数demo2() 调用demo1()
3. 在主程序中调用demo2()

```
def demo1():
    return int(input('请输入一个整数:'))

def demo2():
    return demo1()

try:
    print(demo2())
except ValueError:
    print('请输入正确的整数:')
except Exception as result:
    print('未知错误 %s'% result)
```

### 抛出raise异常

##### 应用场景

- 在开发中，除了**代码执行出错**Python 解释器会**抛出**异常之外
- 还可以根据**应用程序特有的业务需求主动抛出异常**

示例

- 提示用户**输入密码**，如果**长度少于8**,抛出**异常**

注意

- 当前函数**只负责**提示用户输入密码，如果**密码长度不正确，需要其他的函数进行额外处理**
- 因此可以**抛出异常**，由其他需要处理的函数**捕获异常**

##### 抛出异常

- Python 中提供了一个Exception **异常类**
- 在开发时，如果满足**特定业务需求时**,希望**抛出异常**，可以:

1. **创建**一个Exception 的**对象**
2. 使用raise**关键字**抛出**异常对象**

**需求**

- 定义input_ password 函数，提示用户输入密码
- 如果用户输入长度<8,抛出异常
- 如果用户输入长度>=8,返回输入的密码

```
def input_password():

    # 1\. 提示用户输入密码
    pwd = input('请输入密码:')

    # 2\. 判断密码长度,如果长度 >= 8,返回用户输入的密码
    if len(pwd) >= 8:
        return pwd

    # 3\. 密码长度不够,需要抛出异常
    # 1> 创建异常对象 - 使用异常的错误信息字符串作为参数
    ex = Exception('密码长度不够')

    # 2> 抛出异常对象
    raise ex

try:
    user_pwd = input_password()
    print(user_pwd)
except Exception as result:
    print('发现错误: %s'% result)
```

### 自定义异常

自定义异常主要是自己定义的异常类，对异常进行分门别类管理，自定义异常需要继承异常父类Exception一个例子

```
class MyException(Exception):           # 让MyException类继承Exception
    def __init__(self, name, age):
        self.name = name
        self.age = age


try:
    # 知识点:主动抛出异常,就是实例化一个异常类
    raise MyException('zhansgan', 19)   # 实例化一个异常,实例化的时候需要传参数
except MyException as obj:              # 这里体现一个封装,
    print(obj.age, obj.name)            # 捕获的就是MyException类携带过来的信息
except Exception as obj:                # 万能捕获,之前的可能捕获不到,这里添加Exception作为保底
    print(obj)
```

