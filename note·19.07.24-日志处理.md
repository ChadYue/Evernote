# 日志处理

## 基本概念

```
import logging

logging.basicConfig(format='%(asctime)s - %(name)s - %(levelname)s - %(message)s')

logging.debug('This is debug message')
logging.info('This is info message')
logging.warning('This is warning message')
logging.error('This is error message')
logging.critical('This is critical message')
>>>2019-07-24 13:57:06,286 - root - WARNING - This is warning message
>>>2019-07-24 13:57:06,291 - root - ERROR - This is error messa
>>>2019-07-24 13:57:06,291 - root - CRITICAL - This is critical message
```

其中，2018-06-27 15:21:37,941对应%(asctime)s，表示当前时间: root 对应%(name)s ，表示logger实例的名称，默认名称是root;WARNING对应%(levelname)s，表示日志级别(可以看到默认是WARNING,它以下的INFO和DEBUG都不显示) ; This is warning message对应%(message)s，表示用户要输出的日志内容

### 日志级别

| 级别Level                  | 对应数值 |
| -------------------------- | -------- |
| logging.NOYSET             | 0        |
| logging.DEBUG              | 10       |
| logging.INFO               | 20       |
| logging.WARNING (默认级别) | 30       |
| logging.ERROR              | 40       |
| logging.CRIYICAL           | 50       |

```
import logging
print(logging.NOTSET)
>>>0
print(logging.DEBUG)
>>>10
print(logging.INFO)
>>>20
print(logging.WARNING)
>>>30
print(logging.ERROR)
>>>40
print(logging.CRITICAL)
>>>50
```

如本文开头示例，默认日志级别是WARNING，它以下的INFO 和DEBUG都不显示。

假设设置了日志级别为INFO ，则会输出级别大于或等于INOF 的日志，而小于它的如DEBUG则不会输出:

```
import logging

logging.basicConfig(format='%(asctime)s - %(name)s - %(levelname)s - %(message)s', level=logging.INFO)

logging.debug('This is debug message')
logging.info('This is info message')
logging.warning('This is warning message')
logging.error('This is error message')
logging.critical('This is critical message')
>>>2019-07-24 14:05:33,817 - root - INFO - This is info message
>>>2019-07-24 14:05:33,817 - root - WARNING - This is warning message
>>>2019-07-24 14:05:33,817 - root - ERROR - This is error message
>>>2019-07-24 14:05:33,817 - root - CRITICAL - This is critical message
```

### Formatter

定义日志的格式,即输出的每条日志由哪几个部分组成

##### (1)常用参数

| 参数           | 含义                                            |
| -------------- | ----------------------------------------------- |
| %(message)s    | 用户自定义要输出的信息                          |
| %(asctime)s    | 当前的日期时间                                  |
| %(name)s       | logger实例的名称                                |
| %(module)s     | 使用logger实例的模块名                          |
| %(filename)s   | 使用logger实例的模块的文件名                    |
| %(funcName)s   | 使用logger实例的函数名                          |
| %(lineno)s     | 使用logger实例的代码行号                        |
| %(levelname)s  | 日志级别名称。%(levelno)s表示日志级别的数字形式 |
| %(thread)s     | 使用logger实例的线程号(测试多线程时有用)        |
| %(threadName)s | 使用logger实例的线程名称(测试多线程时有用)      |
| %(process)d    | 使用logger实例的进程号(测试多线程时有用)        |

#### (2)创建Formatter

```
formatter = logging.Formatter('%(asctime)s - %(filename)s[line:%(lineno)d] - <%(threadName)s %(thread)d>' + '- <Process %(process)d> - %(levelname)s: %(message)s')
```

### Handler

将日志输出到哪里。像本文开头示例，logging. basicconfig()默认会创建logging , streamHandler()。将日志输出到sys.stdout 标准控制台，即屏幕上。

#### 常用的Handler

**(1)logging.StreamHandler**

输出到控制台

**(2)logging.FileHandler**

输出到指定的日志文件中

**(3)logging.handlers.RotatingFileHandler**

也是输出到日志文件中，还可以指定日志文件的最大大小和副本数，当日志文件增长到设置的大小后，会先将原日志文件test.log重命名，如test.log.1,然后再创建一个test.log继续写入日志。如果设置了副本数N,则最多只能存在N个重命名的8志文件

**(4)logging.handlers.TimedRotatingFileHandler**

按日期时间保存8志文件，如果设置了滚动周期，则只存在这个周期内的8志文件。比如，只保留一周内的日志

**(5)logging.handlers.SMTPHandler** 

