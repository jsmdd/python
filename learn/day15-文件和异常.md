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

通过open函数向另一个文件按行写入另一个文件：
```python
import time,os


def test():
    try:
        with open('13.py','r',encoding='utf-8') as f1:
            for i in f1:
                print(i,end='')
                time.sleep(0.5)
                with open('49.py','a',encoding='utf-8') as f2:
                    f2.write(str(i))
        print()
    finally:
        if os.path.exists('49.py'):  # 通过判断这个文件路径是否存在
            print('输出完成!')
        else:
            print('输出错误!')


if __name__=='__main__':
    test()
```
> 此处加一个知识点：如何用python判断一个文件或者路径是否存在

### os模块
使用os.access()方法判断文件是否可进行读写操作。

语法：
`os.access(path, mode)`

path为文件路径，mode为操作模式，有这么几种:

1. os.F_OK: 检查文件是否存在;
2. os.R_OK: 检查文件是否可读;
3. os.W_OK: 检查文件是否可以写入;
4. os.X_OK: 检查文件是否可以执行 

示例：
```python
        if os.access('49.py',os.F_OK):
            print('输出完成!')
        else:
            print('输出错误!')
```

### 使用Try语句
如果你open的文件不存在，程序会抛出错误，使用try语句来捕获这个错误。

示例：
```python
try:
    f.open()
    f.close()
except IOError:
    print "File is not accessible."
```


### 使用pathlib模块

使用pathlib需要先使用文件路径来创建path对象。此路径可以是文件名或目录路径。

示例:
```python
        if pathlib.Path('49.py'):
            print('输出完成!')
        else:
            print('输出错误!')
```
- 检查路径是否存在
```python
path = pathlib.Path("path/file")
path.exist()
```
- 检查路径是否是文件
```python
path = pathlib.Path("path/file")
path.is_file()
```

## 读写二进制文件

知道了如何读写文本文件要读写二进制文件也就很简单了，下面的代码实现了复制图片文件的功能。

```python
def main():
    assert ('linux' in sys.platform)  # 用来判断执行此脚本的环境是否是linux环境
    try:
        with open('guido.jpg', 'rb') as fs1:
            data = fs1.read()
            print(type(data))  # <class 'bytes'>
        with open('吉多.jpg', 'wb') as fs2:
            fs2.write(data)
    except FileNotFoundError as e:
        print('指定的文件无法打开.')
    except IOError as e:
        print('读写文件时出现错误.')
    print('程序执行结束.')


if __name__ == '__main__':
    main()
```
> 用于判断一个表达式，在表达式条件为 false 的时候触发异常。断言可以在条件不满足程序运行的情况下直接返回错误，而不必等待程序运行后出现崩溃的情况


## 读写JSON文件

`json`模块
写
```python
import json


def main():
    mydict = {
        'name': '骆昊',
        'age': 38,
        'qq': 957658,
        'friends': ['王大锤', '白元芳'],
        'cars': [
            {'brand': 'BYD', 'max_speed': 180},
            {'brand': 'Audi', 'max_speed': 280},
            {'brand': 'Benz', 'max_speed': 320}
        ]
    }
    try:
        with open('data.json', 'w', encoding='utf-8') as fs:
            json.dump(mydict, fs)
    except IOError as e:
        print(e)
    print('保存数据完成!')


if __name__ == '__main__':
    main()
```
读
```python
import json


def main():
    try:
        with open('data.json','r',encoding='utf-8') as f:
            print(json.load(f))
    except IOError as es:
        print(es)
    print('successlly')

if __name__=='__main__':
    main()
```

- `dump` - 将Python对象按照JSON格式写入到文件中
- `dumps` - 将Python对象处理成JSON格式的字符串
- `load` - 将文件中的JSON数据读取成python对象
- `loads` - 将字符串的内容读取成Python对象

json.dump和json.load是python和文件的交互操作。
