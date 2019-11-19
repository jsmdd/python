## 在python中使用`def`定义函数，类似于shell中的函数，但是使用方法不同
```python
def factorial(num):
    result=1
    for i in range(1,num+1):
        result*=i
    return result
```
1. 首先在上述函数`factorial`中有一个需要传参的变量`num`,此变量并不说明传入变量名要为`num`
2. 其次函数中`return`用来返回结果，可以是上述函数中所表达的结果，也可以是任意值
```python
m = int(input())
print(factorial(m))
```
> 上述函数可以用`math`中的`factorial`表示
```python
from math import *
m=5
print(factorial(m))  
```

3. 也可以在定义函数时设置默认值，也可以使用可变参数
```Python
from random import randint

def roll_dice(n=2):
    """摇色子"""
    total = 0
    for i in range(n):
        total += randint(1, 6)
    return total

def add(a=0, b=0, c=0):
    """三个数相加"""
    return a + b + c

def bdd(*args):
    """*代表任意"""
    total=0
    for i in args:
        total+=i
    return total

# 如果没有指定参数那么使用默认值摇两颗色子
print(roll_dice())
# 摇三颗色子
print(roll_dice(n=3))
print(roll_dice(3))
print(add())
print(add(1))
print(add(1, 2))
print(add(1, 2, 3))
# 传递参数时可以不按照设定的顺序进行传递
print(add(c=50, a=100, b=200))
# 可以随意传入相应数量的参数
print(bdd(1,2))
print(bdd(1,2,3,4))
```

