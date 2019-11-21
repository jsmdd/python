```python
>>> list=['aa'*3,'bb','cc']
>>> print(list)
['aaaaaa', 'bb', 'cc']
>>> type(list)
<class 'list'>  # 表明list是列表

>>> list=['aa*3','bb','cc']
>>> print(list)
['aa*3', 'bb', 'cc']
>>> type(list)
<class 'list'>  # 表明list是列表

>>> list=['aa']*3,['bb','cc']
>>> print(list)
(['aa', 'aa', 'aa'], ['bb', 'cc'])
>>> type(list)
<class 'tuple'> # 表明list是元祖
```

> Python的元组与列表类似，不同之处在于元组的元素不能修改。
> 元组使用小括号，列表使用方括号。
> 元组创建很简单，只需要在括号中添加元素，并使用逗号隔开即可。

可以通过for循环用下标遍历，因为`range`和`list`的下标是从0开始，或者直接用列表去遍历
```python
>>> list=[1,2,3,4,5]
>>> for i in range(len(list)):
      print(list[i])
1
2
3
4
5

>>> list=[1,2,3,4,5]
>>> for i in list:
       print(i)
       
1
2
3
4
5
```
`list1.append(200)`向末位插入200，`list1.insert(1, 400)`在下标为1插入400，
`list1.extend([1000, 2000])`，`list1 += [1000, 2000]`，`list1.extend(list2)`，合并两个列表

```python
# 先通过成员运算判断元素是否在列表中，如果存在就删除该元素
if 3 in list1:
	list1.remove(3)
if 1234 in list1:
    list1.remove(1234)
print(list1) # [1, 400, 5, 7, 100, 200, 1000, 2000]
# 从指定的位置删除元素
list1.pop(0)
list1.pop(len(list1) - 1)
print(list1) # [400, 5, 7, 100, 200, 1000]
# 清空列表元素
list1.clear()
print(list1) # []
```


#### 练习1：在屏幕上显示跑马灯文字。
```python
# -*- coding=utf-8 -*-
import os
import time

def main():
    content='welcome~~'
    while True:
        os.system('cls')  ## linux中为`clear`
        print(content)
        time.sleep(0.2)
        content=content[1:] +content[0]
if __name__ == '__main__':
    main()
```

#### 练习2：随机生成验证码
```python
from random import *
import sys
def get_code(code_len=8):
    all_chars='0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
    code=''
    for _ in range(code_len):
        index=randint(0,len(all_chars)-1)
        code+=all_chars[index]
    print(code)

if __name__ == '__main__':
    get_code(int(sys.argv[1]))
```
