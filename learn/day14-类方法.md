Python可以在类中定义类方法，类方法的第一个参数约定名为cls，它代表的是当前类相关的信息的对象
```python
import time
import os

class Clock(object):

    def __init__(self,hour=0,minute=0,sencond=0):
        self.hour=hour
        self.minute=minute
        self.sencond=sencond

    @classmethod   #定义类方法
    def now(cls):
        ctime=time.localtime(time.time())
        return cls(ctime.tm_hour,ctime.tm_min,ctime.tm_sec)  # 获取系统时间

    def run(self):
        print('%02d:%02d:%02d'%(self.hour,self.minute,self.sencond))
        self.sencond+=1
        if self.sencond==60:
            self.sencond=0
            self.minute+=1
        if self.minute==60:
            self.minute=0
            self.hour+=1
        if self.hour==24:
            self.hour=0

def main():
    clock=Clock.now()  # 通过类方法创建对象并获取系统时间
    while True:
        os.system('cls')
        clock.run()
        time.sleep(1)


if __name__=='__main__':
    main()
```

### 这里顺便介绍`time`函数
> 元组（struct_time）方式：struct_time元组共有9个元素，返回struct_time的函数主要有gmtime()，localtime()，strptime()

1. time.localtime([secs])：将一个时间戳转换为当前时区的struct_time。secs参数未提供，则以当前时间为准。
```python
>>> time.localtime()
time.struct_time(tm_year=2011, tm_mon=5, tm_mday=5, tm_hour=14, tm_min=14, tm_sec=50, tm_wday=3, tm_yday=125, tm_isdst=0)
>>> time.localtime(1304575584.1361799)
time.struct_time(tm_year=2011, tm_mon=5, tm_mday=5, tm_hour=14, tm_min=6, tm_sec=24, tm_wday=3, tm_yday=125, tm_isdst=0)
```
2. time.gmtime([secs])：和localtime()方法类似，gmtime()方法是将一个时间戳转换为UTC时区（0时区）的struct_time。
```python
>>>time.gmtime()
time.struct_time(tm_year=2011, tm_mon=5, tm_mday=5, tm_hour=6, tm_min=19, tm_sec=48, tm_wday=3, tm_yday=125, tm_isdst=0)
```
3. time.time()：返回当前时间的时间戳。
```python
>>> time.time()
1304575584.1361799
```
4. time.mktime(t)：将一个struct_time转化为时间戳。
```python
>>> time.mktime(time.localtime())
1304576839.0
```
5. time.sleep(secs)：线程推迟指定的时间运行。单位为秒。
6. time.clock()：这个需要注意，在不同的系统上含义不同。在UNIX系统上，它返回的是“进程时间”，它是用秒表示的浮点数（时间戳）。而在WINDOWS中，第一次调用，返回的是进程运行的实际时间。而第二次之后的调用是自第一次调用以后到现在的运行时间。（实际上是以WIN32上QueryPerformanceCounter()为基础，它比毫秒表示更为精确）
```python
import time  
if __name__ == '__main__':  
    time.sleep(1)  
    print "clock1:%s" % time.clock()  
    time.sleep(1)  
    print "clock2:%s" % time.clock()  
    time.sleep(1)  
    print "clock3:%s" % time.clock()
```
结果为:
```python
clock1:3.35238137808e-006
clock2:1.00004944763
clock3:2.00012040636
```
其中第一个clock()输出的是程序运行时间
第二、三个clock()输出的都是与第一个clock的时间间隔
7. time.asctime([t])：把一个表示时间的元组或者struct_time表示为这种形式：'Sun Jun 20 23:21:05 1993'。如果没有参数，将会将time.localtime()作为参数传入。
```python
>>> time.asctime()
'Thu May 5 14:55:43 2011'
```

> 其余可以去官网查阅`time`模块
