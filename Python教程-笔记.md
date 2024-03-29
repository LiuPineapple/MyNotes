# Python教程-笔记

## 3 Python基础

### 3.2 字符串和编码

格式化：

### 3.7 补充：Python运算符

1. 见如下总结：https://www.runoob.com/python/python-operators.html#ysf8

2. 运算符顺序可以简记为：算术运算符>按位运算符>比较运算符>赋值运算符>身份运算符>成员运算符>逻辑运算符

3. 比较运算符运算的结果是bool值，逻辑运算符是对bool值进行计算

4. 其他按位运算符都是bool值和int值分开算的，对于bool值，按位运算和逻辑运算除了优先级不同其他没什么不同，但~这个按位取反运算符无论是对于bool值还是int值，都会转换成int值然后按位取反。优先级也要高出其他按位运算符，和算术运算符同级

   eg:

```python
In [1]: ~True
Out[1]: -2
In [2]: ~False
Out[2]: -1
```

这是因为True的数字化表示为1，补码按位取反为-2；False的数字化表示为0，补码按位取反为-1

### 3.8 补充：转义

1. 转义即是让转义符后面的字符改变它原本在语言中定义的意思，比如在python中，'\n','\t',n和t本身都是字符，转义为换行符和tab键。'\\'原本是转义符，'\\\\'就是下划线本身的意思
2. 在正则表达式(regular expression)中也存在转义符，也是\，比如'\d'表示匹配数字，再比如，-在正则表达式中表示范围，\\-代表横杠本身
3. 在python中，字符串前面加r代表里面的每个字符都是它本身的意思
4. 建议在使用正则表达式的时候字符串前面加r，这样不用考虑python的转义，但是以然需要考虑正则表达式的转义

## 4 函数

### 4.2 定义函数

1. return的作用为提供函数返回值和终止函数运行，无论函数代码是什么样的，只要运行要return语句就自动终止运行并返回值
2. 函数中只写`return`、 `return None`是作用相同，都是结束执行并返回None
3. 如果不写`return`,python在把整个函数执行完后也会返回None，也就是说python函数一定有返回值
4. 函数返回多个值，本质上还是返回一个tuple，只是利用了创建tuple不用写括号这一特性。
5. 在其他代码中调用函数，但是又只想运行函数不想接收返回值的时候，只需要把函数名和参数写上不用变量接收就可以了。或者函数返回很多值但你只想接收一部分值，使用_来接收不想接收的那部分返回值

### 4.3 函数的参数

#### 4.3.1 位置参数与默认参数

1. 位置参数是必选参数
2. 函数定义时，默认参数必须放在必选参数的后面，而且必须指向不变对象（比如None）。
3. 函数调用时，任何参数（包括后面讲的可变参数等等）都可以有三种传入方式，一是按照定义时的顺序传入，不加参数名，二是不按照顺序传入，但要提供参数名。第三是传入元组和字典。前两种方式可以在一次函数调用中混合使用。
4. 这里面说的参数名就是形参，参数值就是实参。

#### 4.3.2 可变参数

1. 函数定义时，用星号标识可变参数，星号后面的参数将会被认为是一个可变参数，在函数体中作为元组调用
2. 函数调用时，接收的是数目不定（0个或多个）的传入参数，如果数目为0就接收到一个空元组。也可以接收一个元组/列表，前面加星号用来将list和tuple对象中的元素变成可变参数传入，传入之后变成元组是不可变对象，当然不会改变原list或tuple对象的值。

#### 4.3.3 关键字参数

1. 函数定义时，用两个星号标识关键字参数，**后面的参数将会被认为是一个可变参数，在函数体中作为字典调用
2. 函数调用时，接收的是数目不定（0个或多个）的键值对（等号连接）传入参数，如果数目为0就接收到一个空字典。也可以接收一个字典，前面加两个星号用来将l字典中的元素变成关键字参数传入，传入的是拷贝，无论函数做什么操作都不会影响原dict对象的值。

