## 与大多数语言相同 
```
if 条件1:
  xxxxx
elif 条件2:
  xxxxx
else:
  xxxxx
print(xxxx)
```

> 可以查阅一下 ```from random import randit``` 与```import random```的区别，以及random和math函数

## random函数
> https://www.cnblogs.com/chamie/p/4917820.html
```
from random import *
list=[1,2,3,4,5,6,7]
a=sample(list,3)
print(a)

b=random()
print(b)

c=uniform(18,8)
d=int(c)
print(c)
print(d)

e=randint(8,18)
print(e)

f=randrange(0,100,5)
print(f)
```
> random()方法：返回随机生成的一个实数，它在[0,1)范围内

> random.random()方法用于生成一个0到1的随机浮点数：0<=n<1.0

> random.uniform(a,b)：用于生成一个指定范围内的随机浮点数，两格参数中，其中一个是上限，一个是下限。如果a>b，则生成的随机数n，即b<=n<=a；如果a>b，则a<=n<=b。

> random.randint(a,b)：用于生成一个指定范围内的整数。其中参数a是下限，参数b是上限，生成的随机数n：a<=n<=b

> random.randrange([start],stop[, step])：从指定范围内，按指定基数递增的集合中获取一个随机数。如：random.randrange(10,100,2)，结果相当于从[10,12,14,16,...,96,98]序列中获取一个随机数。

> random.choice(sequence)：参数sequence表示一个有序类型。sequence在python不是一种特定的类型，而是泛指一系列的类型。list，tuple，字符串都属于sequence。
```
>>> import random
>>> print random.choice("学习python")
t
>>> print random.choice(["JGood","is","a","handsome","body"])
is
>>> print random.choice(("Tuple","list","Dict"))
list
```

> random.shuffle(x[, random])：用于将一个列表中的元素打乱。
```
>>> import random
>>> p=["pyhton","is","powerful","simple","and so on..."]
>>> random.shuffle(p)
>>> p
['and so on...', 'simple', 'powerful', 'pyhton', 'is']
```

> random.sample(sequence,k)：从指定序列中随机获取指定长度的片段，sample函数不会修改原有序列。(是一个个随机抽取)
