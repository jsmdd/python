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