#### 4.3.4 命名关键字参数

1. 函数定义时，如果有可变参数，就直接放参数名在可变参数后面，如果没有可变参数，就要用,*,这样子，跟位置参数区分开。可以有默认值。
2. 函数调用时，不需要加多余的星号，但必须传入键值对（等号连接）的形式，不然无法与位置参数区分开。

#### 4.3.5 其他

1. 使用`*args`和`**kw`是Python的习惯写法，当然也可以用其他参数名，但最好使用习惯用法。

2. 函数定义中参数位置必须是——必选参数、默认参数、可变参数、命名关键字参数和关键字参数

3. python函数传参是否会改变函数外参数的值（记住即可，不深究）？

   - 也就是说，当我们传的参数是Number ,String , Tuple，bool等不可变对象时，无论函数中对其做什么操作，都不会改变函数外这个参数的值；当传的是dictionary、list等可变对象时，如果是重新对其进行赋值，则不会改变函数外参数的值，如果是对其进行操作，则会改变。

   - 这其实是因为python中的赋值符号=是对象引用的意思，即把a赋值给b其实是让b和a引用同一个对象

   - 而无论哪种编程语言，向函数传递参数的本质都是 形参=实参 即把实参赋值给形参。无论是C++中的值传递，地址传递，引用传递还是python中的对象引用传递都是基于此，赋值符号的意义不同造成了不同语言中参数传递的差异

   - 参考博文：

     https://www.cnblogs.com/monkey-moon/p/9347505.html

     https://blog.csdn.net/liuxiao214/article/details/81673093

4. 函数参数中的类型建议符（type hints），见如下讲解

   https://www.cnblogs.com/ArsenalfanInECNU/p/10724203.html

   https://www.python.org/dev/peps/pep-0484/

   类型建议符类似另一种形式的注释，并不会真的改变函数的执行

## 5 高级特性
### 5.1 切片
1. python的切片是前闭后开的
2. 列表、元组、字符串都可以切片
3. 索引超出范围会报错，但切片超出范围会返回空列表而不会报错
### 5.2 迭代
1. python中循环是通过可迭代对象Iterable完成的，而C++和java中是通过下标完成的。但是python中可以通过range(len())的方式实现下标循环
2. 在python的for循环中一次循环两个变量是很常见的

### 5.3 列表生成式
1. 在列表生成式中，for前面可以加if else三目运算符，这样元素数目不会少。而如果在for后面加if条件，那么只返回if条件为true的。

### 5.4 生成器
1. 创建生成器有两种方法，一个是将列表生成式的方括号改为圆括号，另一个是在定义函数的时候使用yield，那么这个函数将会成为一种特殊的generator函数，调用这个函数会返回generator
2. 生成器的特性是：可以用next()函数获得下一个值；惰性计算，即只有使用的时候才会把值计算出来；是可迭代对象Iterable
3. 生成器函数创建的生成器，除非迭代完成报StopIteration错误，否则永远拿不到return语句返回值。且每次迭代的值是yield的值，下次就从上次yield中断的地方重新开始运行。

### 5.5 迭代器
1. 可用于for循环的称为可迭代对象Iterable，包括python内置的序列类型，迭代器和其他有```__iter__```方法的对象
2. 可以使用next()不断调用获得下一个值的称为迭代器Iterator，它包括生成器。迭代器是惰性计算的，可以看作一个无限未知长度的数据流，而python内置数据类型都是已知长度且事先计算好放在内存中的，因此不是Iterator。
3. Iterable包括Iterator，Iterator包括generator
4. 可以使用iter()函数把Iterable变成Iterator
5. 可以在collections.abc中引入Iterable和Iterator

## 6 函数式编程
### 6.1 高阶函数
所谓高阶函数，就是把另一个函数作为自己的参数或者返回值的函数。python内置了很多高阶函数。

### 6.2 返回函数

### 6.3 匿名函数
匿名函数使用lambda关键字，没有函数名。lambda后面跟参数，可以有不止一个参数但只能有一个表达式，结果即为返回值

