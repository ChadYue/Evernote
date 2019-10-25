# 循环语句

- while循环：在给定的判断条件为 true 时执行循环体，否则退出循环体
- for循环：重复执行语句
- 嵌套循环：你可以在while循环体中嵌套for循环

循环基本四大要素：条件、循环体(语句块)、改变循环变量(使循环不是死循环)、循环变量初始化

### while循环

while 条件:
    语句块(条件满足就执行，
        执行完就又回到while后面的条件继续判断，
        如果条件还满足就继续执行此语句块，
        如果条件不满足就结束while循环)

```
count = 1
sum = 0
while count <= 100:
    sum += count
    count += 1
print(sum)
>>>5050
```

循环变量初始化
while 条件：
    循环体
    改变循环变量的值(使循环正常退出)

### for循环

for item in items:

​	取出item里面的数据

```
for item in "www.neuedu.com":
    print(item)
>>>w
>>>w
>>>w
>>>.
>>>n
>>>e
>>>u
>>>e
>>>d
>>>u
>>>.
>>>c
>>>o
>>>m
```

### 嵌套循环

```
for num in range(10,21):                # 迭代10 到 20之间的数字
    for i in range(2,num):              # 根据因子迭代
        if num %i == 0:                 # 确定第一个因子
            j = num/i                   # 计算第二个因子
            print('%d 是一个合数'% num)
            break                       # 跳出当前循环
    	else:                               # 循环的else部分
        print('%d 是一个质数'% num)
>>>10 是一个合数
>>>11 是一个质数
>>>12 是一个合数
>>>13 是一个质数
>>>14 是一个合数
>>>15 是一个合数
>>>16 是一个合数
>>>17 是一个质数
>>>18 是一个合数
>>>19 是一个质数
>>>20 是一个合数
```

## 循环控制语句

- break：在语句块执行过程中终止循环，并且跳出整个循环（只能存在与循环体内）
- continue：在语句块执行过程中终止当前循环，跳出该次循环，执行下一次循环
- pass：pass是空语句，是为了保持程序结构的完整性

### break语句

当循环遇到break就停止循环，继续循环下面的语句块（只能存在与循环体内）

```
count = 1
sum = 0
while count <= 100:
    sum += count
    if sum > 1000: # 当sum大于1000时结束循环
        break
    count += 1
print(sum)
print(count)
>>>1035
>>>45
```

### continue

结束本层的本次循环，继续执行下一次的循环

```
count = 1
sum = 0
while count <= 100:
    if count %2 == 0:  # 偶数时跳过输出
        count += 1
        continue
    sum = sum + count1
    count += 1
print(sum)
print(count)
>>>2500
>>>101
```