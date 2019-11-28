## 在python中实现文本的操作

## open函数
完整的语法格式为：

`open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)`

open() 函数常用形式：

`open(file, mode='r')`

| 操作模式 | 具体含义                         |
| -------- | -------------------------------- |
| `'r'`    | 读取 （默认）                    |
| `'w'`    | 写入（会先删除之前的内容，如文件不存在，会创建）       |
| `'x'`    | 写入，如果文件已经存在会产生异常 |
| `'a'`    | 追加，将内容写入到已有文件的末尾，如文件不存在，创建新文件进行写入 |
| `'b'`    | 二进制模式                       |
| `'t'`    | 文本模式（默认）                 |
| `'+'`    | 更新（既可以读又可以写）         |

只读操作：
```python
f=open('a.txt','r',encoding='utf-8')
print(f.read())
f.close() ## 使用open函数打开文件后，需要关闭文件
```
写入操作：
```python
f=open('a.txt','w',encoding='utf-8')
f.write(str(111)+'\n') ## 一定要将写入的内容定义str 或 int。 如果不加   `'\n'` 就不会换行。这个是直接覆盖文件原先内容
f.close()
```
追加操作：
```python
f=open('a.txt','a',encoding='utf-8')
f.write(str(222))
f.close()
```

如果open函数指定的文件并不存在或者无法打开，那么将引发异常状况导致程序崩溃。为了让代码有一定的健壮性和容错性，我们可以使用Python的异常机制对可能在运行时发生状况的代码进行适当的处理，如下所示。

```python
def main():
    f = None
    try:
        f = open('a.txt', 'r', encoding='utf-8')
        print(f.read())
    except FileNotFoundError:
        print('无法打开指定的文件!')
    except LookupError:
        print('指定了未知的编码!')
    except UnicodeDecodeError:
        print('读取文件时解码错误!')
    finally:   ## 这个finally是无论如何都会执行的代码块
        if f:
            f.close()


if __name__ == '__main__':
    main()
```

> 如果并不想在最后的`open`函数后加一个`close`，使用`with`关键字就可以。

通过with关键字指定文件对象的上下文环境并在离开上下文环境时自动释放文件资源，如下所示:
```python
with open('a.txt','r') as f:
    f.read()

with open('a.txt','w') as f:
    f.write(str(111),'\n')
```
