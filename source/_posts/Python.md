---
title: Python基础
tags: [linux,Python]
---
## linux命令
ls /cd /pwd /touch /mkdir /vi /cat /mroe /gedit /history /rm /rmdir /mroe /tree /ln /mv /grep /cp
/find /tar /which /cal /date /ps /kill /df /du /ifconfig /su /whoami

重定向:把显示结果存储

ls >xxx.txt //重新生成

ls >>xxx.txt //追加，若不存在则创建

相对路径:从当线路经开始算起的路径

绝对路径:从根目录开始算起的路径

cd - 返回

cd ~ home目录

ctrl + c 不执行


## 权限
* rwx ->可读可写可执行
* r-- ->只读
* r-x ->可读可执行

chmod u=rwx 1.py

文件拥有者可读可写可执行
### 数字法设置权限
* r -> 4
* w -> 2
* x -> 1
* 1可执行
* 2可写
* 3可写可执行
* 4可读
* 5可读可执行
* 6可读可写
* 7可读可写可执行

u文件拥有者、g同组、o其他

chmod 731 1.py

拥有者7 同组3 其他1

## Vim
命令模式---i-a-->编辑（插入）模式---:--->末行模式
### 命令模式

* yy 拷贝光标所在一行
* 4yy 拷贝光标所在行向下的四行
* dd 剪切光标所在一行
* dw 删除单词
* 3dd 剪切光标所在行向下的三行
* p 粘贴
* r 替换 R 替换光标之后的内容

* i 插入（光标前） I（行首）
* a 插入（后） I（行末）
* o 下一行 O上一行

* h左 j下 k上 l右

* M当前屏幕中间呢 H当前屏幕上方 L当场屏幕下方

* ctrl+f向下翻一页 ctrl+b向上翻一页
* ctrl+d向下翻一页 ctrl+u向上翻一页

* 20G 快速定位到第20行代码 G快速定位到整个代码末尾 gg快速定位到整个代码第一行

* w 向后跳一个单词的长度，即跳到下一个单词的开始处
* b 向前跳一个单此的长度，即跳到上一个单词的开始处

* D 从当前光标开始，向后的剪切

* u 撤销

* ctrl+r 反撤销

* d0 从当前光标开始剪切直到行首

* x 删除当前的光标
* X 删除当前的光标前面的字符

* V，v选中一片代码
* ``>>`` 向右移动代码 ``<<``向左移动代码
* . 重复执行代码

* { 按段移动（上移）} 按段移动（下移）
* shift+zz 相当于wq

### 末行模式

* w 保存 q 退出 wq 保存并退出
* / 搜索
* :%s/hello/hi/g  将hello替换为hi（%相当于整篇文章）
* :11,16%s/hello/hi/g  将11-16行hello替换为hi

## Python学习

### 第一个程序
``print("hello world")``
### 交互模式
直接输入python，进入Python的交互模式，exit()退出

python3,ipython,ipython3
### 注释
以#开头注释//单行注释

使用3个`即```包裹起来的为多行注释

### 语法
``score = 100``

``high = input("请输入你的身高：")``

python2：``high = raw_input("请输入你的身高：")``

``print("变能量的值为%s"%high)``

``print("姓名：%s，年龄：%d"%(name,age))`` 多个变量输出

``if age > 18:``

  ####``print("成年") //空格敏感``

``else:``

  ####``print("未成年")``

``type(a)`` 检查变量类型

``age_num = int(age)`` 变量类型转换

``len(name)``字符串长度

``import keyword
keyword.kwlist``查看关键字

``import random
random.randint(0,2)`` 0,1,2 3个随机数

``a%b``  取余

``a//b`` 取商

``a**b = a^b`` a的b次方

``if a>10 or a<5:`` 或

``if a>10 and a<15:`` 且

``if not (a>10 and a<15):``  取反

``if 条件1:``
  ####``xxxxxxx``

  ``elif 条件2:``
  ####``xxxxxxx``

### while循环

``while num<10:``  
  ####``num = num + 1``

``print(num)``

``prit("*",end="")`` 打印*号不换行

遍历字符串

``name  = "laowang"``

``for temp in name:``

取单个字符

``name = "abcde" ``

``name[0],name[1],name[2]``

切片

``name[2:4]``

``name[2:-1:2]`` 负数代表从后往前数，每隔两个取一个