### 6.4 装饰器
1. 本质上，decorator就是一个返回函数的高阶函数。用于把很多函数都要写的重复代码抽象到装饰器中，免得重复去写。
2. 在函数定义前加上@decorator，相当于是先定义了这个function（假设函数名为now），接着又把now这个变量从原本定义的函数重新定向到了以now函数为参数的decorator上，即now = decorator(now)
3. 一般来讲，装饰器最终也会返回参数函数，所以参数函数的逻辑一定会得到执行，只不过在此基础上加了一些别的代码逻辑。
### 6.5 偏函数
1. 当函数的参数个数太多，需要简化时，使用functools.partial可以创建一个新的函数，这个新函数可以固定住原函数的部分参数，从而在调用时更简单。
2. 注意这里只是把这部分参数设定为默认参数且把默认值固定下来，如果想对这个默认参数传入其他值也是可以的。

## 8 面向对象编程

### 8.1 类和实例

一、类名一般首字母大写（建议规范而不是强制规范），python3创建类时括号内可以不写父类，这时默认继承object。在python3中，创建新的类，后面加/不加括号，加括号后里面写object，都是一样的继承object的新式类：

https://www.cnblogs.com/rainbow-ran/p/12204859.html

二、类中方法和普通函数的不同：

1. 创建类方法时第一个参数永远是self，其他参数完全一致
2. 写类方法的函数体时，调用本类的方法或属性时，前面要加self，即self.name等等
3. 调用时不需要传入self参数，因为解释器会帮你传入这个实例本身

三、创建实例属性的两种方法：

1. 创建实例后绑定
2. 使用魔法方法`__init__`（构造函数，本质上还是创建了实例后，实例传给self参数，然后绑定）

四、

1. 创建类属性的方法为不加self直接创建（使用self创建的都是实例属性），相同名字的实例属性会屏蔽掉类属性
2. del关键字可以删除属性

### 8.2 访问限制

1. 以双下划线开头，双下划线结尾的是特殊变量或特殊方法，是有特定作用的，但是属于公共方法，可以直接访问
2. 以双下划线开头的是私有（private）变量，内部可以访问，但外部不能访问
3. 以单下划线开头的是约定俗成的私有变量，可以直接访问，但不建议这么做
4. python类中似乎默认属性和方法是共有（public）的，除非特别说明

### 8.3 继承和多态

一、什么是OOP

Object Oriented Programming 即面向对象编程

二、多态的两种表现

1. 子类重写父类方法（类似C++中的静态多态）
2. 子类传入以父类为变量的函数（类似C++中的动态多态，遵循开闭原则）

三、

1. 总之，多态就是同一种方法，在父类和子类上的实现是不同的
2. python是动态语言，鸭子类型，python中的多态甚至不需要有父子类关系（典型例子len()函数）

四、

在python3中，创建新的类，后面加/不加括号，加括号后里面写object，都是一样的继承object的新式类：

https://www.cnblogs.com/rainbow-ran/p/12204859.html

五、子类调用父类重名函数

1. 子类继承了父类的方法和属性，如果在子类中重写了父类中的函数，子类函数会覆盖父类函数，如果想要调用父类中的重名函数，有两种方法：
   - https://www.bilibili.com/video/av70273365?p=302
   - https://www.cnblogs.com/linshuhui/p/9016553.html
   - https://cloud.tencent.com/developer/article/1486095
   - 注意：如果使用父类名.父类方法，self参数不能省略。如果使用super(本类名，self).或者super(). 那么不需要在方法里加self参数

2. 对于构造函数来说，python默认子类继承父类的构造函数，所以当子类不写构造函数时，默认使用父类的构造函数。但是在java当中，子类默认不继承父类的构造函数，而是使用默认空构造函数。如果子类要写构造函数的话，就算不用父类的构造函数，默认第一行也是父类的空构造函数super()，因此最好显示的写出来super(参数)

### 8.4 获取对象信息

