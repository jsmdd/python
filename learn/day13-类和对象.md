### 定义类

在Python中可以使用`class`关键字定义类，然后在类中通过之前学习过的函数来定义方法，这样就可以将对象的动态特征描述出来，代码如下所示。
```Python
class Student(object):  # （object）表示该类从哪个类继承下来的，object类是所有类都会继承的类。
    def __init__(self,name,age):  
        self.name=name
        self.age=age

    def study(self,course_name):
        print(f"{self.name} are studying {course_name}")

    def watch_move(self):
        if self.age > 18:
            print(f"{self.name} only watch tom and jerry~")
        else:
            print(f"{self.name} can watch AV~")
```
1. `__init__`方法的第一参数永远是`self`，表示创建的类实例本身，因此，在`__init__`方法内部，就可以把各种属性绑定到`self`，因为`self`就指向创建的实例本身。
2. 有了`__init__`方法，创建实例的时候，就不能传入空的参数了，必须传入与`__init__`方法匹配的参数，但`self`不需要传，`Python`解释器会自己把实例变量传进去
3. 另外，这里`self`就是指类本身，`self.name`就是`Student`类的属性变量，是`Student`类所有。而`name`是外部传来的参数，不是`Student`类所自带的。
故，`self.name = name`的意思就是把外部传来的参数`name`的值赋值给`Student`类自己的属性变量`self.name`

### 创建和使用对象
当我们定义好一个类之后，可以通过下面的方式来创建对象并给对象发消息。
```Python
def main():
    stu1 = Student('tom', 23)
    stu1.study('you jump,i jump')
    stu1.watch_move()
    print()
    sut2=Student('jerry',14)
    sut2.study('just dance')
    sut2.watch_move()

if __name__=='__main__':
    main()
```
结果为:
```python
tom are studying you jump,i jump
tom only watch tom and jerry~

jerry are studying just dance
jerry can watch AV~
```

### 练习1：定义一个类描述数字时钟。
```python
import time,os

class Clock(object):

    def __init__(self,hour=0,minute=0,sencond=0):
        self.hour=hour
        self.minute=minute
        self.sencond=sencond

    def run(self):   # 通过判断让时间变化
        self.sencond+=1
        if self.sencond==60:
            self.sencond=0
            self.minute+=1
            if self.minute==60:
                self.minute=0
                self.hour+=1
                if self.hour==24:
                    self.hour=0

    def show(self):
        return '%02d:%02d:%02d'%(self.hour,self.minute,self.sencond)
        # %02d，和%2d差不多，只不过左边补0,用来显示标准时钟的格式
def main():
    #clock=Clock(hour=23,minute=59,sencond=50)
    clock=Clock()
    while True:   #  通过一个sleep 1 让显示的时钟和真实时间对应的上
        os.system('cls')
        print(clock.show())
        time.sleep(1)
        clock.run()

if __name__=='__main__':
    main()
```

#### 练习2：定义一个类描述平面上的点并提供移动点和计算到另一个点距离的方法。
```python
import math
import sys

class Point():

    def __init__(self,x=0,y=0):
        self.x=x
        self.y=y

    def move(self,x,y):
        self.x=x
        self.y=y

    def distance(self,other):
        a=(self.x-other.x)
        b=(self.y-other.y)
        c=math.sqrt(a**2+b**2)
        return c

def main():
    print(sys.argv)   # 可以看出sys.argv的作用
    p1=Point(float(sys.argv[1]),float(sys.argv[2]))
    p2=Point()
    p1.move(3,4)
    p2.move(0,0)
    print("%.2f"%(p2.distance(p1)))

if __name__=='__main__':
    main()
```
