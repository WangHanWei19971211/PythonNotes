## 一 turtle库函数的介绍

1. 在lib目录下有一个turtle.py文件，这就是turtle的安装目录。官方文档：https://docs.python.org/3/library/turtle.html

2. turtle库画笔状态控制函数

   |       函数       | 描述                  |
   | :------------: | :------------------ |
   |    penup()     | 提起画笔，与pendown()配对使用 |
   |   pendwon()    | 放下画笔                |
   | pensize(width) | 设置画笔线条的粗细为指定大小      |

3. turtle库的画笔运动的函数

   |      **函数**       | **描述**                  |
   | :---------------: | :---------------------- |
   |     forward()     | 沿着当前方向前进指定距离            |
   |    backward()     | 沿着当前相反方向后退指定距离          |
   |   right(angle)    | 向右旋转angle角度             |
   |    left(angle)    | 向左旋转angle角度             |
   |    goto(x, y)     | 移动到绝对坐标（x, y)处          |
   |      setx()       | 将当前x轴移动到指定位置            |
   |      sety()       | 将当前y轴移动到指定位置            |
   | setheading(angle) | 设置当前朝向为angle的角度         |
   |      home()       | 设置当前画笔位置为原点，朝向东         |
   |   circle(step)    | 绘制一个指定半径、角度以及绘制步骤step的圆 |
   |   dot(r, color)   | 绘制一个指定半径r和颜色color的圆点    |
   |      undo()       | 撤销画笔最后一步动作              |
   |      speed()      | 设置的绘制速度，参数为0 - 10之间     |

4. turtle库的控制画笔和字体函数

   |           函数            | 描述                        |
   | :---------------------: | :------------------------ |
   |         color()         | 设置画笔的颜色                   |
   |      begin_fill()       | 填充图形前，调用该方法               |
   |       end_fill()        | 填充图形结束                    |
   |        filling()        | 返回填充的状态，True为填充，False为未填充 |
   |         clear()         | 清空当前窗口，但不改变当前画笔的位置        |
   |         reset()         | 清空当前窗口，并重置位置状态为默认值        |
   |      screensize()       | 设置画面的长和宽                  |
   |      hideturtle()       | 隐藏画笔的turtle形状             |
   |      showturtle()       | 显示画笔的turtle形状             |
   |       isvisible()       | 如果turtle可见，则返回Ture        |
   | write(str, font = None) | 输出font字体的字符串              |



