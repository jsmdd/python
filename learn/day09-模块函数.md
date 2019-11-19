## 调用其他模块的函数
`module1.py`
```python
def foo():
    print("1")
```
`module2.py`
```python
def foo():
    print("2")
```
`test.py`
```python
import module1 as m1
import module2 as m2

m1.foo()
m2.foo()
```
　或者
`test.py`
```python
from module1 import foo
foo()

from module2 import foo
foo()
```
> 可以看出python使用函数的时候通过`import`关键字导入指定的模块是一个一个导入的，所以如果像上述代码
中写的那样，只能导入后立马调用，否则这种重名的函数会调用后导入的模块

## 如果在导入的模块中有可执行代码
`module1.py`
```python
import sys
def foo():
    print("1")

sys.exit("bye~")
```
`test.py`
```python
import module1 as m1
m1.foo()
```
> 输出结果为:
```shell
bye~
```

## 所以为避免上述情况，将执行代码放入如下所示的条件中，这样的话除非直接运行该模块，if条件下的这些代码是不会执行的，因为只有直接执行的模块的名字才是"__main__"。
`module3.py`
```python
def foo():
    pass
def bar():
    pass
#pass  为占位符，输出为空

if __name__ == '__main__':
    print('call foo()')
    foo()
    print('call bar()')
    bar()
```
`test.py`
```python
import module3 
```
> 结果为：
```shell


```

## 做个对比

`test.py`
```python
import module1 
```
> 结果为：
```shell
bye~
```
