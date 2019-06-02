## 一 文件的读写

1. file = open(path,flag[,encoding][, errors]) 	打开文件 将会返回一个 file 对象  这样打开需要手动关闭

   encoding:编码方式	encoding="utf-8"
   errors:错误处理		errors="ignore"(忽略错误)

   **注意：**ValueError: binary mode doesn't take an encoding argument

   ​	(ValueError：二进制模式不需要编码参数 )

   ##### open的打开方式

   |         以只读的方式打开文件，文件的描述符放在文件的开头         | r    |
   | :--------------------------------------: | ---- |
   |      以二进制格式打开一个文件用于只读，文件的描述符放在文件的开头      | rb   |
   |         打开一个文件用于读写，文件的描述符放在文件的开头         | r+   |
   |   打开一个文件只用于写入，如果该文件已经存在会覆盖，如果不存在则创建新文件   | w    |
   | 打开一个文件值用于写入二进制，如果该文件已经存在会覆盖，如果不存在则创建新文件  | Wb   |
   |         打开一个文件用于读写  如果不存在则创建新文件          | w+   |
   | 打开一个文件用于追加写，如果文件存在，文件描述符将会放到文件末尾  不存在则创建 | a    |
   | 打开一个文件用于追加写，如果文件存在，文件描述符将会放到文件末尾  不存在则创建 | ab   |
   | 打开一个文件用于读写  如果该文件已存在，文件指针将会放在文件的结尾  不存在则创建 | a+   |

##### 实例

```python
#以utf-8编码的方式读
f = open('1.txt','r',encoding='utf-8') #这个位置 不能使用rb 
#以utf-8编码的方式写
f = open('a.txt','w',encoding='utf-8')
f.write('呵呵哒')
```

####  2 文件的读取

​	file.read([size]) 		从文件读取指定的字节数，如果未给定或为负则读取所有。

​	file.readline([size\])] 	读取整行，包括 "\n" 字符。如果有size 读取所给字节数

​	file.readlines() 		读取所有行并返回列表

​	next(file)			返回文件下一行。

​	seek(offset[,1whence])			方法用于移动文件读取指针到指定位置。

​		f.seek(0)   #移动到首位

​		offset -- 开始的偏移量，也就是代表需要移动偏移的字节数

​		whence：可选，默认值为 0。给offset参数一个定义，表示要从哪个位置开始偏移；0代表从文件开头开始算起，1代表从当前位置开始算起，2代表从文件末尾算起

#### 3 文件的写

​	file.write(str)			将字符串写入文件，没有返回值。

​	file.writelines()		向文件写入一个序列字符串列表，如果需要换行则要自己加入每行的换行符。没有返回值

​	file.flush()			刷新文件内部缓冲，直接把内部缓冲区的数据立刻写入文件, 而不是被动的等待输出缓冲区写入。

#### 4 返回文件当前位置。

​	file.tell（） 		

 #### 5 关闭文件

​	file.close()			

你可以反复调用`write()`来写入文件，但是务必要调用`f.close()`来关闭文件。当我们写文件时，操作系统往往不会立刻把数据写入磁盘，而是放到内存缓存起来，空闲的时候再慢慢写入。只有调用`close()`方法时，操作系统才保证把没有写入的数据全部写入磁盘。忘记调用`close()`的后果是数据可能只写了一部分到磁盘，剩下的丢失了。所以，还是用`with`语句来得保险

#### utf-8一个占3个字节   gbk每个占2个字节

## 二 打开文件不需要关闭

```python
with open(path, "a") as f2:
	f2.write("good man")
```

达语句末尾时，会自动关闭文件，即便出现异常

**实例**

**不使用with的情况**

```python
file = open("test.txt","r")
for line in file.readlines():
    print line
file.close()
```

这样直接打开文件，如果出现异常，如读取过程中文件不存在或异常，则直接出现错误，close方法无法执行，文件无法关闭

**使用with的情况**

```python
file= open("test.txt","r")
try:
    for line in file.readlines():
        print line
except:
    print "error"
finally:
    file.close()
```

with语句作用效果相当于上面的try-except-finally

## 三 编码与解码  使用什么编码 就使用什么解码

1. str.encode("utf-8")
2. str.decode("utf-8")

## 四 列子

1.文件加密

```python
file = open('1.py','r')     
myfile = open('2.py','a+')  
x = file.read()  
for i in x:              
    z = chr(ord(i)+10)   
    myfile.write(z)      
```

2.文件解密

```python
file = open('4.py','r')       
myfile = open('5.py','a+')
x = file.read()  
for i in x:            
    z = chr(ord(i)-10) 
    myfile.write(z)    
```

## 四 pickle 序列化的操作

##### 使用说明：可以将序列 序列化到 文件里 也就是 可以做到 原样写入 原样拿出

##### 以二进制写进文件里 并以二进制的形式读取到内存里

#### (1) dump 写入文件

##### 将数据序列化后写入到 文件里

​	pickle.dump(数据,文件打开返回的file)

#### (2) load  将数据反序列化 取出来

​	pickle.load(文件打开返回的file)

#### (3) dumps 将数据序列化 直接返回

​	pickle.dumps(数据)

#### (4) loads  将dumps序列化后的 进制 转换成 普通的数据类型

​	pickle.loads(序列化的数据)

#### 例如：

```python
import pickle

mylist=[[1,2,3,4,5,6,7],["abc","xyz","hello"]]
file=open(r"C:\Users\xlg\Desktop\list.bin","wb")
pickle.dump(mylist,file) #保存list到文件
file.close()

import pickle
mylist=[]
file=open(r"C:\Users\xlg\Desktop\list.bin","rb")
mylist=pickle.load(file) #读取文件到list
print(mylist)
```



## 五 二进制文件

[二进制文件]。原因大概有三个：　　第一是[二进制文件]比较节约空间，这两者储存[字符型数据]时并没有差别。但是在储存数字，特别是实型数字时，二进制更节省空间，比如储存 Real*4 的数据：3.1415927，文本文件需要 9 个字节，分别储存：3 . 1 4 1 5 9 2 7 这 9 个 ASCII 值，而[二进制文件]只需要 4 个字节（DB 0F 49 40）　　第二个原因是，内存中参加计算的数据都是用二进制无格式储存起来的，因此，使用二进制储存到文件就更快捷。如果储存为文本文件，则需要一个转换的过程。在数据量很大的时候，两者就会有明显的速度差别了。　　第三，就是一些比较精确的数据，使用二进制储存不会造成有效位的丢失。