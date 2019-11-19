## python中的函数的变量作用域

```Python
def foo():
    b = 'hello'

    # Python中可以在函数内部再定义函数
    def bar():
        c = True
        print(a)
        print(b)
        print(c)

    bar()
    # print(c)  # NameError: name 'c' is not defined


if __name__ == '__main__':
    a = 100
    # print(b)  # NameError: name 'b' is not defined
    foo()
```
1. 在`if`分支中定义了一个变量`a`，属于全局作用域，这是一个全局变量，因为它没有定义在任何一个函数中
2. 在`foo`中定义了变量`b`，属于局部作用域，在`foo`函数的外部并不能访问到它，这是一个定义在函数中的局部变量
3. 在`bar`中定义了变量`c`，属于嵌套作用域，在`bar`函数中我们是可以访问到它的，在`bar`函数之外是无法访问的
4. Python查找一个变量时会按照“局部作用域”、“嵌套作用域”、“全局作用域”和“内置作用域”的顺序进行搜索，前三者我们在上面的代码中已经看到了
>  所谓的“内置作用域”就是Python内置的那些标识符，我们之前用过的`input`、`print`、`int`等都属于内置作用域。

## 也可以通过下列所示去声明全局变量
```python
def foo():
  global a
  a=200
  
if __name__='__main__':
  a=100
  foo()
  print(a)
```

> 但是全局变量的影响太大，很可能造成变量污染，所以尽量减少全局变量的使用并且应该尽量让变量的作用域在函数的内部

说了那么多，其实结论很简单，从现在开始我们可以将Python代码按照下面的格式进行书写，这一点点的改进其实就是在我们理解了函数和作用域的基础上跨出的巨大的一步。

```Python
def main():
    # Todo: Add your code here
    pass


if __name__ == '__main__':
    main()
```
