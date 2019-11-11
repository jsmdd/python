# 初识

import this
> 都是“Python之禅”

import turtle
> 一个有点意思的构图函数
```
import turtle
turtle.pensize(4)
turtle.pencolor('red')

turtle.forward(100)
turtle.right(90)
turtle.forward(100)
turtle.right(90)
turtle.forward(100)
turtle.right(90)
turtle.forward(100)
```
> 详解：https://docs.python.org/zh-cn/3/library/turtle.html

特别注意此坐标系为原点的前进方向为forward，后退为backword，下为rt，上为lt(与mode模式有关，默认是standard)
```
"""
python的turtle绘制国旗
"""
import turtle

turtle.pencolor('red')
turtle.fillcolor('red')

turtle.begin_fill()
for i in range(2):
    turtle.forward(240)
    turtle.rt(90)
    turtle.forward(160)
    turtle.rt(90)
turtle.end_fill()

turtle.pencolor("yellow")
turtle.fillcolor("yellow")

turtle.begin_fill()
for i in range(2):
    turtle.backward(240)
    turtle.rt(90)
    turtle.forward(160)
    turtle.rt(90)
turtle.end_fill()

turtle.pencolor("green")
turtle.fillcolor("green")

turtle.begin_fill()
for i in range(2):
    turtle.backward(240)
    turtle.lt(90)
    turtle.forward(160)
    turtle.lt(90)
turtle.end_fill()

turtle.pencolor("blue")
turtle.fillcolor("blue")

turtle.begin_fill()
for i in range(2):
    turtle.forward(240)
    turtle.lt(90)
    turtle.forward(160)
    turtle.lt(90)
turtle.end_fill()

turtle.done()

```