[起始位置:终止位置:步长]

### 列表

``names = ["老王","老刘","老李"]``

#### 列表的CRUD
增

``names.append("悟空")``//添加新的元素

``names.inset(0,"八戒")``//在指定位置插入

``names.extends(names2)``//合并

删

``names.pop()``//删除最后一个

``names.remove("老王")`` //从左查找第一个删除

``del names[0]`` //指定下表删除

改

``names[0] = "沙和尚"``

查

``if "悟空" in names``

#### 遍历列表
``for num in nums:``
####``print(num)``

  for
  else
  for执行完执行else
### 字典
info = {键:值,键:值,键:值,键:值}

#### 字典的CRUD
增

``info["age"] = 18``

删

``del info["age"]``

改

``info["age"] = 29``

查

``info["name"]``

``info.get("name")`` //若无程序也不会崩溃

#### 字典的操作

``len(info)`` //键值对的个数

``info.keys()`` //返回列表，字典中所有的键

``info.value()`` //返回列表，字典中所有的值

``info.items()`` //返回元组列表，字典中所有的键和值

### 元组

``(33,)`` <-- 元组只有一个元素，则有逗号才叫元组
``num = (1,2,3)``

元足与列表类似,但是不能修改

``a = (1,2)``

``b,c = a``

则b=1,c=2

### 函数

``def function():``

``def function(num1,num2):``

返回值:return

函数的四种类型：
* 没有参数，没有返回值
* 有参数，没有返回值
* 没有参数，有返回值
* 有参数，有返回值

####  缺省参数
  ``def fun(a,b=11)``

  ``def fun(a,b,*args)``

  ``def fun(a,b,*args,**kwargs)``

  ``fun(11,22,33,task=88,done=77)``

  ``fun(11,22,33,*88,**77)``

### 变量

局部变量、全局变量

使用global用来对一个全局变量的声明,那么则不是定义一个局部变量，而是对全局变量进行修改。

``global tem ``

``tem = 12``

列表、字典为全局变量，不需要加global

### 引用

python中的等号，都是引用

``a=100``

``b=a``

会发现id相同

``id(a)==id(b)``

### 可变、不可变类型

可变类型：//不允许当字典的key值
* 列表
* 字典

不可变类型：
* 数字类型
* 字符串类型
* 元组

### 递归

### 匿名函数

  ``lambda 参数:式子``

  ``func = lambda x,y:x+y``

  ``func(1,2)``

  ``func_new = input("请输入一个匿名函数：")``

  ``func_new = eval(func_new)`` //在pythpon2中不需要这一步，而在python3中需要

  ``test(1,2,func_new)``


交换a，b方式2

``a = a + b``

``b = a - b``

``a = a - b``


``num = [100]``

``num = num + num`` //让num指向了一个新的值

``num += num `` //num指向直接修改


### 字符串

``mystr.find(str,start = 0,end = len(mystr))``

``mystr.index()`` //若不存在字符串会报错

``mystr.count()`` //字符串在mystr中出现的的次数

``mystr.replace("world","WORLD")`` //原字符串mystr不变，替换所有，第三个参数替换个数

``mystr.split(" ")`` //返回值为列表

``mystr.split()``  若不传参数，则按照不可见字符（空格,\t）切割

``mystr.capitalize()`` //第一个字母大写

``mystr.title()``   //所有字母开头大写

``mystr.splitlines()``


### 文件操作

#### 打开文件

``f = open("test.txt","w")``

#### 写数据

``f.write("hello world!")``

#### 读数据

``f.read()``   

``f.readlines()``

#### 关闭文件

``f.close()``

#### 案例：复制txt文件

步骤：

* 获取要复制的文件名input()
* 打开这个文件("r")
* 创建一个文件 xxx[复件].txt
* 从原文中读取数据
* 将读取的数据写入到新文件中
* 关闭两个文件

#### 定位读写

``f.tell()``

``f.seek(offset,from)``

* offset 偏移量
* from 方向 0:表示文件开头1:表示当前位置2:表示文件末尾


### 文件相关操作

#### 指令

``import os``

``os.rename("xx.txt","abc.txt")``

``os.remove("xx.txt")``

``os.mkdir("haha")``

``os.getcwd()`` //获取当前路径

``os.chdir()`` //改变默认路径