捕获到指定级别的日志后，给相应的邮箱发送邮件

#### 创建Handler

```
# 创建StreamHandler, 输出日志到控制台
stream_handler = logging.StreamHandler()
```

#### Handler的常用方法

- stream handler . setFormatter(formatter) :设置Handler的日志格式，参数formatter为章节1.2中的logging. Formatter实例
- stream handler . setLevel(logging.INFO) :设置Handler的日志级别

**然后，就可以将创建的Handler添加到章节1.4中的logger实例上**

### logger实例

如前面所述，直接使用logging. basicConfig()默认使用root 这个logger实例，我们也可以使用logging.getlogger()创建一个自定义命令的logger实例:

```
# 1. 创建一个叫aiotest的logger实例, 如果参数为空则返回root logger
logger = logging.getLogger('aiotest')

# 2. 设置总日志级别, 也可以给不同的handler设置不同的日志级别
logger.setLevel(logging.DEBUG)

# 3. 将Handler添加到logger实例上
logger.addHandler(stream_handler)
```



## 简单配置

### 使用默认日期时间格式, 设置日志级别

```
import logging

logging.basicConfig(format='%(asctime)s - %(name)s - %(levelname)s - %(message)s', level=logging.INFO)

logging.debug('This is debug message')
logging.info('This is info message')
logging.warning('This is warning message')
logging.error('This is error message')
logging.critical('This is critical message')
>>>2019-07-24 14:05:33,817 - root - INFO - This is info message
>>>2019-07-24 14:05:33,817 - root - WARNING - This is warning message
>>>2019-07-24 14:05:33,817 - root - ERROR - This is error message
>>>2019-07-24 14:05:33,817 - root - CRITICAL - This is critical message
```

### 使用自定义日期格式, 设置日志级别

```
import logging

logging.basicConfig(format='%(asctime)s - %(name)s - %(levelname)s - %(message)s', datefmt='%Y-%m-%d', level=logging.DEBUG)

logging.debug('This is debug message')
logging.info('This is info message')
logging.warning('This is warning message')
logging.error('This is error message')
logging.critical('This is critical message')
>>>2019-07-24 - root - DEBUG - This is debug message
>>>2019-07-24 - root - INFO - This is info message
>>>2019-07-24 - root - WARNING - This is warning message
>>>2019-07-24 - root - ERROR - This is error message
>>>2019-07-24 - root - CRITICAL - This is critical message
```

### 输出到日志文件

```
import logging

logging.basicConfig(filename='test.log', level=logging.INFO)

logging.debug('This is debug message')
logging.info('This is info message')
logging.warning('This is warning message')
logging.error('This is error message')
logging.critical('This is critical message')
INFO:root:This is info message
WARNING:root:This is warning message
ERROR:root:This is error message
CRITICAL:root:This is critical message
```

将会在当前目录下创建一个test.log日志文件, 它的内容为:

```
INFO:root:This is info message
WARNING:root:This is warning message
ERROR:root:This is error message
CRITICAL:root:This is critical message
```

## 同时输出到控制台和日志文件

创建一个.py文件

```
import os
import time
import logging

###
# 1. 创建logger实例, 如果参数为空则返回root logger
###

logger = logging.getLogger('aiotest')
# 设置总日志级别, 也可以给不同的handler设置不同的日志级别
logger.setLevel(logging.DEBUG)

###
# 2. 创建Handler, 输出日志到控制台和文件
###

# 控制台日志和日志文件使用同一个Formatter
formatter = logging.Formatter('%(asctime)s - %(filename)s[line:%(lineno)d] - <%(threadName)s %(thread)d>'
                             + '- <Process %(process)d> - %(levelname)s: %(message)s')

# 日志文件FileHandler
basedir = os.path.abspath(os.path.dirname(__file__))
log_dest = os.path.join(basedir, 'logs')  # 日志文件所在目录
if not os.path.isdir(log_dest):
    os.mkdir(log_dest)
filename = time.strftime('%Y-%m-%d-%H-%M-%S', time.localtime(time.time())) + '.log'
file_handler = logging.FileHandler(os.path.join(log_dest, filename), encoding='utf_8')
file_handler.setFormatter(formatter)
file_handler.setLevel(logging.INFO)

# 控制台日志StreamHandler
stream_handler = logging.StreamHandler()
stream_handler.setFormatter(formatter)
# stream_handler.setLevel(logging.INFO) # 单独设置控制台日志的日志级别, 注释掉则使用总日志级别

###
# 3. 将handler添加到logger中
###

logger.addHandler(file_handler)
logger.addHandler(stream_handler)
```