一、isinstance

1. isinstance判断的是一个变量是否属于某个类，如果变量属于某个类，那么也属于它的父类
2. isinstance可以判断一个变量是否是某些类型中的一种，只需给第二个参数传入一个由类名组成的元组
3. isinstance即可以判断python内置的类，也可以判断我们自己写的类和包中的类（要先import进来）

二、dir

函数参数可以是对象也可以是类，返回其所有属性和方法

### 8.5 实例属性和类属性

见8.1二和三



## 10 错误、调试和测试

### 10.1 错误处理

1. except后面可以不加错误类型直接加冒号: 这时候会捕获所有错误

2. except ZeroDivisionError as e: 这个e并不是ZeroDivisionError而是报错时其后的内容，比如

   ZeroDivisionError: division by zero  则e就是division by zero

3. 如果所有的except后面跟的错误类型都不是真正发生的错误类型则程序还是会报错
4. else和finally区别很大。else和except只能执行其一，而finally只要有则总会执行

## 11 IO编程

### 11.1 文件读写

一、Python中read()、readline()和readlines()三者间的区别和用法:https://www.cnblogs.com/yun1108/p/8967334.html

### 11.5 补充：输入与输出

一、输出：

1. ```sys.stdout.write('hello')```

   标准化的输出

2. ```print('hello')```

   print的使用见官方文档：https://docs.python.org/3.7/library/functions.html#print

   默认的sep是空格' '，默认的end是'\n'，即输出后换行。print内部其实是在调用sys.stdout.write()

   ```print('hello','world')```效果等同于```sys.stdout.write('hello'+' '+'world'+'\n')```

二、输入：

1. ```sys.stdin```

   见如下博文https://www.cnblogs.com/ljxh/p/11189384.html

   需要掌握的就是sys.stdin.readline()和for循环读取for line in sys.stdin:

   前者类似于input()，一次读取一行输入，后者每一次的line都是一行输入。注意，无论输入是什么格式，都会被强转成字符串格式，而且末尾的换行符会保留

   ```python
   In [1]: import sys
   
   In [2]: a = sys.stdin.readline()
   37
   
   In [3]: a
   Out[3]: '37\n'
   ```

2. input()

   https://docs.python.org/3.7/library/functions.html#input

   input()可以展示提示信息，不过输入时一次只能输入一行，就算加换行符也会被当成普通字符。同时输入进来的内容全部会被转换成字符串

3. 两者的相似与不同
   - 两者都会将输入强制转换为字符串，都默认一次接收一行，即使行中有换行符'\n'也会被当成普通字符，两者输入时都不用加引号，因为默认字符串格式，而且就算加引号也会被当成普通字符处理。
   - input()括号内可以以字符串的形式直接填写说明文字，一般input('...\n')会比较好，sys.stdin还需要加个print方法给出提示信息
   - sys.stdin.readline( )会将标准输入全部获取**，**包括末尾的'\n'，因此用len计算长度时是把换行符'\n'算进去了的，但是input( )获取输入时返回的结果是不包含末尾的换行符'\n'的。对于sys.stdin.readline( )可以采用.strip()方法去掉后面的换行符
   - sys.stdin可以循环输入

## 13 正则表达式

2. 方括号[]表示范围，方括号括起来的表示一个要匹配的对象，只要满足方括号中的一个就算匹配上了

## 14 常用内建模块

### 14.12 random

见python官方文档：

https://docs.python.org/3.7/library/random.html?highlight=random#module-random

需要掌握的有：

random.seed() 选定随机数种子

random.randint() 给定上下界，离散均匀分布取值，与np中不同的是它上下界都包括

random.choice() 给定序列，随机从中取值

random.random() [0,1)均匀分布，类似于np中的np.random.rand()

random.uniform() 给定上下届均匀分布，类似于np中的np.random.uniform()，只不过上下界都包括

random.gauss() 生成正态分布，需要给定均值和标准差

random.randrange() 从生成的range中随机选一个，参数与range()相同

