```python
import random
import time
import os
import multiprocessing


def download(filename):
    print("开始下载%s..."%(filename))
    print("进程号为: %s"%(os.getpid()))   # getpid获取此进程的pid，windows中的方式
    use_time=random.randint(3,5)
    time.sleep(use_time)
    print("%s下载完成，耗时%ss"%(filename,use_time))


def main():
    start=time.time()
    p1=multiprocessing.Process(target=download,args=('从删库到跑路',))  
    # 在args中不加 逗号会提示单引号中的字符数量问题
    p1.start()
    p2=multiprocessing.Process(target=download,args=('从入门到放弃',))
    p2.start()
    p1.join()
    p2.join()
    end=time.time()
    print("总耗时%.2f"%(end-start))


if __name__=="__main__":
    main()
```

输出结果：
```shell
开始下载从删库到跑路...
进程号为: 7056
开始下载从入门到放弃...
进程号为: 5820
从删库到跑路下载完成，耗时4s
从入门到放弃下载完成，耗时5s
总耗时5.15
```

在上面的代码中，我们通过`Process`类创建了进程对象，通过`target`参数我们传入一个函数来表示进程启动后要执行的代码，后面的`args`是一个元组，它代表了传递给函数的参数。`Process`对象的`start`方法用来启动进程，而`join`方法表示等待进程执行结束。运行上面的代码可以明显发现两个下载任务“同时”启动了，而且程序的执行时间将大大缩短，不再是两个任务的时间总和。下面是程序的一次执行结果。
