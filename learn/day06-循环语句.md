## for语句
> `for-in`循环
```
for i in range(100) #代表从0~99
for i in range(1,101,2) #代表从1~100的奇数
```

## while语句
> `while`循环
- 
```
a=0
for i in range(2,101,2):
    #if i%2==0:
    while i%2==0:  # 等效于if判断
        a+=i
        break   # 代表结束本次while循环
        #exit(1) # 代表退出脚本
print(a)
```
- `while`共有`break`和`contiue`以及`exit(1)`

- 需要注意的是`break`只能终止它所在的那个循环

- `continue`用来放弃本次循环后续的代码直接让循环进入下一轮

- `exit(1)`用来退出整个脚本

```
# 可以较好理解分支和循环
a=0
for i in range(1,101):
    while True:
        if i%2==1:
            a+=i
            print(a)
        elif i%5==0:
            a-=i
            print(a)
        else:
            a=a
            print(a)
        break
print(a)
```
```
# 判断输入数字是否为素数
from  math import *
num = int(input())
end = int(sqrt(num))
is_prime = True
for i in range(2,end + 1):
    if num%i==0:
        is_prime = False
        break
if is_prime and num != 1:
    print("%d"%(num),"yes")
else:
    print("no")
```