``os.listdir()`` //获取目录列表

``os.rmdir("haha")`` //删除文件夹

#### 批量修改文件名

``import os``

//获取一个要重命名的文件夹的名字

``folder_name = input("请输入要重命名的文件夹：")``

//获取那个个文件夹中所有的文件名字

``file_names = os.listdir(folder_name)``

``os.chdir(folder_name)``

//对获取的名字进行重命名

``for name in file_names:``

####``os.rename("name","[xx出品]-"+name)``

or

####``os.rename("./"+folder_name+"/"+"name","./"+folder_name+"/"+"[xx出品]-"+name)``

### 面向对象OO（object-oriented）

#### 面向过程

stu_a = {
        "name":"A",
        "age":18,
        "gender":1,
}

#### 类，对象

类名、类的属性、类的方法

``class cat:``

# 属性

####``def __init__(self,new_name,new_age):`` //初始化对象

########``self.name = new_name``

########``self.age = new_age``

####``def __str__(self):`` //初始化对象

########``return "%s的年龄是%d"%(self.name.self.age)``  

#方法

####``def eat(self):``

########``print("1")``

####``def drink(self):``

########``print("2")``

创建类对象

``tom = Cat("汤姆"，10)``

``tom.eat()``

``tom.drink()``

//``tom.name = "汤姆"``

//``tom.age = 4``

魔法方法

``__init__``方法：完成初始化功能

``__str__``方法：print(tom) ---> 打印__str__方法


保护对象的属性

setter，getter

私有方法   //私有方法、私有属性不会被继承

``def __test1(self):`` 验证条件满足后在公有方法中调用

``__del__``方法：对象被删除时调用

``import sys``

``sys.getrefcount()`` 测量到一个对象的引用计数（比实际大1）


继承父类

``class Cat(Aimal):``

调用父类方法

``父类名.方法（self）``

``super().方法()``

多继承

``class C(A,B):``

#### 多态

类属性、实例属性

* 类属性：所属于类对象，并且多个实例对象之间共享同一个类属性， 类名.属性名调用。
* 实例属性：和具体的某个实例对象有关系，并且和一个实例对象和另外一个实例对象是不共享属性的。

类方法、实例方法、静态方法

类方法:可以通过类的名字调用类方法，还可以通过这个类创建出来的对象，去调用这个类方法。

//@ 装饰器

``@classmethod``

``def add_num(cls)``

静态方法:类方法、实例方法必须有参数，静态参数可以没有参数，完成一些基本的操作。

``@staticmethod``

``def menu()``

``__new__(cls)``方法

* 调用__new__方法来创建对象，然后找了一个变量来接收__new__的返回值，这个返回值表示创建出来的对象的引用
* ``__init__``（刚刚创建出来的对象的引用）
* 返回对象的引用

//new方法只用于创建，init方法只用于初始化

### 单例

``def __new__(cls)``

####``__instance = None``

####``if cls.__instance == None:``

########``cls.__instance = object.__new__(cls)``

########``return object.__new__(cls)``

####``else:``

########``return cls.__instance``//return 上一次创建的对象的引用

### 异常

``try:``

``except 异常的名字（NameError|FileNotFoundError|Exception as ret）:``

####``print("出现了异常后的处理")``

//raise引发一个你定义的异常
``raise ShortInputException(len(s),3)``


### 模块

``import random``

``import os``

``from random import randint``

``randint()``

``from random import *``


当你导入一个模块时，将会将这个模块执行一遍

``if __name__ == '__main__':``

####``main()``

在模块内加入全局变量

``__all__ = ["test1","test2"]``


### 包

``touch TestMsg/__init__.py``

``__all__ = ["sendMsg"]``

``from . import sendMsg``

### 给程序传参数

``import sys``

``print(sys.argv)``

``name = sys.argv[1]``

### 列表推导式

``for i in range(10,78):``

用法类似切片，返回值为列表

``xxx[1:2:1]``

#### range的风险
python2中占用内存空间过大

#### 列表生成式

`` a = [i for i in range(1,18)]``

`` b = [i for i in range(10) if i%2 == 0]``

``c = [(i,j) for i in range(3) for j in range(2)]``


### set集合

``a = {11,22,33,44,55,66}`` //不能存储相同的

``f = set(a)`` //a为列表
