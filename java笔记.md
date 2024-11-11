# Java笔记

[TOC]

#### 1、Java语言

Java语言是纯粹的面向对象的程序设计语言，这主要表现为Java完全支持面向对象的三种基本特征：封装、继承和多态。Java语言完全以对象为中心，最小的程序单元是类。

#### 2、垃圾回收机制

垃圾回收机制的工作目标是回收无用对象的内存空间，这些内存空间都是JVM堆内存里的内存空间，垃圾回收只能回收内存资源，对其他物理资源，如数据库连接、磁盘 I/O等资源则无能为力、

#### 3、面向过程与面向对象![image-20210912144047236](C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20210912144047236.png)

#### 4、面向对象的基本特征：封装、继承、多态。

封装：将对象的实现细节隐藏起来，然后通过一些公用方法来暴露对象的功能；

继承：子类继承父类后，将直接获得父类的属性和方法；

多态：子类对象可以直接赋给父类引用变量，但运行时依然表现出子类的行为特征。

（使用父类变量时，变量看左边，方法看右边，**但是父类中没有的方法不能访问**；总之父类引用变量都各处都是表现出父类对象的特征，只有在调用子类重写方法时，运行的是子类重写后的方法）

#### 5、Java中四个权限修饰符的作用域

private : 类内访问

默认：包内访问

protected : 包外子类访问  

（被 protected 修饰的成员对于本包和其子类可见：

1. 父类的 protected 成员是包内可见的，并且对子类可见
2. 若子类与父类不在同一包中，那么在子类中，子类实例可以访问从父类继承而来的 protected 方法，而不能访问父类实例的 protected 方法）

public ：包外访问

**在哪个类里写的代码，比如调用一个方法，看的就是这个类有没有该方法的访问权限。**（调用者的类总是有这个方法的访问权限！）

#### 6、基本数据类型

除了8个基本数据类型值外（char, byte, short , int , long , boolean , float , double），一切都是对象。Java中浮点类型默认是double类型，如果希望Java把一个浮点类型值当成float类型处理，应该在这个浮点类型值后紧跟 f 或 F ，long类型的数字后面要跟L，如果不加L，默认的取值范围是int。*Python*3 支持int、float（64bit）、bool、complex（复数）

#### 7、关键字

Java的所有关键字都是小写的，TRUE、FALSE和NULL都不是Java关键字

#### 8、Unicode字符集：

**代码点（Code Point）**：在 Unicode 代码空间中的一个值，取值 0x0 至 0x10FFFF，代表**一个字符**。就是某个任意字符在Unicode编码表中对应的代码值。
**代码单元（Code Unit）**：在具体编码形式中的最小单位。比如 UTF-16 中一个 code unit 为 16 bits，UTF-8 中一个 code unit 为 8 bits。是在计算机中用来表示码点的，大部分码点只需要一个代码单元表示，但是有一些是需要两个代码单元表示的。



![image-20211018123757442](C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211018123757442.png)

在 Unicode 标准中，码点采用十六进制书写，并加上前缀 U+, 例如 U+0041 就是拉丁字母 A 的码点。Unicode 的码点可以分成 17 个代码级别。第一个代码级别称为基本的多语言级别，码点从 U+0000 到 U+FFFF，其中包括经典的 Unicode 代码（里面应该包括了所有常用汉字）；其余的 16个级码点从 U+10000 到 U+10FFFF，其中包括一些辅助字符。



其实 Unicode 涉及到两个步骤，首先是定义一个规范，给所有的字符指定一个唯一对应的数字，这完全是数学问题，可以跟计算机没半毛钱关系（**字符集**）。第二步才是怎么把字符对应的数字保存在计算机中，这才涉及到实际在计算机中占多少字节空间（**编码方案**）。

unicode在计算机中如何存储呢，就是用unicode字符集转换格式，UTF(unicode transformation format)，即我们常见的UTF-8、UTF-16等。

GBK：不论中英文字符都是双字节；

utf-8：英文字符一个字节，中文三个；

utf-16：在Unicode基本多文种平面（码点从 U+0000 到 U+FFFF）定义的字符（无论是拉丁字母、汉字)或其他文字或符号），一律使用2字节储存。而在辅助平面定义的字符，会以代理对（surrogate pair）的形式，以两个2字节的值来储存。

utf-16比起utf-8，好处在于大部分字符都以固定长度的字节（2字节）储存，但utf-16却无法兼容于ASCII编码。

例子1：

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211018123949440.png" alt="image-20211018123949440" style="zoom:67%;" />

已知"严"的unicode是4E25(1001110 00100101), 根据上表, 可以发现4E25处在第三行的范围内(0000 0800 - 0000 FFFF), 因此"严"的UTF-8编码需要三个字节, 即格式是"1110xxxx 10xxxxxx 10xxxxxx". 然后, 从"严"的最后一个二进制位开始, 依次从后向前填入格式中的x, 多出的位补0. 这样就得到了, "严"的UTF-8编码是 "11100100 1011100010100101", 转换成十六进制就是E4B8A5.

例子2：

将某个字符的Unicode值转换为UTF-16的编码按照以下步骤进行。假设U是给Unicode值，小于0x10FFFF。Unicode值大于0x10FFFF不能按照UTF-16进行编码。 

1) **如果U < 0x10000，U的编码就是无符号的十六位整数，值和其本身的值一样，处理结束**。
2) 如果U等于或者小于0x10FFFF，则设U' = U - 0x10000。此时，U'一定小于或者等于0xFFFFF,也就是说，U'的值不会超过20位。
3) 分别初始化2个16位无符号的整数，W1和W2为0xD800和0xDC00。每个整数都有10位可以用来对字符进行编码，正好能容纳U'的20位。
4) 将U'的高10位分配给W1的低10位，将U'的低10位分配给W2的低10位，处理结束。

#### 9、转义字符：

​       在Java程序中表示一个绝对路径：“c:\codes”，这种写法Java会把反斜线当作转义字符，所以应该写成这种形式："c:\\\codes"，只有同时写两个反斜线，Java才会把第一个反斜线当成转义字符，和后一个反斜线组成真正的反斜线。

##### 9.1、Windows中的回车和换行 “\r\n”

在Windows的文件中：

'\r' 回车，回到当前行的行首，而不会换到下一行；（return?）
'\n' 换行，换到当前位置的下一行，而不会回到行首；（newLine?）

linux系统里，每行结尾只有"<换行>"，即"\n"；Windows系统里面，每行结尾是"<回车><换行>"，即"\r\n"；

在vs2017、idea 里输出时，换行都只需要‘\n’。

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211018184819161.png" alt="image-20211018184819161" style="zoom: 80%;" />![image-20211018184912854](C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211018184912854.png)

好像都起到了换行的作用，但实际上写入的字符都没变，第一行末尾确实只有一个字符'\r'，应该是打开文件的程序让这些符号都起到的换行的效果。

而且用Scanner 中的nextLine()  以及BufferedReader 中的readLine() 都可以正确读每一行。

#### 10、 直接量：

直接量是指在程序中通过源代码直接给出的值，例如在int a = 5 ;这行代码中，初始量5就是一个**int型**的直接量。  

#### 11、判断是否相等：

1）基本数据类型用"=="就行了，相等返回true，否则返回false

2）引用数据类型"=="判断的是地址，equals()方法判断的是值

3）自定义对象判断相等，需要重写equals()方法

#### 12、数组：

数组的初始化完成后，长度将不可改变，数组也是一种数据类型，它本身是一种引用类型。

初始化：

1）静态初始化：int[] a = {1,2,3,4};（是int[] a = new int[]{1,2,3,4} 的简化版本）

2）动态初始化：int[] a = new int[4];  //系统默认为数组中的元素分配初始值0

数组虽然是一个对象，但是其并没有提供add()或者remove()等操作元素的方法，要删除元素的话，可以通过将数组对象转换成List再进行remove()

打印数组：Arrays.toString()

集合重写了toString() 方法   

#### 13、长度

length -- 数组的属性

length() -- 字符串的方法

size() -- 集合的方法 

#### 14、二维数组

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20210912203412021.png" alt="image-20210912203412021" style="zoom: 80%;" />

#### 15、字符串与基本数据类型相互转换：

String.valueof(int i) : 将 int 变量 i 转换成字符串；

Integer.parseInt(String s) : 将字符串 s 转换成 int。

#### 16、static:

static的真正作用就是用于区分成员变量、方法、内部类、初始化块这四种成员到底属于类本身还是属于实例。static相当于一个标志，有static修饰的成员属于类本身，没有static修饰的成员属于该类的实例。

静态成员不能直接访问非静态成员

#### 17、编译时类型与运行时类型

Java引用变量有两个类型，一个是编译时类型，还有一个是运行时类型。

编译时类型是由声明该变量时使用的类型所决定，运行时类型是由该变量指向的对象类型决定。

当使用该对象引用进行调用时，有这么一条规则，**对象调用编译时类型的属性和运行时类型的方法。**

#### 18、方法的调用：

方法不能独立存在，方法必须属于类或对象。

在同一个类里不同方法之间相互调用时，不就可以直接调用吗？这里需要指出：同一个类的一个方法调用另外一个方法时，如果被调方法是普通方法，则默认使用this作为调用者；如果被调方法是静态方法，则默认使用类作为调用者。

#### 19、方法的参数传递：

Java里的参数传递方式只有一种：值传递。所谓值传递，就是将实际参数值的副本（复制品）传入方法内，而参数本身不会受到任何影响。（相当于复制一份）

#### 20、方法重载：

如果同一个类中包含了两个或两个以上的**方法名相同，但形参列表不同**，则称为方法重载。

#### 21、成员变量和局部变量：

成员变量无须显示初始化，只要为一个类定义了类变量或实例变量，系统就会在这个类的准备阶段或创建该类的实例时进行默认初始化。

类成员变量可以作为这个类的所有实例的共同变量，也就是共享存储区。

局部变量除了形参之外，都必须显式初始化，否则不可以访问它们。

#### 22、类对象

如果代码是第一次使用某类，则系统通常会在第一次使用该类时加载这个类，并初始化这个类。

会在堆内存区创建一个类对象，为类变量分配空间并初始化。

类名.class 是获得这个类所对应的Class实例（反射？？？？）

对象.getClass() 获得这个类的类对象

#### 23、classpath

一个类的包装从classpath开始。

假如你有如下的目录结构：a\b\c\d\class A , 并且你的类路径从c开始，那么你的类应该在包d中而不是在abc中。（这里的文件A指的是字节码文件）

import关键字可以从当前classpath中导入类，在classpath之外导入不能使用。

#### 24 、this调用构造器

使用 this 调用另一个重载的构造器只能在构造器中使用，而且必须作为构造器执行体的第一条语句。

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20210913201956349.png" alt="image-20210913201956349" style="zoom:67%;" />

#### 25、子类不会继承父类的类变量

1）子类是不继承父类的static变量和方法的。因为这是属于类本身的。但是子类是可以访问的（子类类名.父类static变量）。 
2）子类和父类中同名的static变量和方法都是相互独立的，并不存在任何的重写的关系。**因此也是不存在多态特性的。**而对于普通方法的调用是存在“重写”而最终呈现出多态特性的。

#### 26、方法的重写：

遵循“两同两小一大”规则，“两同”即方法名相同、形参列表相同；“两小”指的是子类方法返回值类型应比父类方法返回值类型更小或相等，子类方法声明抛出的异常应比父类方法声明抛出的异常更小或相等；“一大”指的是子类方法的访问权限应比父类方法的访问权限更大或相等。

#### 27、子类继承实例变量

当程序创建一个子类对象时，系统不仅会为该类中定义的实例变量分配内存，也会为它从父类继承得到的所有实例变量分配内存，即使是子类定义了与父类中同名的实例变量。

也就是说，当系统创建一个Java对象时，如果该Java类有两个父类（一个直接父类A，一个间接父类B)，假设A类中定义了2个实例变量，B类中定义了3个实例变量，当前类中定义了2个实例变量，那么这个Java对象将会保存2+3+2个实例变量。

如果在子类中定义了与父类同名的变量，那么子类中定义的变量会隐藏父类中定义的变量。注意不是完全覆盖，因此系统在创建子类对象时，依然会为父类中定义的、被隐藏的变量分配内存空间。

#### 28、构造器的执行顺序

子类构造器执行体中既没有super调用，也没有this调用，系统会在执行子类构造器之前，隐式调用父类无参数的构造器。

当调用子类构造器来初始化子类对象时，父类构造器总会在子类构造器之前执行；不仅如此，执行父类构造器时，系统会再次上溯执行其父类构造器。。。依此类推，创建任何Java对象，最先执行的总是Java.lang.Object类的构造器。

#### 29、编译时类型和运行时类型：

Person p=new Women()(Women类继承自Person类)那么，假如p的属性修饰符为public 访问属性时得到的是Person类的属性还是Women类的属性，方法调用又是哪个类？答案：会得到Person类的属性，调用Women类的方法。为什么会这样呢？这里就需要知道什么是编译时类型和运行时类型，Java程序状态会分为编译和运行这两种状态，**编译时，JVM会在栈中静态创建基本数据变量，和引用数据变量的引用**，回到刚刚那句代码，显然，p这个引用就是在编译时创建的，那么，p的编译时类型就是Person了，当运行这句Java代码时，JVM在堆中为p新建一块内存，对应new Women（）这句代码，所以p的运行时类型就是Women。

#### 30、instanceof

用法：A instanceof B，返回值是boolean类型，**用来判断A指向的对象是否是B的实例对象或者B子类的实例对象**。

A为引用变量，B为类名，用于判断的是A指向的对象。

通常先用instanceof判断一个对象是否可以强制类型转换，然后再使用（type）运算符进行强制类型转换，从而保证程序不会出现错误。

#### 31、初始化块：

当Java创建一个对象时，系统先为该对象的所有实例变量分配内存（前提是该类已经被加载过了），接着程序开始对这些实例变量执行初始化，其初始化顺序是：先执行初始化块或声明实例变量时指定的初始值（这两个地方指定初始值的执行允许与它们在源代码中的排列顺序相同），再执行构造器里指定的初始值。

从某种程度上来看，初始化块是构造器的补充，初始化块总是在构造器执行之前执行。

实际上初始化块是一个假象，使用Javac命令编译Java类后，该Java类中的初始化块会消失---初始化块中代码会被“还原”到每个构造器中，且位于构造器所有代码的前面。（可以看作把初始化块和public int a = 2中的 a = 2 按照代码顺序带入构造器最开头）

基本用法：

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20210914222245881.png" alt="image-20210914222245881" style="zoom: 80%;" />

普通初始化块负责对对象执行初始化，静态初始化块则负责对类进行初始化。**系统将在类初始化阶段执行静态初始化块**，而不是在创建对象时才执行。

#### 32、自动装箱、自动拆箱

借助包装类的帮助，再加上JDK1.5提供的自动装箱、自动拆箱功能，开发者可以把基本类型的变量“近似”地当成对象使用（所有装箱、拆箱过程都有系统自动完成，无须程序员理会）；反过来，开发者也可以把包装类的实例近似地当成基本类型的变量使用。

#### 33、输出方法——println()

System.out 的 println()方法只能在控制台输出字符串，会默认调用对象的toString（）方法。toString（）方法是Object类里的一个实例方法，因此所有的Java对象都具有toString（）方法。

Object类提供的toString方法总是返回该对象实现类的 “类名+@+hashCode”值。

Object类默认提供的equals()方法只是比较对象的地址，即Object类的equals()方法比较的结果与==运算符比较的结果相同。因此实际应用中常常需要重写equals()方法。

#### 34、"abc"直接量和new String（"abc"）有什么区别呢？

String是一个特殊的包装类数据。即可以用String str = new String("abc");的形式来创建，也可以用String str = "abc"；的形式来创建。

String str = "abc"创建对象的过程：

​    1）、首先在常量池中查找是否存在内容为"abc"字符串对象
​    2）、如果不存在则在常量池中创建"abc"，并让str引用该对象
​    3）、如果存在则直接让str引用该对象

"abc"是怎么保存，保存在哪？
    常量池属于类信息的一部分，而类信息反映到JVM内存模型中是对应存在于JVM内存模型的方法区，也就是说这个类信息中的常量池概念是存在于在方法区中。


String str = new String("abc")创建实例的过程：

​    1）、首先在堆中（不是常量池）创建一个指定的对象"abc"，并让str引用指向该对象
​    2）、在字符串常量池中查看，是否存在内容为"abc"字符串对象
​    3）、若存在，则将new出来的字符串对象与字符串常量池中的对象联系起来
​    4）、若不存在，则在字符串常量池中创建一个内容为"abc"的字符串对象，并将堆中的对象与之联系起来

我们来看以下两个例子加深理解：
String str1 = "abc"; String str2 = "ab" + "c"; str1==str2是true吗？
答案：是。因为String str2 = "ab" + "c"会查找常量池中时候存在内容为"abc"字符串对象，如存在则直接让str2引用该对象，显然String str1 = "abc"的时候，上面说了，会在常量池中创建"abc"对象，所以str1引用该对象，str2也引用该对象，所以str1==str2



String str1 = "abc"; String str2 = "ab"; String str3 = str2 + "c"; str1==str3是false吗？
答案：是。因为String str3 = str2 + "c"涉及到变量（不全是常量）的相加，所以会生成新的对象，其内部实现是先new一个StringBuilder，然后 append(str2),append("c");然后让str3引用toString()返回的对象

#### 35、方法区、堆区与栈区

1).方法区：存储类信息、常量、静态变量。全局共享。
2).堆区：存放对象和数组。全局共享。
3).栈区：基本数据类型、对象的引用都存放在这。线程私有。

#### 36、final

对于final修饰的成员变量而言，一旦有了初始值，就不能被重新赋值。

final成员变量（包括实例变量和类变量）必须由程序员显式初始化，系统不会对final成员进行隐式初始化。

归纳起来，final修饰的类变量、实例变量能指定初始值的地方如下。
>类变量：必须在静态初始化块中指定初始值或声明该类变量时指定初始值，而且只能在两个地方的其中之一指定。
>实例变量：必须在非静态初始化块、声明该实例变量或构造器中指定初始值，而且只能在三个地方的其中之一指定。

final修饰的局部变量，和正常局部变量一样使用，只是只能赋值一次。

final修饰引用变量，保证这个引用变量所引用的地址不变，但是这个对象完全可以发生改变。

#### 37、子类可以继承父类的私有成员吗？

在一个子类被创建的时候，首先会在内存中创建一个父类对象，然后在父类对象外部放上子类独有的属性，两者合起来形成一个子类的对象。所以所谓的继承使子类拥有父类所有的属性和方法其实可以这样理解，子类对象确实拥有父类对象中所有的属性和方法，但是父类对象中的私有属性和方法，子类是无法访问到的，只是拥有，但不能使用。就像有些东西你可能拥有，但是你并不能使用。所以子类对象是绝对大于父类对象的，所谓的子类对象只能继承父类非私有的属性及方法的说法是错误的。**可以继承，只是无法访问到而已**。

#### 38、不可变类：

不可变类的意思是创建该类的实例后，该实例的实例变量是不可改变的。Java提供的8个包装类和String类都是不可变类，当创建它们的实例后，其实例的实例变量不可改变。

#### 39、抽象类

​       有抽象方法的类只能被定义成抽象类，抽象类里可以没有抽象方法

​        抽象类不能被实例化，抽象类的构造器主要是用于被子类调用。

​        例子： `public abstract void sum();`

#### 40、接口（interface）

接口（interface）里不能包含普通方法，接口里所有方法都是抽象方法，只有在Java8以上的版本中才允许在接口中定义默认方法

​        一个接口可以有多个直接父接口，但接口只能继承接口，不能继承类。

​        接口里不能包含构造器和初始化块定义，可以包含成员变量（只能是静态常量），方法（只能是抽象实例方法、类方法或默认方法）、内部类（包括内部接口、枚举）定义。

​       接口里的所有成员，包括常量、方法、内部类和内部类枚举都是public 访问权限。定义接口成员时，可以省略访问控制符，如果指定访问控制符，则只能使用public。

​       对于接口里定义的静态常量而言，系统会自动为这些成员变量增加static 和 final 两个修饰符（没有写则系统默认添加）。

​       接口里的普通方法默认使用public abstract来修饰。

​       从某个角度看，**接口可被当成一个特殊的类，因此一个Java源文件里最多只能有一个public接口**，如果一个Java源文件里定义了一个public接口，则该源文件的主文件名必须与该接口名相同。（接口修饰符可以是public或者默认）



​        (接口继承了父接口的静态常量？？？？？）我觉得没有，无论是子接口或者是实现接口的类，它们的实例都没有继承，只是可以访问，可以直接用接口.变量访问，或者子接口.变量访问，实现接口的类的实例的引用变量.变量（最好 不要这么用），都说了接口就像特殊的类。

#### 41、面向接口编程

与接口耦合，而不是与类耦合

#### 42、外部类与内部类的修饰符：

外部类的上一层单元是包，对于外部类来说，只有两个作用域：同包或者任何位置，因此只需要两种控制权限：包控制权限和公开控制权限，即default和public。

而对于内部类来说就可以使用private和protected修饰符了，因为内部类外部有三个作用域：外部类、同包或者任何位置，以及还有父子类。因此，内部类使用private修饰，限定为本外部类使用；内部类使用protected修饰，限定为本外部类及父子类使用；内部类使用default修饰，限定为同包使用；内部类使用public修饰，任何位置均可使用。

#### 43、内部类：

非静态内部类不能拥有静态成员：

**静态内部类和非静态内部类一样，都不会因为外部内的加载而加载，同时静态内部类的加载不需要依附外部类，在使用时才加载，不过在加载静态内部类的过程中也会加载外部类**

首先内部类作为外部类的一个非静态成员，它的加载必须有外部类的对象实例（此时非静态成员已经加载），而当你加载该对象实例的时候，内部类里的静态成员并未被加载，这就违背了“所有的静态变量必须在所有的非静态变量之前加载”这一原则，所以这本身就是一个矛盾。而如果内部类是静态的话，就不会存在该矛盾了，因为访问Class Inner 是不需要Class Outer的实例的。

**大部分时候，内部类都被作为成员内部类定义，而不是作为局部内部类**。成员内部类是一种与成员变量、方法、构造器和初始化块相似的类成员；局部内部类和匿名内部类则不是类成员。

如果外部类成员变量、内部类成员变量与内部类里方法的局部变量同名，则可通过使用外部类类名.this 、 this作为限定区分。

**如果存在一个非静态内部类对象，则一定存在一个被它寄生的外部类对象**（非静态内部类对象里必须有一个外部类对象的引用）。但是外部类对象存在时，外部类对象里不一定寄生了非静态内部类对象。**因外部类对象访问非静态内部类成员时，可能非静态内部类对象根本不存在！而非静态内部类对象访问外部类成员时，外部类对象一定存在。**



**静态内部类对象不是寄生在外部类的实例中，而是寄生在外部类的类本身中**。当静态内部类对象存在时，并不存在一个被它寄生的外部类对象，静态内部类对象只有外部类的类引用，没有外部类对象的引用。

外部类不能**直接访问**静态内部类或者非静态内部类的成员（相当于外部类的一个方法，需要主语？？用修饰符修饰的内部类访问权限，也于正常方法一样）。内部类也不能被重写，因为内部类类名把外部类类名作为一个命名空间，这样子类中的同名的内部类，也不会与父类中的内部类完全同名，也就不可能被重写。

#### 44、使用内部类：

在外部类以外的地方定义内部类（包括静态和非静态两种）变量的语法格式如下：

`OuterClass.InnerClass   varName` 

在外部类以外的地方使用内部类时，内部类的完整类名是 OuterClass.InnerClass

由于非静态内部类的对象必须寄生在外部类的对象里，因此**创建非静态内部类对象**之前，必须先创建其外部类对象，语法如下：

`OuterInstance. new InnerConstructor()`   //**用外部类实例和 new 来调用非静态内部类的构造器**。

在外部类以外的地方**创建静态内部类对象**：

`new OuterClass.InnerConstructor()`



两者声明变量的语法一样，区别只是在创建内部类对象时，静态内部类只需使用外部类即可调用构造器，而非静态内部类必须使用外部类对象来调用构造器。

相比之下，使用静态内部类比使用非静态内部类要简单很多，只要把外部类当成静态内部类的包空间即可。因此当程序需要使用内部类时，应该优先考虑使用静态内部类。

#### 45、局部内部类（鸡肋，很少使用）：

把一个内部类方法方法里定义，则这个内部类就是一个局部内部类，局部内部类仅仅在该方法里有效。由于只能在方法内使用，所以局部内部类也不能使用访问控制符和static修饰。

（对于局部成员而言，不管是局部变量还是局部内部类，它们的上一级程序单元都是方法，而不是类，使用static 修饰它们没有任何意义。因此，所有的局部成员都不能使用static修饰。static 决定是属于类还是属于对象）

#### 46、匿名内部类（也是一种局部内部类）：

适合创建只需要一次使用的类，**匿名内部类必须继承一个父类，或实现一个接口**，但最多只能继承一个父类，或实现一个接口。而且不能定义构造器。

new  实现接口() | 父类构造器（实参列表）

{

​    //匿名内部类的类体部分

}

在Java 8之前，Java要求局部内部类、匿名内部类**访问的局部变量**必须使用 final修饰，从Java8开始这个限制被取消了，Java8更加智能：如果局部变量被匿名内部类访问，那么该局部变量相当于自动使用了 final修饰。

**用final修饰实际上就是为了保护数据的一致性。**

因为将数据拷贝完成后，如果不用final修饰，则原先的局部变量可以发生变化。这里到了问题的核心了，如果局部变量发生变化后，匿名内部类是不知道的（因为他只是拷贝了局部变量的值，并不是直接使用的局部变量）。那么程序再接着运行下去，可能就会导致程序运行的结果与预期不同。

#### 48、枚举类

一个类的对象是有限且固定的，在Java里被称为枚举类。

| 枚举类特点                                                   |
| :----------------------------------------------------------- |
| 使用enum定义的枚举类默认继承了 Java.lang.Enum类，因此枚举类不能显式继承其他父类。其中 Java.lang.Enum类实现了Java.lang.Serializable 和 Java.lang.Comparable 两个接口。 |
| 使用enum定义、非抽象的枚举类默认会使用final修饰，因此枚举类不能派生子类。 |
| 枚举类的构造器只能使用private访问控制符，如果省略了构造器的访问控制符，则默认使用private修饰。 |
| 枚举类的所有实例必须在枚举类的第一行显式列出，否则这个枚举类永远都不能产生实例。列出这些实例时，系统会自动添加 public static final 修饰，无须程序员显式添加。 |

枚举类默认提供了一个values()方法，该方法可以很方便地遍历所有的枚举值，返回值是枚举类型的数组。

```java
public enum Season {
    //在第一行列出4个枚举实例
    SPRING(1, "spring"), SUMMER(2, "summer"), FALL(3, "fall"), WINTER(4, "winter");
    private int code;
    private String msg;
    private Season(int num, String name) {
       this.code = num;
       this.msg = name;
    }
}
```

使用：Season.SPRING

#### 49、对象与垃圾回收

1. 垃圾回收机制只负责堆内存中的对象，不会回收任何物理资源。（例如数据库连接、网络IO等资源）

2. 程序无法精确控制垃圾回收的运行，垃圾回收会在合适的时候进行。当对象永久性地失去引用后，系统就会在合适的时候回收它所占的内存。

3. 在垃圾回收机制回收任何对象之前，总会先调用它的 finalize() 方法，该方法可能使该对象重新复活（让一个引用变量重新引用该对象），从而导致垃圾回收机制取消回收。

   ![image-20210926203729425](C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20210926203729425.png)

强制系统进行垃圾回收——这种强制只是通知系统进行垃圾回收，但是系统是否进行垃圾回收依然不确定。大部分时候，程序强制系统垃圾回收后总是会有一些效果。强制系统垃圾回收有如下两种方式：

1. 调用System 类的 gc() 静态方法：System.gc() 。
2. 调用Runtime 对象的 gc() 实例方法：Runtime.getRuntime().gc() 。

#### 50、Scanner 类

Scanner类提供了多个构造器，不同的构造器可以接收文件（File 对象）、输入流（Inputstream）、字符串（String）作为数据源。

Scanner 使用空格、tab、换行（'\n'或"\r\n"或'\r'）作为多个输入项之间的分隔符

Scanner主要提供了两个方法来扫描输入。

1. hasNextXxx() ：是否还有下一个输入项，其中Xxx可以是Int、Long等代表基本数据类型的字符串。如果只是判断是否包含下一个字符串，则直接使用 hasNext() 。
2. nextXxx()：获取下一个输入项。

逐行读取：

1. boolean hasNextLine() ：返回输入源中是否还有下一行。
2. String nextLine() : 返回输入源中下一行的字符串。

Scanner 的读取操作可能被阻塞（当前执行顺序流暂停）来等待信息的输入。

#### 51、System

System.currentTimeMillis();   返回一个long型整数，是当前时间与UTC 1970年一月一日的时间差，以毫秒为单位。

System.identityHashCode(Object x) , 该方法返回指定对象的精确hashCode值，也就是根据该对象的地址计算得到的hashCode值，即使该对象的hashCode方法被重写。

#### 52 、Object类

Object类提供的 clone() 方法使用了protected 修饰，因此该方法只能被子类重写或调用。

自定义类实现“克隆”的步骤如下：

1. 自定义类实现 Cloneable 接口。这是一个标记性的接口，实现该接口的对象可以实现“自我克隆”，接口里没有定义任何方法。
2. 自定义类实现自己的 clone() 方法，通过super.clone() ; 调用Object实现的clone() 方法来得到该对象的副本。

```java
public class Demo4 implements Cloneable{
    protected Demo4 clone() throws CloneNotSupportedException{
        return  (Demo4) super.clone();
    }
}
```

Object 类提供的 Clone 机制只对对象里各实例变量进行“简单复制”，对于引用变量也只是简单地复制这个引用变量，“浅克隆”。

#### 53、StringBuilder和 StringBuffer类

实际上，StringBuilder和 StringBuffer基本相似，两个类的构造器和方法也基本相同。不同的是，StringBuffer是线程安全的，而StringBuilder则没有实现线程安全功能，所以性能略高。因此在通常情况下，如果需要创建一个内容可变的字符串对象，则应该优先考虑使用StringBuilder类。

String 的 int compareTo(String anotherString) 方法 : 以ASCII码表的值作为比较，返回第一个不相等的字符差。另一种情况，较长字符串的前面部分恰巧是较短的字符串，则返回它们的长度差。

#### 54 、Random类

Random类专门用于生成一个伪随机数，它有两个构造器：一个构造器使用默认的种子（以当前时间作为种子），另一个构造器需要程序员显式传入一个long型整数的种子。

如果Random类的两个实例是用同一个种子创建的，怼他们以同样的顺序调用方法（nextInt、nextDouble）,则它们会产生相同的数字序列。

#### 55、BigDecimal

当程序使用new BigDecimal(0.1) 来创建一个BigDecimal 对象时，它的值并不是0.1，它实际上等于一个近似0.1的数。这是因为0.1无法准确地表示为double 浮点数。

使用BigDecimal(String val) 构造器的结果是可以预知的，它正好等于预期的0.1，因此通常建议优先使用基于String的构造器。

#### 56、Date类与Calendar类：

推荐使用Calendar。

Calendar类是一个抽象类，所以不能使用构造器来创建Calendar对象。但它提供了几个静态 getInstance() 方法来获取Calendar对象，这些方法根据TimeZone，Locale类来获取特定的Calendar，如果不指定TimeZone、Locale，则使用默认的TimeZone、Locale来创建Calendar。

Calendar类中的很多方法都需要一个int类型的field参数，field是Calendar类的类变量，如Calendar.YEAR、Calendar.MONTH等分别代表了年、月、日、小时、分钟、秒等时间字段。需要指出的是，Calendar.MONTH字段代表月份，月份的起始值不是1，而是0，所以要设置8月时，用7而不是8。如下程序示范了Calendar类的常规用法。

```java
// 使用默认时区和语言环境获得一个日历
Calendar cal = Calendar.getInstance();
// 赋值时年月日时分秒常用的6个值，注意月份下标从0开始，所以取月份要+1
//Calendar.YEAR相当于数组下标（看源码）
System.out.println("年:" + cal.get(Calendar.YEAR));
System.out.println("月:" + (cal.get(Calendar.MONTH) + 1));
System.out.println("日:" + cal.get(Calendar.DAY_OF_MONTH));
System.out.println("时:" + cal.get(Calendar.HOUR_OF_DAY));
System.out.println("分:" + cal.get(Calendar.MINUTE));
System.out.println("秒:" + cal.get(Calendar.SECOND));
```

**Calendar和Date转换：**

 Date now = calendar.getTime();       

 calendar.setTime(now);

#### 57、Java 8新增的日期、时间包

Java 8 专门新增了一个Java.time包，该包下包含了如下常用的类：

LocalDate: 该类表示不带时区的日期，例如 2007-12-03。 

LocalTime: 该类代表不带时区的时间，例如 10:16:23。

LocalDateTime :该类表示不带时区的日期、时间。

以上三个类都是提供了静态的now() 方法来获取当前日期、时间。

Clock :该类用于获取指定时区的当前日期、时间。

#### 58、正则表达式

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20210928213300679.png" alt="image-20210928213300679" style="zoom: 200%;" />

**？、+、*这些数量表示符会一直匹配下去，属于贪婪模式，尽可能多的匹配。**

`“\u0041\\\\”`  这个正则表达式表示匹配 A\ , **因为Java中 \ 需要用 `\\`来表示**，然后正则表示式就是表示成`“\u0041\\”`。

**转义字符，使后一个字符改变原来的意思**。

假如你需要匹配文本中的字符”\“，那么使用编程语言表示的正则表达式里将需要 4 个反斜杠”\\\\\\\\“：前两个和后两个分别用于在**编程语言**里转义成反斜杠，转换成两个反斜杠后再在**正则表达式**里转义成一个反斜杠。

其实和linux中差不多，要经过两层，一层是java编译器，一层是正则表达式处理过程。一个反斜杠具有转义的作用，比如’\t‘ 表示制表符，两个反斜杠，用第一个反斜杠取消第二个反斜杠的转义作用，使第二个反斜杠回归本身，就是一个反斜杠字符。

![image-20210928214043986](C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20210928214043986.png)

![image-20210928220202909](C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20210928220202909.png)

​                       **注意方括号匹配的都是字符**



Pattern对象是正则表达式编译后在内存中的表示形式，因此，正则表达式字符串必须先被编译为Pattern对象，然后再利用该Pattern对象创建对应的Matcher对象(匹配器)。执行匹配所涉及的状态保留在Matcher对象中，多个Matcher对象可共享同一个Pattern对象。

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20210928222301299.png" alt="image-20210928222301299" style="zoom:67%;" />

```java
//将一个字符串编译成Pattern对象
Pattern p = Pattern.compile("a*b");
Matcher m = p.matcher("aabccsdasaabaaaaab");
while(m.find()){
    System.out.println(m.group());
    System.out.println(m.start());
    System.out.println(m.end());
}
```



matches() 和lookingAt() 方法有点相似，只是matches() 方法要求整个字符串和Pattern完全匹配时才返回true，而lookingAt() 只要字符串以Pattern 开头就会返回true。

事实上String类里也提供了matches()方法 ，还有利用正则表达式的replaceAll() 方法、 replaceFirst()方法和 split(String regex) 方法。

#### 59、集合类

集合类和数组不一样，数组元素既可以是基本类型的值，也可以是对象（实际上保存的是对象的引用变量）；而集合里只能保存对象（实际上只是保存对象的引用变量，但通常习惯上认为集合里保存的是对象）。

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20210929165648724.png" alt="image-20210929165648724" style="zoom:67%;" />

![image-20210929165849330](C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20210929165849330.png)

Map 里的 key 是不能重复的。需要根据每项元素的key来访问其 value。（就跟函数一样）

Iterator 接口隐藏了各种Collection实现类的底层细节，向应用程序提供了**遍历Collection集合元素的统一编程接口**。Iterator接口里定义了如下4个方法。
>boolean hasNext（）：如果被迭代的集合元素还没有被遍历完，则返回true。
>Object next()：返回集合里的下一个元素。
>void remove()：删除集合里上一次next方法返回的元素。
>void forEachRemaining（Consumer action），这是Java8为Iterator新增的默认方法，该方法可使用Lambda表达式来遍历集合元素。

```java
Collection c = new ArrayList();
Iterator it = c.iterator();
```

迭代器是工作在一个独立的线程中，并且拥有一个mutex锁，就是说iterator在工作的时候，是不允许被迭代的对象被改变的 (**只允许自己改**是吧！！！) 。也是相当于把对象的引用复制一份。

modCount 是 ArrayList 继承自 AbstractList 的一个变量，modCount 为 list 的结构变化次数，即 list 的元素数量变化次数。查看 ArrayList 的源码，会发现在每次调用 add() 和 remove() 方法，都会进行 modCount++ 操作。

而 expectedModCount 可被视为 Itr 内部记录的集合结构变化次数，当集合的实际结构变化次数 和 Itr 记录的变化次数不相等时，则抛出 ConcurrentModificationException 异常。而在 Itr 的 next() 方法 和 remove() 中都调用了 checkForComodification 方法，来检测两个变化次数是否一致。

为什么使用 Iterator 的 remove 方法操作集合元素不会有问题？

实际上，调用 Itr 的 remove() 方法移除集合元素时，首先会调用 ArrayList 的 remove() 方法，再对 expectedModCount 进行更新。在下次调用 Itr.next() 方法获取下个元素时，不会出现 expectedModCount != modCount 的情况。

Iterator 为什么要检查集合的结构变化次数?

这其实是为了**防止多线程并发修改集合**，在一个线程遍历集合的同时，另一个线程同时增删集合元素，**将无法保证数据的一致性**，集合的遍历过程也将被打乱。采用 modCount 机制，在此情景下及时抛出异常，确保同一时间只会有一个线程修改或遍历集合，也即 fail-fast 策略。

**foreach 循环内部实际是通过 Iterator 实现的。**

#### 60、Set集合

Set集合与 Collection 基本相同，没有提供任何额外的方法，只是行为略有不同（Set不允许包含重复元素）。

#### 61、HashSet类

HashSet 是Set 接口的典型实现，大多数时候使用Set集合时就是使用这个实现类。HashSet集合判断两个元素相等的标准是两个对象通过 equals() 方法比较相等，并且两个对象的 hashCode() 方法返回值也相等。

规则是：如果两个对象通过 equals() 方法比较返回true，这两个对象的 hashCode 值也应该相同。

当程序把可变对象添加到HashSet中之后，尽量不要去修改该集合元素中参与计算hashCode()、equals() 的实例变量，否则将会导致HashSet无法正确访问这些集合元素。虽然修改了集合元素，但是存储位置没变，这个修改后的元素依然放在原来的“桶”里。（判断这个修改元素是否存在时，若采用新hashCode值，则找不到该元素；若采用旧的hashCode值，则equals() 方法不匹配，不能视为相等的元素，还是无法正确访问到）

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211009210736787.png" alt="image-20211009210736787" style="zoom:67%;" />



形式：数组+链表。在发生”hash冲突“时，单个桶会存储多个元素，这些元素以链表形式存储，必须按顺序搜素。

#### 62、LinkedHashSet类

HashSet 还有一个子类LinkedHashSet，LinkedHashSet集合也是根据元素的hashCode值来决定元素的存储位置，**但它同时使用链表维护元素的次序，这样使得元素看起来是以插入的顺序保存的**。也就是说，当遍历LinkedHashSet集合里的元素时，**LinkedHashSet将会按元素的添加顺序来访问集合里的元素。**

#### 63、TreeSet类

与HashSet集合采用hash算法来决定元素的存储位置不同，TreeSet采用红黑树的数据结构来存储集合元素。

如果向TreeSet中添加一个可变对象后，并且后面程序修改了该可变对象的实例变量，这将导致它与其他对象的大小顺序发生了改变，但TreeSet不会再次调整它们的顺序，

TreeSet支持两种排序方法：自然排序和定制排序。在默认情况下，TreeSet采用自然排序。

1. 自然排序

   TreeSet会调用集合元素的compareTo（Object obj）方法来比较元素之间的大小关系，然后将集合元素按升序排列，这种方式就是自然排序。

   对于TreeSet集合而言，**它判断两个对象是否相等的唯一标准是：两个对象通过compareTo（Object obj）方法比较是否返回0**——如果通过compareTo（Object obj）方法比较返回0，TreeSet则会认为它们相等；否则就认为它们不相等。

   Java提供了一个Comparable接口，该接口里定义了一个compareTo（Object obj）方法，该方法返回一个整数值，实现该接口的类必须实现该方法，实现了该接口的类的对象就可以比较大小。

   如果试图把一个对象添加到TreeSet时，则该对象的类必须实现Comparable接口，否则程序将会抛出异常。

   ![image-20211006154205104](C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211006154205104.png)

2. 定制排序

   如果需要实现定制排序，则需要在创建 TreeSet集合对象时，提供一个Comparator对象与该TreeSet集合关联，由该Comparator对象负责集合元素的排序逻辑。

   Comparator接口里包含一个int compare(T o1 ,T o2)方法，用于比较o1和o2的大小。

   通过compare方法判断相等。

#### 64、各Set实现类的性能分析

HashSet和TreeSet是Set的两个典型实现，到底如何选择HashSet和TreeSet呢？HashSet的性能总是比TreeSet好（特别是最常用的添加、查询元素等操作），因为TreeSet需要额外的红黑树算法来维护集合元素的次序。只有当需要一个保持排序的Set时，才应该使用TreeSet，否则都应该使用HashSet。

HashSet 还有一个子类：LinkedHashSet，对于普通的插入、删除操作，LinkedHashSet比 HashSet要略微慢一点，这是由维护链表所带来的额外开销造成的，但由于有了链表，遍历LinkedHashSet会更快。

**EnumSet是所有Set实现类中性能最好的，但它只能保存同一个枚举类的枚举值作为集合元素。**

必须指出的是，Set的三个实现类HashSet、TreeSet和EnumSet都是线程不安全的。如果有多个线程同时访问一个Set集合，并且有超过一个线程修改了该Set集合，则必须手动保证该Set集合的同步性。通常可以通过Collections工具类的synchronizedSet 方法来“包装”该Set集合。此操作最好在创建时进行，以防止对Set集合的意外非同步访问。

#### 65、List集合

List集合代表一个元素有序、可重复的集合，集合中每个元素都有其对应的顺序索引。List可以通过索引来访问指定位置的集合元素。

因此List增加了一种新的遍历集合元素的方法：使用普通的for循环来遍历集合元素。

```java
for(int i=0; i< books.size(); i++){
    System.out.print1n(books.get(i));
}
```

**List 判断俩个对象相等只要通过 equals() 方法比较返回 true 即可。**

```java
List books=new ArrayList();
books.add(new String（"轻量级 Java EE企业应用实战”))；
books.add(new String（"疯狂Java讲义"))；
books.add(new String（"疯狂Android讲义”))；
system.out.println(books)；
//删除集合中的A对象，将导致第一个元素被删除
books.remove(new A()); //A里面equals方法永远返回true
```

**执行remove代码时，程序试图删除一个A对象，List将会调用该A对象的 equals() 方法依次与集合元素进行比较**，如果该equals() 方法以某个集合元素作为参数时返回true，List将会删除该元素。

#### 66、ListIterator 

与 Set 只提供了一个 iterator() 方法不同 ( hasNext、next、remove )，List 还额外提供了一个 listlterator() 方法，该方法返回一个Listlterator 对象，Listlterator 接口继承了Iterator接口，提供了专门操作List的方法。Listlterator接口在Iterator接口基础上增加了如下方法。
>boolean hasPrevious()：返回该迭代器关联的集合是否还有上一个元素。
>
>Object previous() ：返回该迭代器的上一个元素。
>
>void add(Object o) ：在指定位置插入一个元素。
>

拿Listlterator 与普通的Iterator 进行对比，不难发现ListIterator增加了向前迭代的功能（Iterator只能向后迭代），而且Listlterator还可通过 add() 方法向List集合中添加元素（Iterator只能删除元素）。

#### 67、ArrayList 和 Vector 实现类

ArrayList 和 Vector 类都是基于数组实现的List类，所以ArrayList和Vector类封装了一个动态的、允许再分配的 Object[] 数组。ArrayList 或 Vector 对象使用 initialCapacity 参数来设置该数组的长度，当向ArrayList 或Vector中添加元素超出了该数组的长度时，它们的 initialCapacity 会自动增加，默认为10。

实际上，Vector 具有很多缺点，通常尽量少用 Vector 。

除此之外，ArrayList和Vector的显著区别是：ArrayList是线程不安全的，当多个线程访问同一个ArrayList集合时，如果有超过一个线程修改了ArrayList集合，则程序必须手动保证该集合的同步性；但Vector集合则是线程安全的。

实际上，即使需要保证List集合线程安全，也同样不推荐使用Vector实现类。后面会介绍一个Collections工具类，它可以将一个ArrayList变成线程安全的。

#### 68、固定长度的List

​      前面讲数组时介绍了一个操作数组的工具类：Arrays，该工具类里提供了asList（Object... a）方法，该方法可以把一个数组或指定个数的对象转换成一个List集合，这个List集合既不是 ArrayList 实现类的实例，也不是 Vector 实现类的实例，**而是Arrays的内部类ArrayList的实例**。
​       **Arrays.ArrayList是一个固定长度的List集合**，程序只能遍历访问该集合里的元素，**不可增加、删除该集合里的元素**。

#### 69、Queue集合

Queue用于模拟队列这种数据结构，队列通常是指“先进先出”（FIFO）的容器。

Queue接口中定义了如下几个方法。
>void add(Object e) ：将指定元素加入此队列的尾部。
>Object element() ：获取队列头部的元素，但是不删除该元素。
>boolean offer（Object e）：将指定元素加入此队列的尾部。当使用有容量限制的队列时，此方法通常比add（Object e）方法更好。
>Object peek() ：获取队列头部的元素，但是不删除该元素。如果此队列为空，则返回null。
>Object poll() ：获取队列头部的元素，并删除该元素。如果此队列为空，则返回null。
>Object remove() ：获取队列头部的元素，并删除该元素。

Queue 接口有一个PriorityQueue实现类。除此之外，Queue还有一个Deque接口，Deque代表一个
“双端队列”，双端队列可以同时从两端来添加、删除元素，因此Deque的实现类既可当成队列使用，也可当成栈使用。Java为Deque提供了ArrayDeque和LinkedList 两个实现类。

#### 70、PriorityQueue 实现类

PriorityQueue是一个比较标准的队列实现类。之所以说它是比较标准的队列实现，而不是绝对标准的队列实现，是因为**PriorityQueue保存队列元素的顺序并不是按加入队列的顺序，而是按队列元素的大小进行重新排序**。因此当调用 peek() 方法或者 poll() 方法取出队列中的元素时，并不是取出最先进入队列的元素，而是取出队列中最小的元素。从这个意义上来看，PriorityQueue已经违反了队列的最基本规则：先进先出（FIFO）。



直接输出 PriorityQueue 集合时，可能看到该队列里的元素并没有很好地按大小进行排序，但这只是受到 PriorityQueue 的 toString() 方法的返回值的影响。实际上，程序多次调用 PriorityQueue 集合对象的 poll() 方法，即可看到元素按从小到大的顺序“移出队列”。



**PriorityQueue不允许插入null元素，它还需要对队列元素进行排序**，PriorityQueue的元素有两种排序方式。

>自然排序：采用自然顺序的 PriorityQueue 集合中的元素必须实现了Comparable接口，而且应该是同一个类的多个实例，否则可能导致ClassCastException异常。
>定制排序：创建 PriorityQueue 队列时，传入一个Comparator对象，该对象负责对队列中的所有元素进行排序。采用定制排序时不要求队列元素实现Comparable接口。

PriorityQueue 队列对元素的要求与 TreeSet 对元素的要求基本一致，因此关于使用自然排序和定制排序的详细介绍参考上面。

#### 71、Deque接口

Deque接口是 Queue 接口的子接口，它代表了一个双端队列，也可以被当成栈使用（队列头部，相当于栈的顶部）

>void addFirst（Object e）：将指定元素插入该双端队列的开头。
>
>void addLast（Object e）：将指定元素插入该双端队列的末尾。
>
>Iterator descendinglterator() ：返回该双端队列对应的迭代器，该迭代器将以逆向顺序来迭代队列中的元素。
>
>Object getFirst() ：获取但不删除双端队列的第一个元素。
>
>Object getLast() ：获取但不删除双端队列的最后一个元素。
>
>boolean offerFirst（Object e）：将指定元素插入该双端队列的开头。
>
>boolean offerLast（Object e）：将指定元素插入该双端队列的末尾。
>
>Object peekFirst()：获取但不删除该双端队列的第一个元素；如果此双端队列为空，则返回null。
>
>Object peekLast()：获取但不删除该双端队列的最后一个元素；如果此双端队列为空，则返回null。
>
>Object pollFirst() ：获取并删除该双端队列的第一个元素；如果此双端队列为空，则返回null。
>
>Object pollLast() ：获取并删除该双端队列的最后一个元素；如果此双端队列为空，则返回null。
>
>Object pop()（栈方法）：pop出该双端队列所表示的栈的栈顶元素。相当于removeFirst()。
>
>void push(Object e)（栈方法）：将一个元素push进该双端队列所表示的栈的栈顶。相当于addFirst（e）。
>
>Object removeFirst() ：获取并删除该双端队列的第一个元素。
>Object removeFirstOccurrence（Object o）：删除该双端队列的第一次出现的元素o。
>Object removeLast() ：获取并删除该双端队列的最后一个元素。
>boolean removeLastOccurrence（Object o）：删除该双端队列的最后一次出现的元素o。

#### 72、ArrayDeque 实现类

Deque 接口提供了一个典型的实现类：ArrayDeque，从该名称就可以看出，它是一个基于数组实现的双端队列，创建Deque时同样可指定一个 numElements 参数，该参数用于指定 Object[] 数组的长度；如果不指定numElements参数，Deque底层数组的长度为16。

**当需要使用栈时，推荐用ArrayDeque**。

#### 73、LinkedList 实现类

LinkedList类是List接口的实现类——这意味着它是一个List集合，可以根据索引来随机访问集合中的元素。

除此之外，LinkedList还实现了Deque接口，可以被当成双端队列来使用，因此既可以被当成“栈”来使用，也可以当成队列使用。由此可见，LinkedList 是一个功能非常强大的集合类。

LinkedList与ArrayList、ArrayDeque的实现机制完全不同，ArrayList、ArrayDeque内部以数组的形式来保存集合中的元素，因此随机访问集合元素时有较好的性能；而LinkedList内部以链表的形式来保存集合中的元素，因此随机访问集合元素时性能较差，但在插入、删除元素时性能比较出色。需要指出的是，虽然Vector也是以数组的形式来存储集合元素的，但因为它实现了线程同步功能（而且实现机制也不好），所以各方面性能都比较差

#### 74、各种线性表的性能分析

Java提供的List 就是一个线性表接口，而ArrayList、LinkedList又是线性表的两种典型实现：基于数组的线性表和基于链的线性表。

Queue代表了队列，Deque代表了双端队列（既可作为队列使用，也可作为栈使用），接下来对各种实现类的性能进行分析。

初学者可以无须理会ArrayList和LinkedList之间的性能差异，只需要知道LinkedList集合不仅提供了List的功能，还提供了双端队列、栈的功能就行。但对于一个成熟的Java程序员，在一些性能非常敏感的地方，可能需要慎重选择哪个List实现。

一般来说，由于数组以一块连续内存区来保存所有的数组元素，所以**数组在随机访问时性能最好**，所有的内部以数组作为底层实现的集合在随机访问时性能都比较好；而内部以**链表作为底层实现的集合在执行插入、删除操作时有较好的性能**。

但总体来说，ArrayList的性能比LinkedList的性能要好，因此大部分时候都应该考虑使用ArrayList。

关于使用List集合有如下建议。

1. 如果需要遍历List集合元素，对于 ArrayList 集合，应该使用随机访问方法（get）来遍历集合元素，这样性能更好；对于LinkedList集合，则应该采用迭代器（Iterator）来遍历集合元素。
2. 如果需要经常执行插入、删除操作来改变包含大量数据的List集合的大小，可考虑使用LinkedList集合。使用 ArrayList 集合可能需要经常重新分配内部数组的大小，效果可能较差。
3. 如果有多个线程需要同时访问List集合中的元素，开发者可考虑使用Collections将集合包装成线程安全的集合。

#### 75、Map 集合

如果把Map里的所有key放在一起来看，它们就组成了一个Set集合（所有的key没有顺序，key与key之间不能重复），实际上Map 确实包含了一个 keySet() 方法，用于返回Map里所有key组成的Set集合。

不仅如此，Map里key集和Set集合里元素的存储形式也很像，Map子类和Set子类在名字上也惊人地相似，比如Set接口下有HashSet、LinkedHashSet、SortedSet（接口）、TreeSet、EnumSet等子接口和实现类，而Map接口下则有HashMap、LinkedHashMap、SortedMap（接口）、TreeMap、EnumMap等子接口和实现类。正如它们的名字所暗示的，Map的这些实现类和子接口中**key集的存储形式和对应Set集合中元素的存储形式完全相同**。

Set与Map之间的关系非常密切。虽然Map中放的元素是key-value对，Set集合中放的元素是单个对象，但如果把key-value对中的value当成key的附庸：key在哪里，value就跟在哪里。这样就可以像对待Set一样来对待Map了。**事实上，Map提供了一个Entry内部类来封装key-value对，而计算Entry存储时则只考虑Entry封装的key。从Java源码来看，Java是先实现了Map，然后通过包装一个所有value都为null的Map就实现了Set集合。**

如果把Map里的所有value放在一起来看，它们又非常类似于一个List：元素与元素之间可以重复，每个元素可以根据索引来查找，只是Map中的索引不再使用整数值，而是以另一个对象作为索引。

Map中包括一个内部类Entry，该类封装了一个key-value对。Entry包含如下三个方法。
>Object getKey（）：返回该Entry里包含的key值。
>Object getValue（）：返回该Entry里包含的value值。
>Object setValue（V value）：设置该Entry里包含的value值，并返回新设置的value值。

```java
HashMap<String,Integer> map = new HashMap<>();
map.put("疯狂",1);
map.put("java",2);
map.put("讲义",3);
map.put("真的好",4);

//两种遍历map的方法
for(Map.Entry<String,Integer> entry: map.entrySet()) {
    System.out.println(entry.getKey()+"->"+entry.getValue());
}
System.out.println("------------------");

for(String key : map.keySet()){
    System.out.println(key+"->"+map.get(key));
}
System.out.println("------------------");

map.forEach((k,v)-> System.out.println(k+"->"+v));
System.out.println("------------------");
map.forEach((k,v)-> {
    System.out.println(k+"->"+v);
    //随便写的，只是说明如果是代码块的话，就用大括号括起来
});
```

#### 76、HashMap 和 Hashtable 实现类

HashMap和Hashtable都是Map接口的典型实现类，它们之间的关系完全类似于ArrayList和Vector的关系。Hashtable 是一个线程安全的Map 实现，但HashMap是线程不安全的实现。

由于HashMap 里的key不能重复，所以HashMap 里最多只有一个 key-value 对的 key 为 null，但可以有无数多个 key-value 对的 value 为null。

类似于HashSet，HashMap、Hashtable判断两个key相等的标准也是：两个key通过equals ()方法比较返回true，两个key的 hashCode 值也相等, 所以用作 key 的对象必须实现 hashCode() 方法 和 equals() 方法。

除此之外，HashMap 、Hashtable 中还包含一个containsValue() 方法，那么HashMap、Hashtable如何判断两个value相等呢？**HashMap**、Hashtable**判断两个value相等**的标准更简单：**只要两个对象通过 equals() 方法比较返回true即可**。

**与HashSet类似的是，尽量不要使用可变对象作为HashMap、Hashtable的key，如果确实需要使用可变对象作为HashMap、Hashtable的key，则尽量不要在程序中修改作为key的可变对象。**修改后，程序可能再也无法准确访问到 Map 中被修改过的 key 。

**HashMap 在决定元素存储位置时，只考虑key。**

（你以为修改后，会重新计算hashCode值并更换到新的存储地址，但其实他没有这么做）

#### 77、LinkedHashMap 实现类

LinkedHashMap 是 HashMap 的子类，使用双向链表来维护 key-value 对的次序（其实也只考虑 key 的次序），该链表负责维护Map的迭代顺序，迭代顺序与 key-value 对的插入顺序保持一致。

**最大的作用是保持插入顺序。**

#### 78、Java Properties类

  Java中有个比较重要的类Properties（Java.util.Properties），**主要用于读取Java的配置文件**，各种语言都有自己所支持的配置文件，配置文件中很多变量是经常改变的，这样做也是为了方便用户，让用户能够脱离程序本身去修改相关的变量设置。像Python支持的配置文件是.ini文件，同样，它也有自己读取配置文件的类ConfigParse，方便程序员或用户通过该类的方法来修改.ini配置文件。在Java中，其配置文件常为.properties文件，格式为文本文件，文件的内容的格式是“键=值”的格式，文本注释信息可以用"#"来注释。

Properties 相当于一个key、value都是String类型的Map。

它提供了几个主要的方法：

1.  String getProperty ( String key)，用指定的键在此属性列表中搜索属性。也就是通过参数 key ，得到 key 所对应的 value，类似于Map的 get(Object key) 方法。
2.  void load ( InputStream inStream)，从输入流中读取属性列表（键和元素对）。通过对指定的文件（比如说上面的 test.properties 文件）进行装载来获取该文件中的所有键 - 值对。以供 getProperty ( String key) 来搜索。
3.  Object setProperty ( String key, String value) ，调用 Hashtable 的方法 put 。他通过调用基类的put方法来设置 键 - 值对。
4.  void store ( OutputStream out, String comments)，以适合使用 load 方法加载到 Properties 表中的格式，将此 Properties 表中的属性列表（键和元素对）写入输出流。与 load 方法相反，该方法将键 - 值对写入到指定的文件中去。（comments：文件名）
5.  clear ()，清除所有装载的 键 - 值对。该方法在基类中提供。

#### 79、TreeMap 实现类

TreeMap 就是一个红黑树数据结构，每个 key-value 对即作为红黑树的一个节点。TreeMap存储key-value对（节点）时，需要根据key对节点进行排序。TreeMap可以保证所有的key-value对处于有序状态。TreeMap也有两种排序方式。
>自然排序：TreeMap的所有key必须实现Comparable接口，而且所有的key应该是同一个类的对象，否则将会抛出ClassCastException异常。
>
>定制排序：创建TreeMap时，传入一个Comparator对象，该对象负责对TreeMap中的所有key进行排序。采用定制排序时不要求Map的key实现 Comparable 接口。 

类似于TreeSet中判断两个元素相等的标准，TreeMap中判断两个key相等的标准是：两个key通过compareTo() 方法返回0，TreeMap 即认为这两个key是相等的。

如果使用自定义类作为TreeMap的key，且想让TreeMap良好地工作，则重写该类的 equals() 方法和compareTo() 方法时应保持一致的返回结果：两个key通过equals0方法比较返回true时，它们通过compareTo() 方法比较应该返回0。如果equals() 方法与compareTo() 方法的返回结果不一致，TreeMap与Map接口的规则就会冲突。

#### 80、WeakHashMap 实现类

HashMap的key保留了对实际对象的强引用，这意味着只要该HashMap 对象不被销毁，该HashMap的所有key所引用的对象就不会被垃圾回收。

但WeakHashMap 的key 只保留了对实际对象的弱引用，这意味着如果WeakHashMap 对象的key所引用的对象没有被其他强引用变量所引用，则这些key所引用的对象可能被垃圾回收。

#### 81、IdentityHashMap 实现类

这个Map实现类的实现机制与HashMap基本相似，但它在处理两个key相等时比较独特：在IdentityHashMap中，当且仅当两个key严格相等（key1==key2）时，IdentityHashMap 才认为两个key相等；对于普通的HashMap而言，只要keyl和key2通过equals() 方法比较返回true，且它们的hashCode值相等即可。

#### 82、EnumMap 实现类

EnumMap是一个与枚举类一起使用的Map实现，EnumMap中的所有key都必须是单个枚举类的枚举值。创建EnumMap时必须显式或隐式指定它对应的枚举类。

>EnumMap在内部以**数组形式**保存，所以这种实现形式非常紧凑、高效。
>
>EnumMap根据key的自然顺序（即枚举值在枚举类中的定义顺序）来维护key-value对的顺序。
>当程序通过keySet() 、entrySet() 、values() 等方法遍历EnumMap时可以看到这种顺序。
>
>EnumMap不允许使用null作为key，但允许使用null作为value。如果试图使用null作为key时将抛出NullPointerException异常。如果只是查询是否包含值为null的key，或只是删除值为null的key，都不会抛出异常。

EnumSet 与 EnumMap 类似，还是有些许不一样的，比如创建对象的方法。

#### 83、各 Map 实现类的性能分析

​       对于Map的常用实现类而言，虽然HashMap和Hashtable的实现机制几乎一样，但由于Hashtable是一个古老的、线程安全的集合，因此HashMap通常比Hashtable要快。

 	  TreeMap通常比HashMap、Hashtable 要慢（尤其在插入、删除key-value对时更慢），因为TreeMap底层采用红黑树来管理key-value对（红黑树的每个节点就是一个key-value对）。使用TreeMap有一个好处：TreeMap中的key-value对总是处于有序状态，无须专门进行排序操作。

​        当TreeMap被填充之后，就可以调用keySet() ，**取得由key组成的Set，然后使用toArray() 方法生成key的数组，接下来使用Arrays的binarySearch() 方法在已排序的数组中快速地查询对象**。

​        对于一般的应用场景，程序应该多考虑使用HashMap，因为HashMap正是为快速查询设计的（**HashMap底层其实也是采用数组来存储key-value对**）。但如果程序需要一个总是排好序的Map时，则可以考虑使用TreeMap。

​        LinkedHashMap 比HashMap慢一点，因为它需要维护链表来保持Map中key-value时的添加顺序。

​        IdentityHashMap性能没有特别出色之处，因为它采用与HashMap基本相似的实现，只是它使用==而不是equals() 方法来判断元素相等。EnumMap的性能最好，但它只能使用同一个枚举类的枚举值作为key。

#### 84、操作集合的工具类：Collections

1、Collections提供了如下常用的类方法用于对List集合元素进行排序。

>void reverse（List list）：反转指定List集合中元素的顺序。
>void shuffle（List list）：对List集合元素进行随机排序（shuffle方法模拟了“洗牌”动作）。
>void sort（List list）：根据元素的自然顺序对指定List集合的元素按升序进行排序。
>void sort（List list，Comparator c）：根据指定 Comparator产生的顺序对List集合元素进行排序。
>void swap（List list，int i，int j）：将指定List集合中的i处元素和j处元素进行交换。
>void rotate（List list，int distance）：当distance为正数时，将list集合的后distance个元素“整体”移到前面；当distance为负数时，将list集合的前distance个元素“整体”移到后面。该方法不会改变集合的长度。

2、Collections 还提供了如下常用的用于查找、替换集合元素的类方法。

>int binarySearch（List list，Object key）：使用二分搜索法搜索指定的List集合，以获得指定对象在List集合中的索引。如果要使该方法可以正常工作，则必须保证List中的元素已经处于有序状态。
>Object max（Collection coll）：根据元素的自然顺序，返回给定集合中的最大元素。
>Object max（Collection coll，Comparator comp）：根据Comparator指定的顺序，返回给定集合中的最大元素。
>Object min（Collection coll）：根据元素的自然顺序，返回给定集合中的最小元素。
>Object min（Collection coll，Comparator comp）：根据Comparator指定的顺序，返回给定集合中的最小元素。
>void fill（List list，Object obj）：使用指定元素 obj 替换指定List集合中的所有元素。
>int frequency（Collection c，Object o）：返回指定集合中指定元素的出现次数。
>int indexOfSubList（List source，List target）：返回子List对象在父List对象中第一次出现的位置索引；如果父List中没有出现这样的子List，则返回-1。
>int lastlndexOfSubList（List source，List target）：返回子List对象在父List对象中最后一次出现的位置索引；如果父List中没有出现这样的子List，则返回-1。
>boolean replaceAll（List list，Object oldVal，Object newVal）：使用一个新值newVal替换List对象的所有旧值oldVal。

元素的自然顺序——自定义类实现了Comparable接口。

3、同步控制

Collections类中提供了多个 synchronizedXxx() 方法，该方法可以将指定集合包装成线程同步的集合，从而可以解决多线程并发访问集合时的线程安全问题。
Java中常用的集合框架中的实现类HashSet、TreeSet、ArrayList、ArrayDeque、LinkedList、HashMap和TreeMap都是线程不安全的。如果有多个线程访问它们，而且有超过一个的线程试图修改它们，则存在线程安全的问题。Collections提供了多个类方法可以把它们包装成线程同步的集合。

```java
Collection c = Collections.synchronizedCollection(new ArrayList());
List list = Collections.synchronizedList(new ArrayList());
Set set = Collections.synchronizedSet(new HashSet());
Map map = Collections.synchronizedMap(new HashMap());
```

此时的 map 是类Collections$SynchronizedMap的对象。

4、设置不可变集合

Collections提供了如下三类方法来返回一个不可变的集合。
>emptyXxx() ：返回一个空的、不可变的集合对象，此处的集合既可以是List，也可以是SortedSet、Set，还可以是Map、SortedMap等。
>singletonXxx() ：返回一个只包含指定对象（只有一个或一项元素）的、不可变的集合对象，此处的集合既可以是List，还可以是Map。
>unmodifiableXxx() ：返回指定集合对象的不可变视图，此处的集合既可以是List，也可以是Set、SortedSet，还可以是Map、SorteMap等。

上面三类方法的参数是原有的集合对象，返回值是**该集合的“只读”版本**。

```java
 //创建一个空的、不可改变的List对象
 List unmodifiableList = Collections.emptyList();
 //创建一个只有一个元素，且不可改变的Set对象，如果是List或者Map,需要在singleton后面加 
 Set unmodifiableSet = Collections.singleton("疯狂Java讲义");
 //创建一个普通的Map对象
 Map scores =new HashMap();
 scores.put("语文",80);
 scores.put("数学",90);
 //返回普通的Map对象对应的不可变版本
 Map unmodifiableMap=Collections.unmodifiableMap(scores);
```

#### 85、泛型

java集合有个缺点——把一个对象“丢进”集合里之后，集合就会“忘记”这个对象的数据类型，当再次取出对象时，该对象的编译类型就变成了Object类型（其运行时类型没变）。(为了装下各种各样的对象)

Java7的菱形语法：

```java
List<String> strList = new ArrayList<>();
Map<String,Integer> scores = new HashMap<>();

//定义泛型类
public class A<E>{
    void add(E x);
    E next();
}
```

所谓泛型，就是允许在定义类、接口、方法时使用类型形参，类型形参在整个接口、类体内可当成类型使用。

为Apple<T> 类定义构造器，其构造器名依然是Apple，而不是Apple<T>

#### 86、从泛型类派生子类

当创建了带泛型声明的接口、父类之后，可以为该接口创建实现类，或从该父类派生子类，需要指出的是，当使用这些接口、父类时不能再包含类型形参，如：

```java
Public class A extends Apple<T>{} // 错
Public class A extends Apple<String>{} //对
```

也就是，定义类、接口、方法时可以声明类型形参，但是使用它们时应该为类型形参传入实际的类型。

#### 87、并不存在泛型类

事实上，ArrayList<String>类像一种特殊的ArrayList类：该ArrayList<String>对象只能添加String对象作为集合元素。但实际上，系统并没有为ArrayList<String>生成新的class文件，而且也不会把ArrayList<String>当成新类来处理。

```java
ArrayList<String> list1 = new ArrayList<>();
ArrayList<Integer> list2 = new ArrayList<>();
//结果是true，原理是泛型擦除，在运行时，jvm都视作ArrayListd
System.out.println(list1.getClass() == list2.getClass());

ArrayList list3 = new ArrayList();
System.out.println(list1.getClass() == list3.getClass());//结果也是true

// 都是java.util.ArrayList类
System.out.println(list1.getClass()); //输出：class java.util.ArrayList
System.out.println(list2.getClass()); //输出：class java.util.ArrayList
System.out.println(list3.getClass()); //输出：class java.util.ArrayList
```

不管为泛型的类型形参传入哪一种类型实参，对于Java 来说，它们依然被当成同一个类处理，在内存中也只占用一块内存空间。

```java
List<String> list1 = new ArrayList<>();
List<Object> list2 = list1; //编译报错，不能赋值
```

List<String>类并不是List<Object>类的子类。

如果Foo是Bar的一个子类型（子类或者子接口），G<Foo>并不是G<Bar>的子类型！这一点非常值得注意，因为它与大部分人的习惯认为是不同的。

#### 88、使用类型通配符

类型通配符是一个问号（？），写作List<?>  list ，这种带通配符的List 仅表示它是各种泛型List的父类，list中的元素类型是Object，这永远都是安全的。

但这种带通配符的List仅表示它是各种泛型List的父类，并不能把元素加入到其中。

```java
List<?> c = new ArrayList<String>();
//下面程序引起编译错误，编译不通过
c.add(new Object());
```

因为程序无法确定c集合中元素的类型，所以不能向其中添加对象。

根据前面的List<E>接口定义的代码可以发现：add() 方法有类型参数E作为集合的元素类型，所以传给add的参数必须是E类的对象或者其子类的对象。但因为在该例中不知道E是什么类型，所以程序无法将任何对象“丢进”该集合。

另一方面，程序可以调用get() 方法来返回 List<?> 集合指定索引处的元素，其返回值是一个未知类型，但可以肯定的是，它总是一个Object。因此，把get() 的返回值赋值给一个Object类型的变量，或者放在任何希望是Object类型的地方都可以。

**通配符上限**：

List<? extends Shape> 此处的问号代表一个未知的类型，但是这个未知类型一定是Shape的子类型（也可以是Shape本身），因此可以把Shape称为这个通配符的上限。

类似地，由于程序无法确定这个受限制的通配符的具体类型，所以不能把Shape对象或其子类的对象加入这个泛型集合中。

```java
public void add(List<? extends Shape> shapes){
  //下面代码引起编译错误
  shapes.add(0, new Rectangle());
  //Rectangle是Shape的一个子类
}
```

**设定类型形参的上限：**

Java 泛型不仅允许在使用通配符形参时设定上限，而且可以在定义类型形参时设定上限，用于表示传给该类型形参的实际类型要么是该上限类型，要么是该上限类型的子类。

`public class Apple<T extends Number>`

**通配符下限：**

Java 允许设定通配符的下限 ：<? super Type>，这个通配符表示它必须是Type本身，或是Type的父类。

#### 89、泛型方法

用法格式如下：

修饰符  <T，S>  返回值类型 方法名(形参列表){} ;

```java
public static <T> void fromArrayToCollection(T[] a, Collection<T> c){
	for(T o : a){
		c.add(o);
	}
}

//调用的时候和普通方法一样，只是需要注意参数
```

泛型构造器：

```java
class Foo{
    public <T> Foo (T t){
        System.out,println(t);
    }
}
```

#### 90、擦除

泛型擦除是指Java泛型中的泛型参数信息只在编译时有效，编译之后就会被擦除，也就是在运行时是不知道一个泛型的泛型参数是什么的，Gen<Integer>对象和Gen<String>对象在虚拟机看来其实都是Gen对象。

**JVM并不知道泛型的存在，因为泛型在编译过后就已经被处理成普通的类和方法**； 
处理机制是通过类型擦除，擦除规则：

1. 若泛型类型没有指定具体类型，用Object作为原始类型；
2. 若有限定类型< T exnteds XClass >，使用XClass作为原始类型；

既然都被替换成原始类型，那么为什么我们在获取的时候，不需要进行强制类型转换呢？

看下ArrayList.get() 方法：

```java
public E get(int index){
	RangeCheck(index); 
    return (E)elementData[index];
}
```

可以看到，在return之前，会根据泛型变量进行强转。假设泛型类型变量为Date，虽然泛型信息会被擦除掉，但是会将 (E) elementData[index]，编译为 (Date) elementData[index]。所以我们不用自己进行强转。



在严格的泛型代码里，带泛型声明的类总应该带着类型参数。**如果没有为这个泛型类指定实际的类型参数**，则该类型参数被称作 raw type（原始类型），**默认是声明该类型参数时指定的第一个上限类型**。

当把一个具有泛型信息的对象赋给另一个没有泛型信息的变量时，**所有在尖括号之间的类型信息都被扔掉**：比如一个List<String> 类型被转换为List ，则该List对集合元素的类型检查变成了**类型参数的上限**（即Object）。

```java
public class Demo9 {
    public static void main(String[] args){
        Apple<Integer> a = new Apple<>(6);
        //把a对象赋给Apple 变量，丢失尖括号里的类型信息
        Apple b =a;
        //Apple的类型形参上限是Number类，所以编译器依然知道b的getSize()方法返回Number类型，但具体是Number的哪个子类就不清楚了。b对象的size的编译时类型变成了Number
        Number size1 = b.getSize();
        //下面代码引起编译错误
        Integer size2 = b.getSize();
    }
}

class Apple<T extends Number>{
    T size;
    public Apple(T size){
        this.size = size;
    }
    public T getSize(){
        return this.size;
    }
}
```

**Java不支持泛型数组**。数组元素的类型部门包含类型变量或类型形参，除非是无上限的类型通配符。

#### 91、异常处理机制

```java
try{
    //业务逻辑代码
    //try里声明的变量只在try块内有效
    ...
}
catch(Exception e){
    //对异常进行处理
}
```

​       如果执行try块里的业务逻辑代码时出现异常，系统自动生成一个异常对象，该异常对象被提交给Java运行时环境，这个过程被称为抛出（throw）异常。

​       当Java运行时环境收到异常对象时，会寻找能处理该异常对象的catch块，如果找到合适的catch块，则把该异常对象交给该catch块处理，这个过程被称为捕获（catch）异常；如果Java运行时环境找不到捕获异常的catch块，则运行时环境终止，Java程序也将退出。

如何为该异常对象寻找 catch块呢？

当java运行时环境接受到异常对象后，会依次判断该异常对象是否是catch块后异常类或其子类的实例，如果是，Java运行时环境将调用该catch块来处理该异常；否则再次拿该异常对象和下一个catch块里的异常类进行比较。

原则是：先捕获小异常，在捕获大异常。

异常处理语法结构中只有try块是必需的，也就是说，如果没有try块，则不能有后面的catch块和finally块；**catch块和finally块都是可选的，但catch块和finally块至少出现其中之一**，也可以同时出现；可以有多个catch块，捕获父类异常的catch块必须位于捕获子类异常的后面；但不能只有try块，既没有catch块，也没有finally块；多个catch块必须位于try块之后，finally块必须位于所有的catch块之后。看如下程序。

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211012210259704.png" alt="image-20211012210259704" style="zoom: 80%;" />

**Java 7提供的多异常捕获**

从Java 7开始，一个catch块可以捕获多种类型的异常。

使用一个catch块捕获多种类型的异常时需要注意如下两个地方。
>捕获多种类型的异常时，多种异常类型之间用竖线（|）隔开。
>捕获多种类型的异常时，异常变量有隐式的final修饰，因此程序不能对异常变量重新赋值。（catch 块捕获一种异常时，异常变量没有final修饰）

```java
catch (IndexOutOfBoundsException | NumberFormatException
	| ArithmeticException ie){
    System.out.println(ie.getMessage());
}
```

所有的异常对象都包含了如下几个常用方法。
>getMessage() ：返回该异常的详细描述字符串。
>printStackTrace() ：将该异常的跟踪栈信息输出到标准错误输出。
>printStackTrace（PrintStream s）：将该异常的跟踪栈信息输出到指定输出流。
>getStackTrace() ：返回该异常的跟踪栈信息。

**使用 finally 回收资源**

不管try块中的代码是否出现异常，也不管哪一个catch块被执行，甚至在try块或catch块中执行了return语句，finally块总会被执行。

但是如果在catch块中使用 System.exit(1) 语句来退出虚拟机，则finally块将失去执行机会。

一旦在finally块中使用了return 或throw语句，将会导致try块、catch块中的return、throw语句失效。

当Java程序执行try块、catch块时遇到了return或throw语句，这两个语句都会导致该方法立即结束，但是系统执行这两个语句并不会结束该方法，而是去寻找该异常处理流程中是否包含finally块，如果没有finally块，程序立即执行return或throw语句，方法终止；如果有finally块，系统立即开始执行finally块——**只有当finally块执行完成后，系统才会再次跳回来执行try块、catch块里的return 或throw语句**；如果finally 块里也使用了return或throw等导致方法终止的语句，finally块已经终止了方法，系统将不会跳回去执行try块、catch块里的任何代码。

**尽量避免在finally块里使用return或throw等导致方法终止的语句，否则可能出现一些很奇怪的情况。**

**Java 的自动关闭资源的 try语句**：

Java 7增强了try语句的功能——它允许在try关键字后紧跟一对圆括号，圆括号可以声明、初始化一个或多个资源，此处的资源指的是那些必须在程序结束时显式关闭的资源（比如数据库连接、网络连接、IO），try语句在该语句结束时自动关闭这些资源。

自动关闭资源的try语句相当于包含了隐式的finally块（这个finally块用于关闭资源），因此这个try语句可以既没有catch块，也没有finally块。

**throws**

使用throws声明抛出异常时有一个限制，就是方法重写时“两小”中的一条规则：子类方法声明抛出的异常类型应该是父类方法声明抛出的异常类型的子类或相同，子类方法声明抛出的异常不允许比父类方法声明抛出的异常多。

**throw**

如果需要在程序中自行抛出异常，则应使用throw语句，throw语句可以单独使用，throw语句抛出的不是异常类，而是一个异常实例，而且每次只能抛出一个异常实例。throw语句的语法格式如下：

throw ExceptionInstance;

不管是系统自动抛出的异常，还是程序员手动抛出的异常，Java运行时环境对异常的处理没有差别。

如果throw语句抛出的异常是Checked异常，则该throw语句要么处于try块里，显式捕获该异常，要么放在一个带 throws声明抛出的方法中，即把该异常交给该方法的调用者处理；如果throw 语句抛出的异常是Runtime异常，则该语句无须放在try块里，也无须放在带 throws声明抛出的方法中；程序既可以显式使用try..catch来捕获并处理该异常，也可以完全不理会该异常，把该异常交给该方法调用者处理。

**自定义异常类**

用户自定义异常都应该继承Exception基类，如果希望自定义Runtime异常，则应该继承RuntimeException基类。定义异常类时通常需要提供两个构造器：一个是无参数的构造器；另一个是带一个字符串参数的构造器，这个字符串将作为该异常对象的描述信息（也就是异常对象的getMessage() 方法的返回值）。

```java
public class AuctionException extends Exception
{
	//无参数的构造器
	public AuctionException(){}
	//带一个字符串参数的构造器
	public AuctionException(String msg)
	{
		super(msg);
    }
}
```

在大部分情况下，创建自定义异常都可采用上述相似的代码完成，只需改变类名即可，让该异常类的类名可以准确描述该异常。

**异常处理规则：**

1. 不要过度使用异常，异常只应该用于处理非正常的情况，不要使用异常处理来代替正常的流程控制（比正常流程慢）。对于一些完全可预知，而且处理方式清楚的错误，程序应该提供相应的错误处理代码，而不是将其笼统地称为异常。
2. 不要使用过于庞大的try块。正确的做法是，把大块的try块分割成多个可能出现异常的程序段落，并把它们放在单独的try块中，从而分别捕获并处理异常。

#### 92、基本Annotation

5个基本的Annotation如下：把Annotation当成一个修饰符使用，用于修饰它支持的程序元素。

>@Override
>@Deprecated
>@Suppress Warnings
>@Safe Varargs
>@FunctionalInterface

1、@Override

用来指定方法覆载的，它可以强制一个子类必须覆盖父类的方法。

只能修饰方法，不能修饰其他程序元素。

```java
public class Fruit{
	public void info(){
        System.out.println("水果的info方法");
    }
}

class Apple extends Fruit{
    //使用@Override指定下面方法必须重写父类方法
    @Override
    public void info(){
        System.out.println("苹果重写水果的info方法");
    }
}
```

2、标识已过时：@Deprecated

用于表示某个程序元素（类、方法等）已过时，当其他程序使用已过时的类、方法时，编译器将会给出警告。

3、抑制编译器警告：@SuppressWarnings

指示被该Annotation修饰的程序元素（以及该程序元素中的所有子元素）取消显示指定的编译器警告。

@SuppressWarnings (value = "unchecked")

4、@SafeVarargs

堆污染：把一个不带泛型的对象赋给一个带泛型的变量时，往往就会发生这种“堆污染”。

```java
List list=new ArrayList<Integer>();
//添加元素时引发unchecked异常
1ist.add(20);
//下面代码引起“未经检查的转换”的警告，编译、运行时完全正常，发生堆污染
List<String> 1s = list;
```

抑制堆污染警告：

   >使用@SafeVarargs修饰引发该警告的方法或构造器。
   >使用@SuppressWarnings（"unchecked"）修饰。

5、Java8的函数式接口与@Functionallnterface

Java8规定：如果接口中只有一个抽象方法（可以包含多个默认方法或多个static方法），该接口就是函数式接口。@Functionallnterface就是用来指定某个接口必须是函数式接口。

**。。。还有一些内容没看完。。。**

##### 问题：java编译器编码和JVM编码问题？

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211018123623345.png" alt="image-20211018123623345" style="zoom:80%;" />

首先，Java源码文件。这些文件可以是任意字符编码的。
然后在Java的Class文件里存储的字符串是UTF-8编码的。

JVM内部使用的编码是utf-16

从Java源码文件到Java Class文件，中间会经过Java源码编译器（例如javac或ECJ）的编译。
也就是说，是Java源码编译器负责将Java源码文件的编码转换为最终的UTF-8。

如果不指定encoding，则使用平台默认的转换器，在简体中文的Windows上，平台默认编码会是GBK，那么javac就会以GBK编码的形式读取源码文件。

##### 问题：FileReader可以读取中文文件？？？

　    其实，java中有外码和内码之分，顾名思义，外码就是JVM外部使用的编码，比如你在编辑器中输入的“字”，假设是UTF-8编码，UTF-8是变长编码，一个中文可能是1-3个字节来表示；那么，在JVM中，用的都是utf-16编码，所有字符都统一使用两个字节表示，这就是Java的内码。

文件的编码：表示文件的存储形式，比如是utf-8编码的文件，字符 ’我‘ 就会占三个字节大小的空间。

平台默认编码：如果读取或写入文件时，没有指定编码形式，则采用默认的编码。（在Windows下，默认是GBK）

JVM编码：统一使用utf-16。

将idea里的默认编码改成utf-8后，FileReader可以读取中文文件，因为此时会默认用utf-8编码读取文件，刚好文件也是utf-8编码，所以 jvm 可以准确的读取到每个字符，并转化成utf-16编码，存入一个char之中。

#### 93、File类

如果希望在程序中操作文件和目录，都可以通过File类来完成。File能新建、删除、重命名文件和目录，但是File不能访问文件内容本身。如果需要访问文件内容本身，则需要使用输入/输出流。

File类可以使用文件路径字符串来创建File实例，该文件路径字符串既可以是绝对路径，也可以是相对路径。在默认情况下，系统总是依据用户的工作路径来解释相对路径，这个路径由系统属性“user.dir”
指定，通常也就是运行Java虚拟机时所在的路径。

```java
String str = System.getProperty("user.dir");
System.out.println("当前工作目录为："+ str);
```

>long lastModified（）：返回文件的最后修改时间。
>long length（）：返回文件内容的长度。

#### 94、输入、输出流

##### 1、流的分类

Java的输入流主要由 InputStream 和 Reader作为基类，而输出流则主要由 OutputStream 和 Writer 作为基类。它们都是一些抽象基类，无法直接创建实例。

字节流主要由 InputStream 和 OutputStream 作为基类，而字符流（16位）则主要由 Reader 和 Writer 作为基类。

![image-20211017193731277](C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211017193731277.png)

按照流的角色来分，可以分为节点流和处理流。
可以从/向一个特定的IO设备（如磁盘、网络）读/写数据的流，称为节点流，节点流也被称为低级流

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211017194330343.png" alt="image-20211017194330343" style="zoom:80%;" />

从图15.3中可以看出，当使用节点流进行输入/输出时，程序直接连接到实际的数据源，和实际的输入/输出节点连接。

处理流则用于对一个已存在的流进行连接或封装，通过封装后的流来实现数据读/写功能。处理流也被称为高级流。图15.4显示了处理流示意图。

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211017194427118.png" alt="image-20211017194427118" style="zoom:80%;" />

通过使用处理流，Java程序无须理会输入/输出节点是磁盘、网络还是其他的输入/输出设备，程序只要将这些节点流包装成处理流，就可以使用相同的输入/输出代码来读写不同的输入/输出设备的数据。

##### 2、InputStream 和 Reader

InputStream和Reader是所有输入流的抽象基类，本身并不能创建实例来执行输入，但它们将成为所有输入流的模板，所以它们的方法是所有输入流都可使用的方法。
在InputStream里包含如下三个方法。

>int read（） ：从输入流中读取单个字节，返回所读取的字节数据 (返回是int类型)。
>int read（byte[] b）：从输入流中最多读取 b.length 个字节的数据，并将其存储在字节数组b中，返回实际读取的字节数。
>int read（byte[] b，int off，int len)：从输入流中最多读取len个字节的数据，并将其存储在数组b中，放入数组b中时，并不是从数组起点开始，而是从off位置开始，返回实际读取的字节数。

在Reader里包含如下三个方法。
>int read（）：从输入流中读取单个字符，返回所读取的字符数据（返回值为int类型）。
>int read（char[] cbuf）：从输入流中最多读取cbuf.length个字符的数据，并将其存储在字符数组cbuf中，返回实际读取的字符数。
>int read（char[] cbuf，int off，int len）：从输入流中最多读取len个字符的数据，并将其存储在字符数组cbuf中，放入数组cbuf中时，并不是从数组起点开始，而是从off位置开始，返回实际读取的字符数。[off , off+len) 

read()方法 返回-1，表明到了输入流的结束点。

正如前面提到的，InputStream和Reader都是抽象类，本身不能创建实例，但它们分别有一个用于读取文件的输入流：FilelnputStream和FileReader，**它们都是节点流——会直接和指定文件关联**。

##### 3、OutputStream 和 Writer

OutputStream和Writer也非常相似，两个流都提供了如下三个方法。对应物理节点不存在时，自动创建一个，存在则把文件内容清空，从头开始写入。
>void write（int c）：将指定的字节/字符输出到输出流中，其中c既可以代表字节，也可以代表字符。
>void write（byte[]/char[] buf）：将字节数组/字符数组中的数据输出到指定输出流中。
>void write（byte[]/char[] buf，int off，int len）：将字节数组/字符数组中从off位置开始，长度为len的字节/字符输出到输出流中。

因为字符流直接以字符作为操作单位，所以Writer可以用字符串来代替字符数组，即以String对象作为参数。Writer里还包含如下两个方法。
>void write（String str）：将str字符串里包含的字符输出到指定输出流中。
>void write（String str，int off，int len）：将str字符串里从off位置开始，长度为len的字符输出到指定输出流中。

##### 4、处理流的用法

只要流的构造器参数不是一个物理节点，而是已经存在的流，那么这种流就一定是处理流；而所有节点流都是直接以物理IO节点作为构造器参数的。

优势：

1. 使用处理流进行输入输出操作更简单；
2. 使用处理流的执行效率更高。

在使用处理流包装了底层节点流之后，关闭输入输出流资源时，只要关闭最上层的处理流即可，系统会自动关闭被该处理流包装的节点流。

##### 5、输入输出流体系

![image-20211018165532871](C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211018165532871.png)

```java
FileWriter fw = new FileWriter("a.txt", true);  //true 表示向文件尾追加内容
FileOutputStream fos = new FileOutputStream("b.txt", true);
```

##### 6、转换流

输入输出流体系中还提供了两个转换流，这两个转换流用于实现将字节流转换成字符流，其中InputStreamReader 将字节输入流转换成字符输入流，OutputStreamWriter 将字节输出流转换成字符输出流。

Java使用System.in 代表标准输入，即键盘输入，但这个标准输入流是 InputStream 类的实例，使用不太方便，而且键盘输入内容都是文本内容，所以可以使用 InputStreamReader 将其转换成字符输入流，普通的 Reader 读取输入内容时依然不太方便，可以将普通的Reader再次包装成BufferedReader，利用 BufferedReader 的 readLine() 方法可以一次读取一行内容。

##### 7、重定向标准输入输出

Java的标准输入/输出分别通过 System.in 和 System.out 来代表，在默认情况下它们分别代表键盘和显示器，当程序通过 System.in 来获取输入时，实际上是从键盘读取输入；当程序试图通过 System.out 执行输出时，程序总是输出到屏幕。
在System类里提供了如下三个重定向标准输入/输出的方法。

>static void setErr（PrintStream err）：重定向“标准”错误输出流。
>static void setIn（InputStream in）：重定向“标准”输入流。
>static void setOut（PrintStream out）：重定向“标准”输出流。下面程序通过重定向标准输出流，将System.out的输出重定向到文件输出，而不是在屏幕上输出。

##### 8、Java虚拟机读写其他进程的数据 (还没看)

在第7章已经介绍过，使用Runtime对象的 exec() 方法可以运行平台上的其他程序，该方法产生一个Process对象，Process对象代表由该Java程序启动的子进程。Process类提供了如下三个方法，用于让程序和其子进程进行通信。

>InputStream getErrorStream（）：获取子进程的错误流。
>
>InputStream getlnputStream（）：获取子进程的输入流。
>
>OutputStream getOutputStream（）：获取子进程的输出流。

此处的输入流、输出流非常容易混淆，如果试图让子进程读取程序中的数据，那么应该用输入流还是输出流？不是输入流，而是输出流。**要站在Java程序的角度来看问题**，子进程读取Java程序的数据，就是让Java程序把数据输出到子进程中（就像把数据输出到文件中一样，只是现在由子进程节点代替了文件节点），所以应该使用输出流。

##### 9、RandomAccessFile

RandomAcessFile 是 Java 输入输出体系中功能最丰富的文件内容访问类，它提供了众多的方法来访问文件内容，特别的是RandomAcessFile 支持”随机访问“的方式，程序可以直接跳转到文件的任意地方来读写数据。

RandomAccessFile 对象也包含了一个记录指针，用以标识当前读写处的位置，当程序新创建一个RandomAccessFile 对象时，该对象的文件记录指针位于文件头（也就是0处），当读/写了n个字节后，文件记录指针将会向后移动n个字节。除此之外，RandomAccessFile可以自由移动该记录指针，既可以向前移动，也可以向后移动。RandomAccessFile包含了如下两个方法来操作文件记录指针。

>long getFilePointer（）：返回文件记录指针的当前位置。
>
>void seek（long pos）：将文件记录指针定位到pos位置。

RandomAccessFile 既可以读文件，也可以写，所以它既包含了完全类似于InputStream的三个read()
方法，其用法和InputStream的三个read() 方法完全一样；也包含了完全类似于OutputStream的三个 write() 方法，其用法和OutputStream的三个write() 方法完全一样。除此之外，RandomAccessFile还包含了一系列的 readXxx() 和 writeXxx() 方法来完成输入、输出。

```java
//将记录指针移动到文件末尾
raf.seek(raf.length());
raf.write("追加的内容！\r\n".getBytes());
```

RandomAccessFile类有两个构造器，一个使用String参数来指定文件名，一个使用File参数来指定文件本身。除此之外，创建RandomAccessFile对象时还需要指定一个mode参数，该参数指定RandomAccessFile的访问模式，该参数有如下4个值。
>"r"：以只读方式打开指定文件。如果试图对该RandomAccessFile执行写入方法，都将抛出IOException异常。
>"rw"：以读、写方式打开指定文件。如果该文件尚不存在，则尝试创建该文件。
>"rws"：以读、写方式打开指定文件。相对于“rw”模式，还要求对文件的内容或元数据的每个更新都同步写入到底层存储设备。
>"rwd”：以读、写方式打开指定文件。相对于“rw”模式，还要求对文件内容的每个更新都同步写入到底层存储设备。

**RandomAccessFile 依然不能向文件的指定位置插入内容**，如果直接将文件记录指针移动到中间某位置后开始输出，则**新输出的内容会覆盖文件中原有的内容**。如果需要向指定位置插入内容，程序需要先把插入点后面的内容读入缓冲区，等把需要插入的数据写入文件后，再将缓冲区的内容追加到文件后面。**(那你有鸡毛用)**

#### 95、对象序列化

序列化机制允许将实现序列化的Java对象转换成字节序列，这些字节序列可以保存在磁盘上，或通过网络传输，以备以后重新恢复成原来的对象。序列化机制使得对象可以脱离程序的运行而独立存在。

对象的序列化（Serialize）指将一个Java对象写入IO流中，与此对应的是，对象的反序列化（Deserialize）则指从IO流中恢复该Java对象。
如果需要让某个对象支持序列化机制，则必须让它的类是可序列化的（serializable）。为了让某个类是可序列化的，该类必须实现如下两个接口之一。

>Serializable
>Externalizable

Java的很多类已经实现了Serializable，该接口是一个标记接口，实现该接口无须实现任何方法，它只是表明该类的实例是可序列化的。

一旦某个类实现了 Serializable 接口，该类的对象就是可序列化的，程序可以通过如下两个步骤来序列化该对象：

1. 创建一个 ObjectOutputStream，这个输出流是一个处理流，所以必须建立在其他节点流的基础之上。

    ```java
    ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("object.txt"));
    ```

2. 调用ObjectOutputStream对象的 writeObject() 方法

    ```java
    //将一个Person对象输出到输出流中,Person类实现了Serializable 接口
    oos.WriteObject(person);
    ```

从二进制流中恢复Java对象，则需要使用反序列化：

1. 创建一个ObjectInputStream输入流，这个输入流是一个处理流，所以必须建立在其他节点流的基础之上。

    ```java
    ObjectInputStream ois = new ObjectInputStream(new FileInputStream("object.txt"));
    ```

2. 调用ObjectlnputStream对象的 readObject() 方法读取流中的对象，该方法返回一个Object类型的Java对象，如果程序知道该Java对象的类型，则可以将该对象强制类型转换成其真实的类型。

    ```java
    Person p = (Person)ois.readObject();
    ```

 反序列化机制无须通过构造器来初始化Java对象。

##### 1、serialVersionUID（序列化版本）

- **serialVersionUID是序列化前后的唯一标识符，就像是类的身份证号码一样**
- **默认如果没有人为显式定义过 serialVersionUID ，那编译器会为它自动声明一个！**
- **最好自己定义一个，这样即使对应的类被修改了，该对象也依然可以被正确地反序化。**

**第1个问题：** `serialVersionUID`序列化ID，可以看成是序列化和反序列化过程中的“暗号”，在反序列化时，JVM会把字节流中的序列号ID和被序列化类中的序列号ID做比对，只有两者一致，才能重新反序列化，否则就会报异常来终止反序列化的过程。

**第2个问题：** 如果在定义一个可序列化的类时，没有人为显式地给它定义一个`serialVersionUID`的话，则Java运行时环境会根据该类的各方面信息自动地为它生成一个默认的`serialVersionUID`，一旦更改了类的结构或者信息，则类的默认的`serialVersionUID`也会跟着变化！

##### 2、同一个对象多次序列化的处理

- 所有保存到磁盘中的对象都有一个序列化编号（和上面的ID 应该不是一个东西）。

- 当程序试图序列化一个对象时，程序将先检查该对象是否已经被序列化过，只有该对象从未（在本次虚拟机中）被序列化过，系统才会将该对象转换成字节序列并输出。

- 如果某个对象已经序列化过，程序将只是直接输出一个序列化编号，而不是再次重新序列化该对象。

**潜在的问题**：当程序序列化一个可变对象时，只有第一次使用writeObject() 方法输出时才会将该对象转换成字节序列并输出，当程序再次调用writeObject() 方法时，程序只是输出前面的序列化编号，即使后面该对象的实例变量值已被改变，改变的实例变量值也不会被输出。

##### 3、两种不被序列化的字段

序列化时，只对对象的状态进行保存，而不管对象的方法。

- 凡是被`static`修饰的字段是不会被序列化的
- 凡是被`transient`修饰符修饰的字段也是不会被序列化的

**对于第一点**，因为序列化保存的是**对象的状态**而非类的状态，所以会忽略`static`静态域也是理所应当的。

**对于第二点**，就需要了解一下`transient`修饰符的作用了。如果在序列化某个类的对象时，就是不希望某个字段被序列化（比如这个字段存放的是隐私值，如：密码等），那这时就可以用`transient`修饰符来修饰该字段。这样在序列化这个字段时，会设置为默认值 null 或 0。

##### 4、父类与子类序列化

1. 当一个父类实现序列化，子类自动实现序列化，不需要显式实现Serializable接口；
2. 当一个可序列化类有多个父类时（包括直接父类和间接父类），这些父类要么有无参数的构造器，要么也是可序列化的——否则反序列化时将抛出InvalidClassException异常。
3. 如果父类是不可序列化的，只是带有无参数的构造器，则该父类中定义的成员变量值不会序列化到二进制流中。这种情况下子类要先序列化自身，然后子类要负责序列化父类的域 （用反射？？）。

##### 5、对象引用得序列化

如果某个类的成员变量的类型不是基本类型或String类型或数组（都可序列化），而是另一个引用类型，那么这个引用类必须是可序列化的，否则拥有该类型成员变量的类也是不可序列化的。

当程序序列化一个Teacher对象时，如果该Teacher对象持有一个Person对象的引用，为了在反序列化时可以正常恢复该Teacher对象，程序会顺带将该Person对象也进行序列化，所以Person类也必须是可序列化的，否则Teacher类将不可序列化。

##### 6、自定义序列化

自定义序列化的类需要继承 Serializable 接口，并要写三个方法：

- private void writeObject(ObjectOutputStream out)   //序列化时会调用此方法
- private void readObject(ObjectInputStream in)   //反序列化时会调用此方法
- private void readObjectNoData()   //当序列化的类版本和反序列化的类版本不同时，或者ObjectInputStream流被修改时，会调用此方法。

Serializable接口中没有任何成员，上面3个方法都是我们自己写的。3个方法都是可选的，不强制，但一般都要实现前2个方法。

```java
class User implements Serializable{
 3     private int id;
 4     private String name;
 5     private String password;
 6     //......其他成员变量
 7 
 8     public User(int id,String name,String password){
 9         this.id=id;
10         this.name=name;
11         this.password=password;
12     }
13     //setter、getter方法
14     ...
26     //自定义序列化
27     private void writeObject(ObjectOutputStream out) throws IOException {
28         //只序列化以下3个成员变量
29         out.writeInt(id);
30         out.writeObject(name);
31         //写入反序后的密码，当然我们也可以使用其他加密方式。这样别人打开文件，看到的就不是真正的密码，更安全。
32         out.writeObject(new StringBuffer(password).reverse());
33     }
35     //自定义反序列化。注意：read()的顺序要和write()的顺序一致。
36     private void readObject(ObjectInputStream in) throws IOException, ClassNotFoundException {
37         this.id=in.readInt();
38         //readObject()返回的是Object，要强制类型转换
39         this.name=(String)in.readObject();
40         //反序才得到真正的密码
41         StringBuffer pwd=(StringBuffer)in.readObject();
42         this.password=pwd.reverse().toString();
43     }
44 
45 }
```

```java
class Test {
    public static void main(String[] args) throws IOException,   ClassNotFoundException {
        User zhangsan=new User(1,"张三","1234");

        //序列化
        ObjectOutputStream out=new ObjectOutputStream(new FileOutputStream("./obj.txt"));
        //调用我们自定义的writeObject()方法
        out.writeObject(zhangsan);
        out.close();

        //反序列化
        ObjectInputStream in=new ObjectInputStream(new FileInputStream("./obj.txt"));
        //调用自定义的readObject()方法
        User user=(User)in.readObject();
        in.close();
    }
}
```

我们甚至可以偷梁换柱，替换序列化的整个对象。不写上面提到的3个方法，而是写writeReplace()方法:

`private/default/protected/public Object writeReplace() throws ObjectStreamException{................}`

访问权限可以是任意的。 返回一个Object类型的对象。

序列化时，会先自动调用writeReplace()方法，用返回的这个对象，替换要序列化的那个对象，再进行序列化。就是说，实际序列化的是writeReplace()返回的这个对象，并不是原来的对象。

```java
//在User类里写此方法
private Object writeReplace(){
         User lisi=new User(2,"李四","qwer");
         return lisi;
}

//测试
User zhangsan=new User(1,"张三","1234");
//序列化
ObjectOutputStream out=new ObjectOutputStream(new FileOutputStream("./obj.txt"));
//执行writeObject() 时，会先自动调用writeReplace()，用返回的lisi替换原来的zhangsan，再序列化，实际序列化的对象是lisi
out.writeObject(zhangsan);
out.close();

//反序列化
ObjectInputStream in=new ObjectInputStream(new FileInputStream("./obj.txt"));
User user=(User)in.readObject();   
in.close()
```

系统在序列化某个对象之前，会先调用该对象的writeReplace（）和writeObject（）两个方法，系统总是先调用被序列化对象的writeReplace（）方法，如果该方法返回另一个对象，系统将再次调用另一个对象的writeReplace（）方法……直到该方法不再返回另一个对象为止，程序最后将调用该对象的writeObject（）方法来保存该对象的状态。



我们也可以替换掉反序列化得到的整个对象。

`private/default/protected/public Object readResolve(){................}`

在反序列化读取对象后，会自动调用此方法，将读取的对象替换为指定的对象。

与writeReplace（）方法类似的是，readResolve（）方法也可以使用任意的访问控制符，因此父类的readResolve（）方法可能被其子类继承。如果父类包含一个 protected 或public的 readResolve（）方法，而且子类也没有重写该方法，将会使得子类反序列化时得到一个父类的对象一—这显然不是程序要的结果。

通常的建议是用 private 修饰方法。

##### 7、另一种自定义序列化机制

这种序列化方式完全由程序员决定存储和恢复对象数据，要实现该目标，Java类必须实现 Externalizable 接口，该接口里定义了如下两个方法：

- void readExternal（ObjectInput in）：该方法调用Datalnput（它是Objectlnput的父接口）的方法来恢复基本类型的实例变量值，**调用ObjectInput的readObject() 方法来恢复引用类型的实例变量值。**

- void writeExternal（ObjectOutput out）：该方法调用DataOutput（它是ObjectOutput的父接口）的方法来保存基本类型的实例变量值，**调用ObjectOutput的writeObject() 方法来保存引用类型的实例变量值。**

```java
public class Blip implements Externalizable {
    
    private int i ;
    private String s;//没有初始化
    
    public Blip(String s ,int i) {
        this.s = s;
        this.i = i;
    }

    @Override
    public void readExternal(ObjectInput in) throws IOException,
            ClassNotFoundException {
        s = (String)in.readObject();
        i = in.readInt();
    }

    @Override
    public void writeExternal(ObjectOutput out) throws IOException {
        out.writeObject(s); 
        out.writeInt(i);
    }
}
```

如果程序需要序列化实现Externalizable接口的对象，一样调用ObjectOutputStream的writeObject（）
方法输出该对象即可；反序列化该对象，则调用ObjectInputStream的readObject（）方法，此处不再赘述。

![image-20211021215126424](C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211021215126424.png)

#### 96、NIO

新IO和传统的IO有相同的目的，都是用于进行输入/输出，但新IO使用了不同的方式来处理输入/输出，新IO采用**内存映射文件**的方式来处理输入/输出，新IO将文件或文件的一段区域映射到内存中，这样就可以像访问内存一样来访问文件了（这种方式模拟了操作系统上的虚拟内存的概念），通过这种方式来进行输入/输出比传统的输入/输出要快得多。

**内存映射文件**：硬盘上的文件的位置与进程逻辑地址空间中一块大小相同的区域之间一 一对应。相当于把整个文件放到了逻辑内存中，如果逻辑地址转化成物理地址后，物理地址对应的空间找不到，发生缺页中断，从硬盘上将文件读取到物理内存中。

Channel（通道）和 Buffer（缓冲）是新IO中的两个核心对象，Channel是对传统的输入/输出系统的模拟，在新IO系统中所有的数据都需要通过通道传输；Channel与传统的InputStream、OutputStream最大的区别在于它提供了一个map() 方法，通过该map() 方法可以直接将“一块数据”映射到内存中。
如果说传统的输入/输出系统是面向流的处理(最底层都是一个字节一个字节的处理)，则新IO则是面向块的处理。

Buffer可以被理解成一个容器，它的本质是一个数组，发送到Channel中的所有对象都必须首先放到Buffer中，而从Channel中读取的数据也必须先放到Buffer中。此处的Buffer有点类似于前面介绍的“竹筒”，但该Buffer既可以像“竹筒”那样一次次去Channel中取水，也允许使用Channel直接将文件的某块数据映射成Buffer。

##### 1、使用Buffer

从内部结构上来看，Buffer就像一个数组，它可以保存多个类型相同的数据。Buffer是一个抽象类，其最常用的子类是ByteBuffer，它可以在底层字节数组上进行get/set操作。除了ByteBuffer之外，对应于其他基本数据类型（boolean除外）都有相应的Buffer 类：CharBuffer、ShortBuffer、IntBuffer、LongBuffer、FloatBuffer、DoubleBuffer。

上面这些Buffer类，除了ByteBuffer之外，它们都采用相同或相似的方法来管理数据，只是各自管理的数据类型不同而已。这些Buffer类都没有提供构造器，通过使用如下方法来得到一个Buffer对象。

> static XxxBuffer allocate（int capacity）：创建一个容量为capacity的XxxBuffer对象。

但实际使用较多的是ByteBuffer和CharBuffer，其他Buffer子类则较少用到。其中ByteBuffer类还有一个子类：MappedByteBuffer，它用于表示Channel将磁盘文件的部分或全部内容映射到内存中后得到的结果，通常MappedByteBuffer对象由Channel的map() 方法返回。

在Buffer中有三个重要的概念：容量（capacity）、界限（limit）和位置（position）。
>容量（capacity）：缓冲区的容量（capacity）表示该Buffer的最大数据容量，即最多可以存储多少数据。缓冲区的容量不可能为负值，创建后不能改变。
>界限（limit）：第一个不应该被读出或者写入的缓冲区位置索引。也就是说，位于limit后的数据既不可被读，也不可被写。
>位置（position）：用于指明下一个可以被读出的或者写入的缓冲区位置索引（类似于IO流中的记录指针）。当使用Buffer从Channel中读取数据时，position的值恰好等于已经读到了多少数据。当刚刚新建一个Buffer对象时，其position为0；如果从Channel中读取了2个数据到该Buffer中，则position为2，指向Buffer中第3个（第1个位置的索引为0）位置。

除此之外，Buffer里还支持一个可选的标记（mark，类似于传统I0流中的mark），Buffer允许直接将position定位到该mark处。这些值满足如下关系：

0 ≤ mark ≤ position ≤ limit ≤ capacity

Buffer装入数据，开始时position为0，limit为capacity，当Buffer 装入数据结束后，调用Buffer的**flip() 方法，该方法将limit 设置为position所在位置，并将position设为0**（此时的 limit 等于Buffer的有效长度），这就使得Buffer的读写指针又移到了开始位置。也就是说，**Buffer 调用flip() 方法之后，Buffer为输出数据做好准备**；当Buffer 输出数据结束后，Buffer调用clear() 方法，**clear() 方法不是清空Buffer的数据，它仅仅将position置为0，将limit 置为capacity，这样为再次向Buffer中装入数据做好准备。**

除此之外，Buffer还包含如下一些常用的方法。
>int capacity（）：返回Buffer的 capacity大小。
>
>int limit（）：返回Buffer的界限（limit）的位置。
>
>Buffer limit（int newLt）：重新设置界限（limit）的值，并返回一个具有新的limit的缓冲区对象。
>
>int position（）：返回Buffer中的position值。
>
>Buffer position（int newPs）：设置Buffer的position，并返回position被修改后的Buffer对象。
>
>boolean hasRemaining（）：判断当前位置（position）和界限（limit）之间是否还有元素可供处理。
>
>int remaining（）：返回当前位置和界限（limit）之间的元素个数。
>
>Buffer mark（）：设置Buffer的mark位置，记录下Buffer对象调用此方法时的position。
>
>Buffer reset（）：将位置（position）转到mark所在的位置。
>
>Buffer rewind（）：将位置（position）设置成0，取消设置的mark。



除了这些方法之外，Buffer的所有子类还提供了两个重要的方法：put（）和get（）方法，用于向Buffer中放入数据和从Buffer中取出数据。当使用put（）和get（）方法放入、取出数据时，Buffer既支持对单个数据的访问，也支持对批量数据的访问（以数组作为参数）。
当使用put（）和get（）来访问Buffer中的数据时，分为相对和绝对两种。

>相对（Relative）：从Buffer的当前position处开始读取或写入数据，然后将 position 的值按处理元素的个数增加。
>绝对（Absolute）：直接根据索引（自己提供）向Buffer中读取或写入数据，使用绝对方式访问Buffer里的数据时，并不会影响 position 的值。

##### 2、使用 Channel

Channel类似于传统的流对象，但与传统的流对象有两个主要区别。（操作有点像处理流）

- Channel可以直接将指定文件的部分或全部直接映射成Buffer。

- 程序不能直接访问Channel中的数据，包括读取、写入都不行，Channel只能与Buffer进行交互。也就是说，如果要从Channel中取得数据，必须先用Buffer从Channel中取出一些数据，然后让程序从Buffer中取出这些数据；如果要将程序中的数据写入Channel，一样先让程序将数据放入Buffer中，程序再将Buffer里的数据写入Channel中。

所有的Channel都不应该通过构造器来直接创建，而是通过传统的节点 InputStream、OutputStream 的 getChannel() 方法来返回对应的Channel，不同的节点流获得的Channel不一样。例如，FileInputStream、FileOutputStream 的 getChannel() 返回的是FileChannel，而 PipedInputStream 和 PipedOutputStream 的 getChannel() 返回的是Pipe.SinkChannel、Pipe.SourceChannel。

Channel中最常用的三类方法是map（）、read（）和write（），**其中map（）方法用于将Channel对应的部分或全部数据映射成ByteBuffer**（一次搞定，不用一次次地读取、写入）；而read（）或write（）方法都有一系列重载形式，这些方法用于从Buffer中读取数据或向Buffer中写入数据。

FileChannel的read() 和write() 方法（与旧输入输出体系中的方法功能类似）：

- read(ByteBuffer dst) : 把FileChannel中的数据读入ByteBuffer中
- write(ByteBuffer dst) : 把ByteBuffer的数据写入FileChannel中
- position(long newPosition) : 设置此通道的记录指针

map（）方法的方法签名为：                                                                                              

MappedByteBuffer map（FileChannel.MapMode mode，long position，long size）

第一个参数执行映射时的模式，分别有只读、读写等模式；而第二个、第三个参数用于控制将Channel的哪些数据映射成ByteBuffer。

虽然 FileChannel 既可以读取也可以写入，但 FileInputStream 获取的 FileChannel 只能读，而FileOutputStream 获取的 FileChannel 只能写。RandomAccessFile 返回的 FileChannel 是只读的还是读写的，则取决于RandomAccessFile 打开文件的模式。

```java
File file = new File("b.txt");
//以文件输入流创建FileChannel
FileChannel inChannel = new FileInputStream(file).getChannel();
FileChannel outChannel = new FileOutputStream("a.txt").getChannel();

//一次性存取
MappedByteBuffer mappedByteBuffer = inChannel.map(FileChannel.MapMode.READ_ONLY,0,file.length());
outChannel.write(mappedByteBuffer);
//调整position、limit位置，不然后面的charBuffer为空
mappedByteBuffer.clear();
// 如何将ByteBuffer转成字符串
//方法1
Charset charset = StandardCharsets.UTF_8;//Charset.forName("utf-8")
CharsetDecoder decoder = charset.newDecoder();
//这里的decode()方法也认limit,也就是只会转换position到limit之间的字j
CharBuffer charBuffer = decoder.decode(mappedByteBuffer);
//CharBuffer 的toString()方法可以获取对应字符串，ByteBuffer只能获取对应状态，如position、limit
System.out.println(charBuffer);
//方法2，报错，不知道为什么MappedByteBuffer不能用array(）方法,但是自己定义的ByteBuffer可以用
//System.out.println(new String(mappedByteBuffer.array()));

//用竹筒多次重复取水
ByteBuffer byteBuffer = ByteBuffer.allocate(256);
while((inChannel.read(byteBuffer)) !=-1){
    //锁定Buffer的空白区
    byteBuffer.flip();
    outChannel.write(byteBuffer);
    //用这种方法得到字符串，会有点问题，需要得到limit,不然就会把整个byteBuffer都输出
    //System.out.println(new String(byteBuffer.array()));
    //转成字符串的方法2
    System.out.println(new String(byteBuffer.array(),0,byteBuffer.limit()));
    //将Buffer初始化，为下一次读取数据做准备
    byteBuffer.clear();
}
```

##### 3、字符集和Charset

计算机里的文件在底层都是二进制文件，计算机底层是没有文本文件、图片文件之分的，它只是忠实地记录每个文件的二进制序列而已。当需要保存文本文件时，程序必须先把文件中的每个字符翻译成二进制序列；当需要读取文本文件时，程序必须把二进制序列转换为一个个的字符。（编码解码是站在人的角度，像摩斯密码一样）

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211024134420826.png" alt="image-20211024134420826" style="zoom:67%;" />

JDK1.4提供Charset来处理字节序列和字符序列（字符串）之间的转换关系，该类包含了用于创建解码器和编码器的方法，还提供了获取Charset所支持字符集的方法，Charset类是不可变的。

Java7新增了一个StandardCharsets类，该类里包含了ISO_8859_1、UTF_8、UTF_16
等类变量，这些类变量代表了最常用的字符集对应的Charset对象。

获得了Charset对象之后，就可以通过该对象的newDecoder() 、newEncoder() 这两个方法分别返回CharsetDecoder和CharsetEncoder对象，代表该Charset的解码器和编码器。调用CharsetDecoder的 decode()方法就可以将ByteBuffer（字节序列）转换成CharBuffer（字符序列），调用CharsetEncoder的encode() 方法就可以将 CharBuffer 或 String(字符序列) 转换成ByteBuffer(字节序列)。

```java
        Charset charset = StandardCharsets.UTF_8;
        //Charset charset1 = Charset.forName("GBK");
        CharsetEncoder encoder = charset.newEncoder();
        CharsetDecoder decoder = charset.newDecoder();
```

**实际上，Charset类也提供了如下三个方法。**

>CharBuffer decode（ByteBuffer bb）：将ByteBuffer中的字节序列转换成字符序列的便捷方法。
>
>ByteBuffer encode（CharBuffer cb）：将CharBuffer中的字符序列转换成字节序列的便捷方法。
>
>ByteBuffer encode（String str）：将String中的字符序列转换成字节序列的便捷方法。

也就是说，获取了Charset对象后，如果仅仅需要进行简单的编码、解码操作，其实无须创建CharsetEncoder和CharsetDecoder对象，直接调用Charset的encode() 和decode() 方法进行编码、解码即可。

在String类里也提供了一个getBytes（String charset）方法，该方法返回byte[]，该方法也是使用指定的字符集将字符串转换成字节序列。

##### 4、文件锁

**排他锁**：指该锁一次只能被一个线程持有，如果线程T对数据A加上排他锁后，则其他线程不能再对A加任何类型的锁。获得排他锁的线程既能读数据又能修改数据。

**共享锁**：该锁可被多个线程所持有。如果线程T对数据A加上共享锁后，则其他线程只能对A再加共享锁，不能加排他锁。获得共享锁的线程只能读数据，不能修改数据。

在NIO中，Java提供了 FileLock 来支持文件锁定功能，在FileChannel中提供的 lock() /tryLock()方法可以获得文件锁 FileLock 对象，从而锁定文件。

lock() 和 tryLock()方法存在区别：当lock() 试图锁定某个文件时，如果无法得到文件锁，程序将一直阻塞；而 tryLock() 是尝试锁定文件，它将直接返回而不是阻塞，如果获得了文件锁，该方法则返回该文件锁，否则将返回 null 。

如果FileChannel只想锁定文件的部分内容，而不是锁定全部内容，则可以使用如下的 lock() 或tryLock() 方法。
>lock（long position，long size，boolean shared）：对文件从position开始，长度为size的内容加锁，该方法是阻塞式的。
>
>tryLock（long position，long size，boolean shared）：非阻塞式的加锁方法。参数的作用与上一个方法类似。

当参数shared为true时，表明该锁是一个共享锁，它将允许多个进程来读取该文件，但阻止其他进程获得对该文件的排他锁。当shared为false时，表明该锁是一个排他锁。

直接使用 lock() 或 tryLock() 方法获取的文件锁是排他锁。

程序可以通过调用 FileLock 的 isShared 来判断它获得的锁是否为共享锁。

处理完后文件后通过 FileLock 的 release() 方法释放文件锁。

文件锁是由Java虚拟机所持有的，如果两个Java程序使用同一个Java虚拟机运行，则它们不能对同一个文件加锁。

##### 5、Java 7 的NIO.2

Java7对原有的NIO进行了重大改进，改进主要包括如下两方面的内容。

- 提供了全面的文件IO和文件系统访问支持。

- 基于异步Channel的IO。

第一个改进表现为 Java7 新增的 java.nio.file 包及各个子包；第二个改进表现为Java7在 java.nio.channels 包下增加了多个以 Asynchronous 开头的Channel接口和类。Java7把这种改进称为NIO.2，本章先详细介绍NIO的第二个改进。

NIO.2为了弥补 File 类的不足，引入了一个Path接口，Path接口代表一个平台无关的平台路径。除此之外，NIO.2还提供了Files、Paths两个工具类，其中Files包含了大量静态的工具方法来操作文件；Paths则包含了两个返回Path的静态工厂方法（获得path对象的手段）。

下面程序简单示范了Path接口的功能和用法。

```java
//以当前路径中的文件来创建Path对象
Path path = Paths.get("a.txt");
System.out.println(path.getFileName());//输出a.txt

Path absolutePath = path.toAbsolutePath();
System.out.println(absolutePath);//输出D:\Java\xuexi\a.txt
//path里包含的路径数量，下面例子输出3
System.out.println(absolutePath.getNameCount());
System.out.println(absolutePath.getFileName());//输出a.txt

//以多个String来构建Path对象
Path path1 = Paths.get("D:","Java","xuexi");
//返回D:\Java\xuexi
```

Files类是一个高度封装的工具类，它提供了大量的工具方法来完成文件复制、读取文件内容、写入文件内容等功能——这些原本需要程序员通过IO操作才能完成的功能，现在Files类只要一个工具方法即可。

- static long copy(Path source, OutputStream out) : 将文件中的所有字节复制到输出流。
- static List<String> readAllLines(Path path) : 从文件中读取所有行
- static List<String> readAllLines(Path path, Charset cs) : 从文件中读取所有行
- static Path write(Path path, Iterable<? extends CharSequence> lines, Charset cs, OpenOption... options)

List 、Set 都实现了 Iterable 接口

```java
List<String> list = new ArrayList<>();
list.add("日照香炉生紫烟");
list.add("飞流直下三千尺");
//直接将多个字符串内容写入指定文件中
Files.write(Paths.get("poem.txt"),list, StandardCharsets.UTF_8);
```

**使用FileVisitor 遍历文件和目录**

Files里的 walkFileTree(...)方法

......

**使用 WatchService 监控文件变化**

在以前的Java版本中，如果程序需要监控文件的变化，则可以考虑启动一条后台线程，这条后台线程每隔一段时间去“遍历”一次指定目录的文件，如果发现此次遍历结果与上次遍历结果不同，则认为文件发生了变化。但这种方法不仅十分繁琐，而且性能也不好。

NIO.2的Path类提供了 register(...) 方法来监听文件系统的变化。

**访问文件属性**

Java7的NIO.2在java.nio.file.attribute包下提供了大量的工具类，通过这些工具类，开发者可以非常简单地读取、修改文件属性。这些工具类主要分为如下两类。
>XxxAttributeView：代表某种文件属性的“视图”。
>
>XxxAttributes：代表某种文件属性的“集合”，程序一般通过XxxAttributeView对象来获取XxxAttributes。

在这些工具类中，FileAttributeView是其他XxxAttributeView的父接口。

#### 97、多线程

##### 1、线程和进程

线程可以拥有自己的堆栈、自己的程序计数器和自己的局部变量，但不拥有系统资源，它与父进程的其他线程共享该进程所拥有的全部资源。操作系统无须将多个线程看作多个独立的应用，对多线程实现调度和管理以及资源分配。**线程的调度和管理由进程本身负责完成。**

##### 2、线程的创建和启动

Java使用Thread类代表线程，所有的线程对象都必须是Thread类或其子类的实例。每个线程的作用是完成一定的任务，实际上就是执行一段程序流（一段顺序执行的代码）。Java使用线程执行体来代表这段程序流。

当 Java 程序开始运行后，程序至少会创建一个主线程，而main() 方法的方法体代表主线程的线程执行体。

###### 通过继承Thread类来创建并启动多线程：

1. 定义Thread类的子类，并重写该类的 run() 方法，该 run() 方法的方法体就代表了线程需要完成的任务。因此把 **run() 方法称为线程执行体**。

2. 创建Thread子类的实例，即创建了线程对象。

3. 调用线程对象的 start() 方法来启动该线程。

    ```java
    public void run(){};
    ```

Thread 类的几个方法：

1. static Thread currentThread() : 获取当前线程
2. String getName() : 返回当前线程的名字
3. void setName(String name) : 为线程设置名字。在默认情况下，主线程的名字为main，用户启动的多个线程的名字依次为 Thread-0、Thread-1、。。。、Thread-n。

注意：使用继承 Thread 类的方法来创建线程类时，多个线程之间无法共享线程类的**实例变量**。

###### 实现 Runnable 接口创建线程类，并启动：

1. 定义 Runnable 接口的实现类，并重写该接口的 run() 方法，该 run() 方法的方法体同样是该线程的线程执行体。
2. 创建 Runnable 实现类的实例，并以此实例作为 Thread 的 target 来创建Thread对象，该Thread对象才是真正的线程对象。
3. 调用线程对象的 start() 方法来启动该线程。

```java
//创建 Runnable 实现类的对象
SecondThread st = new SecondThread();
//以 st 作为Thread的target来创建Thread对象，即线程对象
new Thread(st).start();
//创建 Thread 对象时指定target和新线程的名字
new Thread(st,"新线程1").start();
```

Runnable 对象仅仅作为 Thread 对象的 target，Runnable 实现类里包含的 run() 方法仅作为线程执行体。而实际的线程对象依然是 Thread 实例，只是该 Thread 线程负责执行其 target 的 run() 方法。

注意：采用Runnable接口的方式创建的多个线程可以共享线程类的实例变量。

###### 使用 Callable 和 Future 创建线程

从 Java 5 开始，Java 提供了 Callable 接口，该接口怎么看都像是 Runnable 接口的增强版，Callable接口提供了一个 call() 方法可以作为线程执行体，但 call() 方法比 run() 方法功能更强大。

- call() 方法可以有返回值
- call() 方法可以声明抛出异常

Java 5提供了 Future 接口来代表 Callable<V> 接口里 call() 方法的返回值（类型为V），并为 Future 接口提供了一个FutureTask 实现类，该实现类实现了 Future 接口，并实现了 Runnable 接口——可以作为 Thread 类的target。

Future 接口用来代表计算的结果（方法的返回值）。提供方法来检查计算是否完成，等待其完成，并检索计算结果。结果只能在计算完成后使用方法`get`进行检索，如有必要，阻塞，直到准备就绪。

在Future接口里定义了如下几个公共方法来控制它关联的Callable任务。

>boolean cancel（boolean mayInterruptlfRunning）：试图取消该Future里关联的Callable任务。
>
>V get（）：返回 Callable 任务里 call() 方法的返回值。调用该方法将导致程序阻塞，必须等到子线程结束后才会得到返回值。
>
>V get（long timeout，TimeUnit unit）：返回 Callable 任务里 call() 方法的返回值。该方法让程序最多阻塞timeout和unit 指定的时间，如果经过指定时间后Callable任务依然没有返回值，将会抛出TimeoutException异常。
>
>boolean isCancelled（）：如果在Callable任务正常完成前被取消，则返回true。
>boolean isDone（）：如果Callable任务已完成，则返回true。

FutureTask 的get 和 cancel 执行示意图：

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211025133043236.png" alt="image-20211025133043236" style="zoom:50%;" />

创建并启动有返回值的线程的步骤如下：

1. 创建 Callable 接口的实现类，并实现 call() 方法，该 call() 方法将作为线程执行体，且该 call() 方法有返回值，再创建 Callable 实现类的实例。从 Java8 开始，可以直接使用 Lambda 表达式创建Callable 对象。
2. 使用 FutureTask 类来包装Callable对象，该 Future Task 对象封装了该 Callable 对象的 call() 方法的返回值。
3. 使用 FutureTask 对象作为 Thread 对象的target创建并启动新线程。
4. 调用 FutureTask 对象的 get() 方法来获得子线程执行结束后的返回值。

```java
class MyCallable implements Callable<Integer>{
    public Integer call(){
        int  i = 0;
        for(;i<100;i++){
            System.out.println(Thread.currentThread().getName()+" 的循环变量i的值："+i);
        }
        return i;
    }
}

public class Demo12 {
    public static void main(String[] args){
        //FutureTask的泛型与Callable的泛型一样，即返回值的类型
        FutureTask<Integer> task = new FutureTask<>(new MyCallable());
        
        for(int i=0;i<100;i++){
            System.out.println(Thread.currentThread().getName()+" 的循环变量i的值："+i);
            if(i == 10){
                //实质还是以 Callable 对象来创建并启动线程的
                new Thread(task,"有返回").start();
            }
        }
        try {
            //获取线程返回值
            System.out.println(task.get());
        } catch (InterruptedException | ExecutionException e) {
            e.printStackTrace();
        }
    }
}
```

**不论 FutureTask 调用多少次 run() 或者 call() 方法，它都能确保只执行一次 Runnable 或Callable 任务。所以如果想让多个线程共享同一个Callable 对象，需要用不同的FutureTask对象来包装这个Callable 对象。**

###### 创建线程的三种方式对比

通过继承 Thread 类或实现 Runnable、Callable 接口都可以实现多线程，不过实现Runnable接口与实现Callable 接口的方式基本相同，只是Callable接口里定义的方法有返回值，可以声明抛出异常而已。因此可以将实现Runnable接口和实现Callable接口归为一种方式。这种方式与继承Thread方式之间的主要差别如下。

采用实现Runnable、Callable接口的方式创建多线程的优缺点：

- 线程类只是实现了Runnable接口或Callable接口，还可以继承其他类。
- 在这种方式下，**多个线程可以共享同一个 target 对象**，所以**非常适合多个相同线程来处理同一份资源的情况**，从而可以将CPU、代码和数据分开，形成清晰的模型，较好地体现了面向对象的思想。
    劣势是，编程稍稍复杂，如果需要访问当前线程，则必须使用 Thread.currentThread() 方法。

采用继承Thread类的方式创建多线程的优缺点：
劣势是，因为线程类已经继承了Thread类，所以不能再继承其他父类。
优势是，编写简单，如果需要访问当前线程，则无须使用 Thread.currentThread() 方法，直接使用this即可获得当前线程。

鉴于上面分析，因此一般推荐采用实现Runnable接口、Callable接口的方式来创建多线程。

##### 3、线程的生命周期

当线程被创建并启动以后，它既不是一启动就进入了执行状态，也不是一直处于执行状态，在线程的生命周期中，它要经过新建（New）、就绪（Runnable）、运行（Running）、阻塞（Blocked）和死亡（Dead）5种状态。尤其是当线程启动以后，它不可能一直“霸占”着CPU独自运行，所以CPU需要在多条线程之间切换，于是线程状态也会多次在运行、阻塞之间切换。

###### 新建和就绪状态

当程序使用new关键字创建了一个线程之后，该线程就处于新建状态，**此时它和其他的Java对象一样，仅仅由Java虚拟机为其分配内存，并初始化其成员变量的值**。此时的线程对象没有表现出任何线程的动态特征，程序也不会执行线程的线程执行体。

当线程对象调用了 start() 方法之后，该线程处于就绪状态，**Java虚拟机会为其创建方法调用栈和程序计数器，处于这个状态中的线程并没有开始运行，只是表示该线程可以运行了**。至于该线程何时开始运行，取决于JVM里线程调度器的调度。

调用 start() 方法来启动线程，系统会把该 run() 方法当成线程执行体来处理；但如果直接调用线程对象的 run() 方法，则 run() 方法立即就会被执行，而且在 run() 方法返回之前其他线程无法并发执行——也就是说，**如果直接调用线程对象的 run() 方法，系统把线程对象当成一个普通对象，而 run() 方法也是一个普通方法，而不是线程执行体。**

如果希望调用子线程的 start() 方法后子线程立即开始执行，程序可以使用 Thread.sleep(1) 来让当前运行的线程（主线程）睡眠1毫秒——1毫秒就够了，因为在这1毫秒内**CPU不会空闲**，它会去执行另一个处于就绪状态的线程，这样就可以让子线程立即开始执行。

###### 运行和阻塞状态

如果处于就绪状态的线程获得了CPU，开始执行 run() 方法的线程执行体，则该线程处于运行状态。

当发生如下情况时，线程将会进入阻塞状态。

- 线程调用 sleep() 方法主动放弃所占用的处理器资源。
- 线程调用了一个阻塞式IO方法，在该方法返回之前，该线程被阻塞。
- 线程试图获得一个同步监视器，但该同步监视器正被其他线程所持有。关于同步监视器的知识、后面将有更深入的介绍。
- 线程在等待某个通知（notify）。
- 程序调用了线程的 suspend() 方法将该线程挂起。但这个方法容易导致死锁，所以应该尽量避免使用该方法。**(已弃用)**

被阻塞的线程会在合适的时候重新进入就绪状态，注意是就绪状态而不是运行状态。针对上面几种情况，当发生如下特定的情况时可以解除上面的阻塞，让该线程重新进入就绪状态。

- 调用 sleep() 方法的线程经过了指定时间。
- 线程调用的阻塞式IO方法已经返回。
- 线程成功地获得了试图取得的同步监视器。
- 线程正在等待某个通知时，其他线程发出了一个通知。
- 处于挂起状态的线程被调用了 resume() 恢复方法。**(已弃用)**

![image-20211025140936181](C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211025140936181.png)

###### 线程死亡

线程会以如下三种方式结束，结束后就处于死亡状态。

- run() 或 call() 方法执行完成，线程正常结束。
- 线程抛出一个未捕获的 Exception 或 Error。
- 直接调用该线程的 stop() 方法来结束该线程——该方法容易导致死锁，通常不推荐使用。**(已弃用)**

注意：当主线程结束时，其他线程不受任何影响，并不会随之结束。一旦子线程启动起来后，它就拥有和主线程相同的地位。(生而平等。。。)

为了测试某个线程是否已经死亡，可以调用线程对象的 isAlive() 方法，当线程处于就绪、运行、阻塞三种状态时，该方法将返回 true；当线程处于新建、死亡两种状态时，该方法将返回 false。

##### 4、控制线程

###### join 线程

Thread 提供了让一个线程等待另一个线程完成的方法—— join() 方法。当在某个程序执行流中调用其他线程的 join() 方法时，这个程序执行流将被阻塞，直到被 join() 方法加入的 join 线程执行完为止。
join() 方法通常由使用线程的程序调用，以将大问题划分成许多小问题，每个小问题分配一个线程。
当所有的小问题都得到处理后，再调用主线程来进一步操作。

```java
FutureTask<Integer> task = new FutureTask<>(new MyCallable());
for(int i = 0;i<100;i++){
	System.out.println("主线程："+i);
	Thread thread = new Thread(task);
	thread.start();
    //主线程将一直处于阻塞状态，直到thread线程执行完成。才继续向下执行
	thread.join();
}
```

join() 方法有如下三种重载形式:

- join() ：等待被join的线程执行完成。
- join( long millis) ：等待被join的线程的时间最长为 millis 毫秒。如果在millis毫秒内被join的线程还没有执行结束，则不再等待。
- join（long millis，int nanos）：等待被join的线程的时间最长为millis 毫秒加nanos毫微秒。一般不用，程序对时间的精度无须精确到毫微秒；计算机硬件、操作系统本身也无法精确到毫微秒。

###### 后台线程

有一种线程，它是在后台运行的，它的任务是为其他的线程提供服务，这种线程被称为“后台线程(Daemon Thread) ”，又称为“守护线程”或“精灵线程”。JVM的垃圾回收线程就是典型的后台线程。

后台线程有个特征：如果所有的前台线程都死亡，后台线程会自动死亡。

调用 Thread 对象的 setDaemon(true) 方法可将指定线程设置成后台线程。当整个虚拟机中只剩下后台线程时，程序就没有继续运行的必要了，所以虚拟机也就退出了。

要将某个线程设置为后台线程，必须再该线程启动之前设置，也就是说，**setDaemon(true) 必须在 start() 方法之前调用。**

主线程默认是前台线程。前台线程创建的子线程默认是前台线程，后台线程创建的子线程默认是后台线程。

###### 线程睡眠：sleep

**static** void sleep(long millis) : 让当前正在执行的线程暂停 millis 毫秒，并进入阻塞状态。

###### 线程让步：yield

yield() 方法（无参数）是一个和 sleep() 方法有点相似的方法，它也是Thread类提供的一个**静态方法**，它也可以让当前正在执行的线程暂停，但它不会阻塞该线程，它只是将该线程转入就绪状态。yield() 只是让当前线程暂停一下，完全可能的情况是：当某个线程调用了 yield() 方法暂停之后，线程调度器又将其调度出来重新执行。

实际上，当某个线程调用了 yield() 方法暂停之后，线程调度器重新调度，优先级高的优先（即使之前已经调用过 yield() 方法），当优先级相同时，之前没有执行过 yield() 方法的线程优先。

###### 改变线程优先级

优先级高的线程获得较多的执行机会，而优先级低的线程则获得较少的执行机会。

每个线程默认的优先级都与创建它的父线程的优先级相同，在默认情况下，main线程具有普通优先级，由main线程创建的子线程也具有普通优先级。

Thread 类提供了setPriority（int newPriority）、getPriority() 方法来设置和返回指定线程的优先级，其中 setPriority() 方法的参数可以是一个整数，范围是1~10之间，也可以使用Thread类的如下三个静态常量。

- MAX_PRIORITY：其值是10。

- MIN_PRIORITY：其值是1。
- NORM_PRIORITY：其值是5。

值得指出的是，虽然 Java 提供了10个优先级，但这些优先级级别需要操作系统的支持。不同操作系统上的优先级并不相同，而且也不能很好地和 Java 的10个优先级对应，例如 Windows 2000 仅提供了7个优先级。因此应该尽量避免直接为线程指定优先级，而应该使用MAX_PRIORITY、MIN_PRIORITY 和NORM PRIORITY三个静态常量来设置优先级，这样才可以保证程序具有最好的可移植性。

设置优先级可以在 start() 之后。

##### 5、线程同步

###### 同步代码块

```java
synchronized(obj){
	...
	//此处的代码就是同步代码块，就是一个临界区
    //同一时刻最多只有一个线程处于临界区内，从而保证了线程的安全性
}
```

上面语法格式中 synchronized 后括号里的obj就是同步监视器，上面代码的含义是：线程开始执行同步代码块之前，必须先获得对同步监视器的锁定（加锁）。**任何时刻只能有一个线程可以获得对同步监视器的锁定**，当同步代码块执行完成后，该线程会释放对该同步监视器的锁定。

这样的做法符合 ” 加锁 ->  修改 -> 释放锁 “的逻辑。任何线程在修改指定资源之前，首先对该资源加锁，在加锁期间其他线程无法修改该资源，当该线程修改完成后，该线程释放对该资源的锁定。

虽然Java程序允许使用任何对象作为同步监视器，但想一下同步监视器的目的：阻止两个线程对同一个共享资源进行并发访问，因此通常推荐使用可能被**并发访问的共享资源充当同步监视器**。

###### 同步方法

与同步代码块对应，Java 的多线程安全支持还提供了同步方法，同步方法就是使用synchronized 关键字来修饰某个方法，则该方法称为同步方法。对于 synchronized 修饰的实例方法（非static方法）而言，无须显式指定同步监视器，同步方法的同步监视器是 this，也就是调用该方法的对象。

也就是说同一时刻最多只有一个线程在执行同步方法

JDK所提供的StringBuilder、StringBuffer就是为了照顾单线程环境和多线程环境所提供的类，在单线程环境下应该使用StringBuilder来保证较好的性能；当需要保证多线程安全时，就应该使用StringBuffer。

**当一个线程进入一个对象的一个synchronized方法后，其他线程可以进入此对象的普通方法**

###### 释放同步监视器的锁定

程序无法显示释放对同步监视器的锁定，线程会在如下几种情况下释放对同步监视器的锁定。

- 当前线程的同步方法、同步代码块执行结束，当前线程即释放同步监视器。
- 当前线程在同步代码块、同步方法中遇到 break、return 终止了该代码块、该方法的继续执行，当前线程将会释放同步监视器。(这不也是执行结束？？？)
- 当前线程在同步代码块、同步方法中出现了未处理的Error 或Exception，导致了该代码块、该方法异常结束时，当前线程将会释放同步监视器。
- 当前线程执行同步代码块或同步方法时，程序执行了同步监视器对象的 wait() 方法，则当前线程暂停，并释放同步监视器。

在如下所示的情况下，线程不会释放同步监视器。

- 线程执行同步代码块或同步方法时，程序调用 Thread.sleep() 、Thread.yield() 方法来暂停当前线程的执行，当前线程不会释放同步监视器。
- 线程执行同步代码块时，其他线程调用了该线程的 suspend() 方法将该线程挂起，该线程不会释放同步监视器。当然，程序应该尽量避免使用 suspend() 和 resume() 方法来控制线程。

###### 同步锁（Lock）

​		从Java5开始，Java提供了一种功能更强大的线程同步机制——通过显式定义同步锁对象来实现同步，在这种机制下，同步锁由Lock对象充当。Lock 提供了比 synchronized 方法和 synchronized 代码块更广泛的锁定操作，Lock允许实现更灵活的结构，可以具有差别很大的属性，并且支持多个相关的Condition对象。

​		Lock 是控制多个线程对共享资源进行访问的工具。通常，**锁提供了对共享资源的独占访问，每次只能有一个线程对Lock对象加锁，线程开始访问共享资源之前应先获得Lock对象**。（显式地使用 Lock 对象当作同步监视器）

​		Lock、ReadWriteLock（读写锁） 是 Java5 提供的两个根接口，并为 Lock 提供了 ReentrantLock（可重入锁）实现类，为 ReadWriteLock 提供了 ReentrantReadWriteLock 实现类。

​		Java8 新增了新型的 StampedLock 类，在大多数场景中它可以替代传统的ReentrantReadWriteLock。ReentrantReadWriteLock 为读写操作提供了三种锁模式：Writing、ReadingOptimistic、Reading。

​		在实现线程安全的控制中，比较常用的是 ReentrantLock（可重入锁）。使用该Lock对象可以显式地加锁、释放锁。

```java
class X{
	//定义锁对象，最好是给一个共享资源对象设置一个lock对象
	private final ReentrantLock lock = new ReentrantLock();
	// ...
	//定义需要保证线程安全的方法
    public void m(){
        //加锁
        lock.lock();
        try{
            //需要保证线程安全的代码
        }
        //使用 finally 块来保证释放锁
        finally{
            lock.unlock();
        }
    }
}
```

​		虽然同步方法和同步代码块的范围机制使得多线程安全编程非常方便，而且还可以避免很多涉及锁的常见编程错误，但有时也需要以更为灵活的方式使用锁。Lock提供了同步方法和同步代码块所没有的其他功能，包括用于非块结构的 tryLock() 方法，以及试图获取可中断锁的lockInterruptibly() 方法，还有获取超时失效锁的 tryLock（long，TimeUnit）方法。

​		ReentrantLock 锁具有**可重入性**，也就是说，一**个线程可以对已被加锁ReentrantLock锁再次加锁**，ReentrantLock 对象会维持一个计数器来追踪 lock() 方法的嵌套调用，线程在每次调用 lock() 加锁后，必须显式调用 unlock() 来释放锁，**所以一段被锁保护的代码可以调用另一个被相同锁保护的方法。**

###### 死锁

当两个线程相互等待对方释放同步监视器时就会发生死锁，Java虚拟机没有监测，也没有采取措施来处理死锁情况，所以多线程编程时应该采取措施避免死锁出现。一旦出现死锁，整个程序既不会发生任何异常，也不会给出任何提示，只是所有线程处于阻塞状态，无法继续。

##### 6、线程通信

###### 传统的线程通信

Object 类提供了 wait() 、notify() 和 notifyAll() 三个方法，这三个方法并不属于Thread类，而是属于Object类，用来控制线程的协作。**但这三个方法必须由同步监视器对象来调用**，这可分成以下两种情况。

- 对于使用 synchronized 修饰的同步方法，因为该类的默认实例（this）就是同步监视器，所以可以在同步方法中直接调用这三个方法。
- 对于使用 synchronized 修饰的同步代码块，同步监视器是synchronized后括号里的对象，所以必须使用该对象调用这三个方法。

关于这三个方法的解释如下:

- wait() ：导致当前线程等待，处于阻塞状态，直到其他线程调用该同步监视器的 notify() 方法或 notifyAll() 方法来唤醒该线程。该 wait() 方法有三种形式——无时间参数的wait（一直等待，直到其他线程通知）、带毫秒参数的 wait() 和带毫秒、毫微秒参数的 wait() （这两种方法都是等待指定时间后自动苏醒）。**调用 wait() 方法的当前线程会释放对该同步监视器的锁定。**
- notify() ：唤醒在此同步监视器上等待的单个线程。如果所有线程都在此同步监视器上等待，**则会选择唤醒其中一个线程。选择是任意性的**。只有当前线程放弃对该同步监视器的锁定后（使用 wait() 方法），才可以执行被唤醒的线程。
- notifyAll() ：唤醒在此同步监视器上等待的所有线程。只有当前线程放弃对该同步监视器的锁定后，才可以执行被唤醒的线程。

**一些想法**：前面的同步代码块、同步方法、同步锁，都是控制多个线程对共享资源进行访问，相当于控制多个消费者的消费；而这里的三个方法是控制线程间的协作，相当于控制消费者与生产者之间的协作。多线程一般是要解决线程同步和线程协作的问题，**就像操作系统的互斥量（mutex）与信号量(semaphore)一样。**

###### 使用 Condition 控制线程通信

​		如果程序不使用 synchronized 关键字来保证同步，而是直接使用 Lock 对象来保证同步，则系统中不存在隐式的同步监视器，也就不能使用 wait() 、notify() 、notifyAll() 方法进行线程通信了。

​		当使用 Lock 对象来保证同步时，Java 提供了一个 Condition 类来控制线程的协调运行，使用Condition 可以让那些已经得到 Lock 对象却无法继续执行的线程释放 Lock 对象，Condition 对象也可以唤醒其他处于等待的线程。

​		Condition 实例被绑定在一个 Lock 对象上。要获得特定 Lock 实例的 Condition 实例，**调用Lock 对象的 newCondition()** 方法即可。Condition类提供了如下三个方法:

- await() ：类似于隐式同步监视器上的 wait() 方法，导致当前线程等待，直到其他线程调用该Condition 的 signal() 方法或 signalAll() 方法来唤醒该线程。该 await() 方法有更多变体，如long awaitNanos（long nanosTimeout）、void awaitUninterruptibly() 、awaitUntil（Date deadline）等，可以完成更丰富的等待操作。
- signal() ：唤醒在此 Lock 对象上等待的单个线程。如果所有线程都在该 Lock 对象上等待，则会选择唤醒其中一个线程。选择是任意性的。只有当前线程放弃对该Lock对象的锁定后（使用 await() 方法），才可以执行被唤醒的线程。
- signalAll() ：唤醒在此Lock对象上等待的所有线程。只有当前线程放弃对该Lock对象的锁定后，才可以执行被唤醒的线程。

###### 使用 BlockingQueue 控制线程通信

Java5 提供了一个 BlockingQueue 接口，虽然 BlockingQueue 也是 Queue 的子接口，但它的主要用途并不是作为容器，而是作为线程同步的工具。BlockingQueue 具有一个特征：当生产者线程试图向 BlockingOueue 中放入元素时，如果该队列已满，则该线程被阻塞；当消费者线程试图从 BlockingQueue 中取出元素时，如果该队列已空，则该线程被阻塞。

程序的两个线程通过交替向 BlockingQueue 中放入元素、取出元素，即可很好地控制线程的通信。BlockingQueue提供如下两个支持阻塞的方法。

- put(E e) ：尝试把E元素放入 BlockingQueue 中，如果该队列的元素已满，则阻塞该线程。
- take() ：尝试从 BlockingQueue 的头部取出元素，如果该队列的元素已空，则阻塞该线程。

BlockingQueue继承了Queue接口，当然也可使用Queue接口中的方法。这些方法归纳起来可分为如下三组。

- 在队列尾部插入元素。包括add(E e)、offer(E e) 和 put(E e) 方法，当该队列已满时，这三个方法分别会抛出异常、返回false、阻塞队列。
- 在队列头部删除并返回删除的元素。包括 remove() 、poll() 和 take() 方法。当该队列已空时，这三个方法分别会抛出异常、返回false、阻塞队列。
- 在队列头部取出但不删除元素。包括 element() 和 peek() 方法，当队列已空时，这两个方法分别抛出异常、返回false。

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211027111702606.png" alt="image-20211027111702606" style="zoom:80%;" />

图中中以黑色方框框出的都是 Java7 新增的阻塞队列。从图中可以看到，BlockingQueue 包含如下5个实现类：

- ArrayBlockingQueue：基于数组实现的BlockingQueue队列。
- LinkedBlockingQueue：基于链表实现的BlockingQueue队列。
- PriorityBlockingQueue：它并不是标准的阻塞队列。与前面介绍的PriorityQueue类似，该队列调用remove() 、poll() 、take() 等方法取出元素时，并不是取出队列中存在时间最长的元素，而是队列中最小的元素。PriorityBlockingQueue判断元素的大小即可根据元素（实现Comparable接口）的本身大小来**自然排序**，也可使用Comparator 进行定制排序。
- SynchronousQueue：同步队列。对该队列的存、取操作必须交替进行。
- DelayQueue：它是一个特殊的 BlockingQueue，底层基于 PriorityBlockingQueue 实现。不过，DelayQueue 要求集合元素都实现 Delay 接口（该接口里只有一个 long getDelay() 方法），DelayQueue 根据集合元素的 getDalay() 方法的返回值进行排序。

（看书中的代码啊，put() 和 take() 确实可以完成线程间的协作，但是多个生产者线程并发调用 put() 方法不会出现问题吗？？哈哈哈，看了看put() 和 take() 的源码，里面果然定义了 Lock 对象来控制生产者线程的同步）

**上面介绍的那些 BlockingQueue 中的方法（看源码）在实现时，都定义了 Lock 对象来控制线程间的同步。**

##### 7、线程组

Java 使用 ThreadGroup 来表示线程组，它可以对一批线程进行分类管理，Java 允许程序直接对线程组进行控制。对线程组的控制相当于同时控制这批线程。如果程序没有显式指定线程属于哪个线程组，则该线程属于默认线程组。在默认情况下，子线程和创建它的父线程处于同一个线程组内，例如A线程创建了B线程，并且没有指定B线程的线程组，则B线程属于A线程所在的线程组。

主线程所在的线程组为 main，这是所有线程默认的线程组。

**一旦某个线程加入了指定线程组之后，该线程将一直属于该线程组，直到该线程死亡，线程运行中途不能改变它所属的线程组**。

Thread类提供了如下几个构造器来设置新创建的线程属于哪个线程组。

- Thread（ThreadGroup group，Runnable target）：以 target 的 run() 方法作为线程执行体创建新线程，属于 group 线程组。
- Thread（ThreadGroup group，Runnable target，String name）：以 target 的 run() 方法作为线程执行体创建新线程，该线程属于group线程组，且线程名为name。
- Thread（ThreadGroup group，String name）：创建新线程，新线程名为name，属于group 线程组。

因为中途不可改变线程所属的线程组，所以 Thread 类没有提供 setThreadGroup() 方法来改变线程所属的线程组，但提供了一个 getThreadGroup() 方法来返回该线程所属的线程组，getThreadGroup() 方法的返回值是 ThreadGroup 对象，表示一个线程组。

ThreadGroup 类提供了如下两个简单的构造器来创建实例。

- ThreadGroup（String name）：以指定的线程组名字来创建新的线程组。
- ThreadGroup（ThreadGroup parent，String name）：以指定的名字、指定的父线程组创建一个新线程组。

上面两个构造器在创建线程组实例时都必须为其指定一个名字，也就是说，线程组总会具有一个字符串类型的名字，该名字可通过调用 ThreadGroup 的 getName()  方法来获取，但不允许改变线程组的名字。

ThreadGroup类提供了如下几个常用的方法来操作整个线程组里的所有线程。

>int activeCount（）：返回此线程组中活动线程的数目。（也就是所有就绪、运行、阻塞状态的线程数）
>
>interrupt（）：中断此线程组中的所有线程。
>
>isDaemon（）：判断该线程组是否是后台线程组。
>
>setDaemon（boolean daemon）：把该线程组设置成后台线程组。后台线程组具有一个特征——当后台线程组的最后一个线程执行结束或最后一个线程被销毁后，后台线程组将自动销毁。
>
>setMaxPriority（int pri）：设置线程组的最高优先级。
>
>list() : 将线程组中的线程打印到标准输出。

##### 8、线程池

​		系统启动一个新线程的成本是比较高的，因为它涉及与操作系统交互。在这种情形下，使用线程池可以很好地提高性能，尤其是当程序中需要创建大量生存期很短暂的线程时，更应该考虑使用线程池。

​		与数据库连接池类似的是，**线程池在系统启动时即创建大量空闲的线程**，程序将一个Runnable 对象或 Callable 对象传给线程池，线程池就会启动一个线程来执行它们的 run() 或call() 方法，当 run() 或 call() 方法执行结束后，该线程并不会死亡，而是再次返回线程池中成为空闲状态，等待执行下一个 Runnable 对象的 run() 或 call() 方法。

###### java 8 改进的线程池

在 Java5 以前，开发者必须手动实现自己的线程池；从 Java5 开始，Java内建支持线程池。Java5新增了一个 Executors 工厂类来产生线程池，该工厂类包含如下几个**静态工厂方法**来创建线程池。
>newCachedThreadPool() ：创建一个具有缓存功能的线程池，系统根据需要创建线程，这些线程将会被缓存在线程池中。
>
>newFixedThreadPool（int nThreads）：创建一个可重用的、具有固定线程数的线程池。
>
>newSingleThreadExecutor() ：创建一个只有单线程的线程池，它相当于调用newFixedThreadPool() 方法时传入参数为1。
>
>newScheduledThreadPool（int corePoolSize）：创建具有指定线程数的线程池，它可以在指定延迟后执行线程任务。corePoolSize 指池中所保存的线程数，即使线程是空闲的也被保存在线程池内。
>
>newSingleThreadScheduledExecutor() ：创建只有一个线程的线程池，它可以在指定延迟后执行线程任务。
>
>ExecutorService newWorkStealingPool（int parallelism）：创建持有足够的线程的线程池来支持给定的并行级别，该方法还会使用多个队列来减少竞争。
>
>ExecutorService newWorkStealingPool() ：该方法是前一个方法的简化版本。如果当前机器有4个CPU，则目标并行级别被设置为4，也就是相当于为前一个方法传入4作为参数。

上面7个方法中的前三个方法返回一个 ExecutorService 对象，该对象代表一个线程池，它可以执行 Runnable 对象或 Callable 对象所代表的线程；

而中间两个方法返回一个 ScheduledExecutorService 线程池，它是 ExecutorService 的子类，它可以在指定延迟后执行线程任务；

最后两个方法则是 Java8 新增的，这两个方法可充分利用多CPU并行的能力。这两个方法生成的 work stealing 池，都相当于后台线程池，如果所有的前台线程都死亡了，work stealing 池中的线程会自动死亡。

ExecutorService 代表**尽快执行线程**的**线程池**（**只要线程池中有空闲线程，就立即执行线程任务**），程序只要将一个Runnable对象或Callable对象（代表线程任务）提交给该线程池，该线程池就会尽快执行该任务。ExecutorService 里提供了如下三个方法。

- Future<?>  submit( Runnable task) ：将一个 Runnable 对象提交给指定的线程池，线程池将在有空闲线程时执行 Runnable 对象代表的任务。**其中 Future 对象代表 Runnable 任务的返回值**——但 run() 方法没有返回值，所以 Future 对象将在 run() 方法执行结束后返回null。但可以调用 Future 的 isDone() 、isCancelled() 方法来获得  Runnable 对象的执行状态。
- <T>  Future<T>  submit( Runnable task，T result) ：将一个Runnable对象提交给指定的线程池，线程池将在有空闲线程时执行Runnable对象代表的任务。其中result显式指定线程执行结束后的返回值，所以 Future 对象将在 run() 方法执行结束后返回 result。
- <T>  Future<T>  submit( Callable<T> task) ：将一个 Callable 对象提交给指定的线程池，线程池将在有空闲线程时执行 Callable 对象代表的任务。**其中 Future 代表 Callable 对象里call() 方法的返回值**。

ScheduledExecutorService 代表可在指定延迟后或周期性地执行线程任务的**线程池**，它提供了如下4个方法。

- ScheduledFuture<V>  schedule( Callable<V>  callable，long delay，TimeUnit unit）：指定 callable 任务将在delay延迟后执行。unit -- 延迟参数的时间单位 (秒、毫秒。。。)
- ScheduledFuture<?>   schedule( Runnable  command，long delay，TimeUnit unit）：指定 command 任务将在 delay 延迟后执行。
- ScheduledFuture<?>   scheduleAtFixedRate( Runnable  command，long initialDelay，long period，TimeUnit unit）：指定 command 任务将在 delay 延迟后执行，而且以设定频率重复执行。也就是说，在initialDelay后开始执行，依次在initialDelay+period、initialDelay+2*period.…处**重复执行**（不管前面的结没结束），依此类推。
- ScheduledFuture<?>   scheduleWithFixedDelay( Runnable  command，long initialDelay，long delay，TimeUnit unit）：创建并执行一个在给定初始延迟后首次启用的定期操作，随后在**每一次执行终止和下一次执行开始之间都存在给定的延迟**。如果任务在任一次执行时遇到异常，就会取消后续执行；否则，只能通过程序来显式取消或终止该任务。



用完一个线程池后，应该调用该线程池的 shutdown() 方法，该方法将启动线程池的有序关闭，调用 shutdown() 方法后的线程池不再接收新任务，但会将以前所有已提交任务执行完成。当线程池中的所有任务都执行完成后，池中的所有线程都会死亡；无返回值。

另外也可以调用线程池的 shutdownNow() 方法来关闭线程池，该方法**试图停止**所有正在执行的活动任务，不再处理还在池队列中等待的任务，当然，它会返回那些正在等待执行的任务列表。（新任务不用说了，肯定不会接收的）

它试图终止线程的方法是通过调用 Thread.interrupt() 方法来实现的，但是大家知道，这种方法的作用有限，如果线程中没有sleep 、wait、Condition、定时锁等应用, interrupt() 方法是无法中断当前的线程的。所以，ShutdownNow() 并不代表线程池就一定立即就能退出，它可能必须要等待所有正在执行的任务都执行完成了才能退出。 

###### Java 8 增强的 ForkJoinPool （并行计算）

Java 7 提供了 ForkJoinPool 来支持将一个任务拆分成多个“小任务”并行计算，再把多个“小任务”
的结果合并成总的计算结果。ForkJoinPool 是 ExecutorService 的实现类，因此是一种特殊的线程池。(为了充分利用多核处理器)
ForkJoinPool提供了如下两个常用的构造器。

>ForkJoinPool（int parallelism）：创建一个包含 parallelism 个并行线程的 ForkJoinPool。
>
>ForkJoinPool（）：以 Runtime.availableProcessors（）方法的返回值作为 parallelism 参数来创建 Fork JoinPool。

Java8进一步扩展了 ForkJoinPool 的功能，Java8 为 ForkJoinPool 增加了通用池功能。ForkJoinPool 类通过如下两个静态方法提供通用池功能。

>static ForkJoinPool commonPool（）：该方法返回一个通用池，通用池的运行状态不会受shutdown() 或 shutdownNow() 方法的影响。当然，如果程序直接执行System.exit(0)；来终止虚拟机，通用池以及通用池中正在执行的任务都会被自动终止。
>
>int getCommonPoolParallelism（）：该方法返回通用池的并行级别。

创建了 ForkJoinPool 实例之后，就可调用 ForkJoinPool 的submit（ForkJoinTask task）或invoke（ForkJoinTask task）方法来执行指定任务了。其中ForkJoinTask代表一个可以并行、合并的任务。

ForkJoinTask 是一个抽象类，它还有两个抽象子类：RecursiveAction 和 Recursive Task。其中Recursive Task代表有返回值的任务，而RecursiveAction代表没有返回值的任务。

##### 9、线程相关类

###### ThreadLocal 类

ThreadLocal，是 Thread Local Variable（线程局部变量）的意思，也许将它命名为ThreadLocalVar 更加合适。线程局部变量（ThreadLocal）的功用其实非常简单，就是为**每一个使用该变量的线程都提供一个变量值的副本**，使每一个线程都可以独立地改变自己的副本，而不会和其他线程的副本冲突。从线程的角度看，就好像每一个线程都完全拥有该变量一样。
ThreadLocal<T> 类的用法非常简单，它只提供了如下三个public方法。（T为变量的类型）

>T  get（）：返回此线程局部变量中当前线程副本中的值。
>void remove（）：删除此线程局部变量中当前线程的值。
>void set（T value）：设置此线程局部变量中当前线程副本中的值。

定义在共享资源类的实例变量的地方

```java
private ThreadLocal<String> name = new ThreadLoacl<>();
```

ThreadLocal 和其他所有的**同步机制**一样，都是为了解决多线程中对同一变量的访问冲突，在普通的同步机制中，是通过对象加锁来实现多个线程对同一变量的安全访问的。

ThreadLocal从另一个角度来解决多线程的并发访问，ThreadLocal将需要并发访问的资源**复制多份，每个线程拥有一份资源，每个线程都拥有自己的资源副本**，从而也就没有必要对该变量进行同步了。

###### 包装线程不安全的集合

前面介绍 Java 集合时所讲的ArrayList、LinkedList、HashSet、TreeSet、HashMap、TreeMap等都是线程不安全的，也就是说，当多个并发线程向这些集合中存、取元素时，就可能会破坏这些集合的数据完整性。
如果程序中有多个线程可能访问以上这些集合，就可以使用Collections提供的类方法把这些集合包装成线程安全的集合。Collections提供了如下几个静态方法。

>static  <T>  Collection<T>  synchronizedCollection（Collection<T>  c）：返回指定 collection对应的线程安全的collection。
>
>static  <T>  List<T>  synchronizedList（List<T>  list）：返回指定List对象对应的线程安全的List对象。
>
>static  <K,V>  Map<K,V>  synchronizedMap（Map<K,V>  m）：返回指定Map对象对应的线程安全的Map对象。
>
>static  <T>  Set<T>  synchronizedSet（Set<T>  s）：返回指定Set对象对应的线程安全的Set对象。
>static  <K,V>  SortedMap<K,V>  synchronizedSortedMap（SortedMap<K,V>  m）：返回指定SortedMap对象对应的线程安全的SortedMap对象。
>
>static  <T>  SortedSet<T>  synchronizedSortedSet（SortedSet<T>  s）：返回指定 SortedSet对象对应的线程安全的SortedSet对象。

如果需要把某个集合包装成线程安全的集合，则应该在创建之后立即包装。注意返回的是List、Set...

###### 线程安全的集合类

实际上从 Java5 开始，在 java.util.concurrent 包下提供了大量支持高效并发访问的集合接口和实现类，如图16.19所示。

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211027230231889.png" alt="image-20211027230231889"  />

从图16.19所示的类图可以看出，这些线程安全的集合类可分为如下两类。
>以 Concurrent 开头的集合类，如 ConcurrentHashMap、ConcurrentSkipListMap、ConcurrentSkipListSet、ConcurrentLinkedQueue 和ConcurrentLinkedDeque。
>
>以CopyOnWrite 开头的集合类，如CopyOnWriteArayList、CopyOnWriteArraySet。

其中以 Concurrent 开头的集合类代表了支持并发访问的集合，它们可以支持多个线程并发写入访问，这些写入线程的所有操作都是线程安全的，但读取操作不必锁定。以Concurrent开头的集合类采用了更复杂的算法来保证永远不会锁住整个集合，因此在并发写入时有较好的性能。

当多个线程共享访问一个公共集合时，ConcurrentLinkedQueue 是一个恰当的选择。
ConcurrentLinkedQueue 不允许使用null元素。ConcurrentLinkedQueue 实现了多线程的高效访问，多个线程访问 ConcurrentLinkedQueue 集合时无须等待。

在默认情况下，ConcurrentHashMap 支持16个线程并发写入，当有超过16个线程并发向该Map中写入数据时，可能有一些线程需要等待。实际上，程序通过设置 concurrencyLevel 构造参数（默认值为16）来支持更多的并发写入线程。

与前面介绍的 HashMap 和普通集合不同的是，因为 ConcurrentLinkedQueue 和ConcurrentHashMap 支持多线程并发访问，所以当使用迭代器来遍历集合元素时，该迭代器可能不可以反映出创建迭代器之后所做的修改，但程序不会抛出任何异常。

java 8 扩展了 ConcurrentHashMap 的功能，增强后的 ConcurrentHashMap 更适合作为缓存实现类使用。

由于 CopyOnWriteArraySet 的底层封装了 CopyOnWriteArrayList，因此它的实现机制完全类似于 CopyOnWriteArrayList 集合。对于 CopyOnWriteArrayList 集合，正如它的名字所暗示的，它采用复制底层数组的方式来实现写操作。

当线程对 CopyOnWriteArrayList 集合执行**读取操作**时，**线程将会直接读取集合本身，无须加锁与阻塞**。当线程对 CopyOnWriteArrayList 集合执行写入操作时（包括调用add() 、remove() 、set() 等方法），该集合会在底层复制一份新的数组，接下来对新的数组执行写入操作，修改完毕后，再将原来的引用指向新的数组。（**源码中写入的方法都还是用了 Lock 对象来控制线程同步，这里的写时复制应该是为了？？？？**）

需要指出的是，由于 CopyOnWriteArrayList 执行写入操作时需要频繁地复制数组，性能比较差，但由于读操作与写操作不是操作同一个数组，而且读操作也不需要加锁，因此读操作就很快、很安全。由此可见，CopyOnWriteArrayList 适合用在读取操作远远大于写入操作的场景中，例如缓存等。

#### 98、网络编程

端口是一个 16 位的整数，用于表示数据交给哪个应用程序处理，不同的应用程序处理不同端口上的数据。当一个程序需要发送数据时，需要指定目的地的IP地址和端口，如果指定了正确的IP地址和端口号，计算机网络就可以将数据送给该IP地址和端口所对应的程序。

##### 1、Java 的基本网络支持

Java 为网络支持提供了 java.net 包，该包下的 URL 和 URLConnection 等类提供了以编程方式访问 Web 服务的功能，而 URLDecoder 和 URLEncoder 则提供了普通字符串和     application/x-www-form-urlencoded MIME 字符串相互转换的静态方法。

###### 使用 InetAddress

Java 提供了 **InetAddress 类**来代表**IP地址**，InetAddress 下还有两个子类：Inet4Address、Inet6Address，它们分别代表 IPv4 地址和 IPv6 地址。
InetAddress类没有提供构造器，而是提供了如下两个静态方法来获取InetAddress实例。

>getByName（String host）：根据主机名获取对应的 InetAddress 对象。主机名称可以是机器名称，例如“java.sun.com”或其IP地址的文本表示“127.0.0.1”。
>
>getByAddress（byte[] addr）：根据原始IP地址来获取对应的 InetAddress 对象。

InetAddress还提供了如下三个方法来获取InetAddress实例对应的IP地址和主机名。

- String getCanonicalHostName（）：获取此IP地址的全限定域名。
- String getHostAddress（）：返回该InetAddress实例对应的IP地址字符串（以字符串形式）。
- String getHostName（）：获取此IP地址的主机名。

除此之外，InetAddress类还提供了一个 getLocalHost() 方法来获取本机IP地址对应的 InetAddress 实例 

InetAddress类还提供了一个 isReachable( int timeout ) 方法（timeout 超时值，以毫秒为单位），用于测试是否可以到达该地址。该方法将尽最大努力试图到达主机，但防火墙和服务器配置可能阻塞请求，使得它在访问某些特定的端口时处于不可达状态。如果可以获得权限，典型的实现将使用 ICMPECHO REQUEST；否则它将试图在目标主机的端口 7（Echo）上建立TCP连接。

下面程序测试了 InetAddress 类的简单用法。

```java
	//根据主机名来获取对应的 InetAddress 实例
    InetAddress ip = InetAddress.getByName("www.crazyit.org");
    //判断是否可达
	System.out.println("crazyit 是否可达："+ ip.isReachable(2000));
	//获取该InetAddress 实例的 IP 字符串:"185.199.108.153"
	System.out.println(ip.getHostAddress());
	//获取此IP地址的主机名：“www.crazyit.org”
	System.out.println(ip.getHostName());
	//获取此IP地址的全限定域名：“cdn-185-199-108-153.github.com”
	System.out.println(ip.getCanonicalHostName());
	//根据原始IP地址来获取对应的 InetAddress 实例
	InetAddress local = InetAddress.getByAddress(new byte[]{127, 0, 0, 1});
```

###### 问题：主机名和域名

**主机名**：在局域网中，**每台主机都有一个主机名**，可以使用英文字母或者单词组成的主机名来代替该主机的IP地址（在多网卡或者路由器等的情况下，每个主机可以有多个IP）。

**域名**：域名可以认为是主机在公网环境中的标识，在公网下，**对应一个唯一的IP**。

主机名的含义是机器本身的名字，域名是方便记录IP地址才做的一种IP映射；从应用场景上可以这么简单理解二者的区别：主机名用于局域网中；域名用于公网中。

一个域名下可以有多个主机名，例如，域名abc.com下，有主机server1和server2，其主机全名就是server1.abc.com和server2.abc.com。

http://mail.163.com/index.html
1）http:   这个是协议，也就是HTTP超文本传输协议，也就是网页在网上传输的协议。
2）mail：这个是**服务器名**，代表着是一个邮箱服务器，所以是mail。（这里的服务器名，也就是主机名）
3）163.com:  这个是域名，是用来定位网站的独一无二的名字。
4）mail.163.com：这个是主机名（网站名），由服务器名+域名组成。（一般说主机名，都应该指这里的主机名，也就是主机全名）
5）/：这个是根目录，也就是说，通过网站名找到服务器，然后在服务器存放网页的根目录
6）index.html：这个是根目录下的默认网页（当然，163的默认网页是不是这个我不知道，只是大部分的默认网页，都是index.html）

举个正在使用中的**三级域名**的实例，www.ncic.ac.cn，其中www前缀表明此域名对应着万维网服务（百度百科中的例子）

**因特网上的主机或Web站点由主机名识别**

###### 使用 URLDecoder 和 URLEncoder

URLDecoder 和 URLEncoder 用于完成普通字符串和 application/x-www-form-urlencoded MIME 字符串之间的相互转换。可能有读者觉得后一个字符串非常专业，以为又是什么特别高深的知识，其实不是。

当 URL 地址里包含非西欧字符的字符串时，系统会将这些非西欧字符串转换成特殊字符串。编程过程中可能涉及普通字符串和这种特殊字符串的相关转换，这就需要使用URLDecoder和URLEncoder类。

>URLDecoder 类包含一个 decode（String s，String enc）静态方法，它可以将看上去是乱码的特殊字符串转换成普通字符串。
>
>URLEncoder 类包含一个encode（String s，String enc）静态方法，它可以将普通字符串转换成application/x-www-form-urlencoded MIME字符串。

```java
//将普通字符串编码成application/x-www-form-urlencoded MIME 字符串
String str = URLEncoder.encode("疯狂Java讲义","utf-8");
System.out.println(str);
//解码
String str1 = URLDecoder.decode(str,"utf-8");
System.out.println(str1);
```

这种编码在国内的浏览器中运用的并不多，谷歌浏览器有用到该编码。但是现在好像也没用了。

###### URL、URLConnection 和 URLPermission

URL（Uniform Resource Locator）对象代表统一资源定位器，**它是指向互联网“资源”的指针**。资源可以是简单的文件或目录，也可以是对更为复杂对象的引用，例如对数据库或搜索引擎的查询。在通常情况下，URL可以由协议名、主机、端口和资源组成，即满足如下格式（带[]的表示可省略）：

`protocol://hostname[:port]/path/[;parameters][?query]#fragment`

1. **path（路径）**：由零或多个“/”符号隔开的字符串，一般用来表示主机上的一个目录或文件地址。
2. **;parameters（参数）**：这是用于指定特殊参数的可选项。
3. **?query(查询)**：可选，用于给动态网页（如使用CGI、ISAPI、PHP/JSP/ASP/ASP.NET等技术制作的网页）传递参数，可有多个参数，用“&”符号隔开，每个参数的名和值用“=”符号隔开。
4. **fragment**（信息片断）：字符串，用于指定网络资源中的片断。例如一个网页中有多个名词解释，可使用fragment直接定位到某一名词解释。

URL类提供了多个构造器用于创建URL对象，一旦获得了URL对象之后，就可以调用如下方法来访问该URL对应的资源。
>String getFile() ：获取该URL的资源名。（resourceName）
>
>String getHost() ：获取该URL的主机名。(host ，或者是域名)
>
>String getPath() ：获取该URL的路径部分。
>
>int getPort() ：获取该URL的端口号。
>
>String getProtocol() ：获取该URL的协议名称。
>
>String getQuery() ：获取该URL的查询字符串部分。
>
>URLConnection openConnection() ：返回一个URLConnection对象，它代表了与URL所引用的远程对象的连接。
>
>InputStream openStream() ：打开与此URL的连接，并返回一个用于读取该URL资源的InputStream。通过该方法可以非常方便地读取远程资源——甚至实现多线程下载。

```java
URL url = new URL("https://www.baidu.com/s?tn=15007414_9_dg&wd=URL");
// 输出：“/s?tn=15007414_9_dg&wd=URL”
System.out.println(url.getFile());
// 输出：“www.baidu.com”
System.out.println(url.getHost());
// 输出：“/s”
System.out.println(url.getPath());
// 输出：-1
System.out.println(url.getPort());
// 输出：https
System.out.println(url.getProtocol());
//// 输出：tn=15007414_9_dg&wd=URL
System.out.println(url.getQuery());
```

URLConnection 对象表示应用程序和URL之间的通信连接，而 HttpURLConnection 对象表示与URL之间的HTTP连接。程序可以通过 URLConnection 实例向该URL发送请求、读取URL引用的资源。

Java8 新增了一个 URLPermission 工具类，用于管理 HttpURLConnection 的权限问题，如果在HttpURLConnection 安装了安全管理器，通过该对象打开连接时就需要先获得权限。

通常创建一个和URL的连接，并发送请求、读取此URL引用的资源需要如下几个步骤：

1. 通过调用URL对象的 openConnection() 方法来创建 URLConnection 对象。
2. 设置 URLConnection 的参数和普通请求属性。（不需要做，每个URLConnection的具体子类都在首部中设置一些默认的键值对，实际上只有HttpURLConnection这样做，因为HTTP是唯一以这种方式使用首部的主要协议）
3. 如果只是发送GET方式请求，则使用 connect() 方法建立和远程资源之间的实际连接即可；如果需要发送POST方式的请求，则需要获取 URLConnection 实例对应的输出流来发送请求参数。
4. 远程资源变为可用，程序可以访问远程资源的头字段或通过输入流读取远程资源的数据。

URLConnection类有7个保护的实例字段，定义了客户端如何向服务器做出请求：

```java
protected URL url;
protected boolean doInput=true; 
protected boolean doOutput=false; 
protected boolean allowUserInteraction =defaultAllowUserInteraction; 
protected boolean useCaches =defaultuseCaches; 
protected long ifModifiedSince=0; 
protected boolean connected=false;
```

配置客户端请求HTTP首部:

> setRequestProperty（String key，String value）：设该URLConnection的key 请求头字段的值为value。
>
> addRequestProperty（String key，String value）：为该URLConnection的key 请求头字段增加value值，该方法并不会覆盖原请求头字段的值，而是将新值追加到原请求头字段中。
>
> String getRequestProperty(String key) ： 获取请求头字段key对应的value
>
> Map<String,List<String>> getRequestProperties()

每个URLConnection会在首部默认设置一些不同的名–值对。（实际写代码时为了方便可以不写）

当远程资源可用之后，程序可以使用以下方法来访问头字段和内容。

>Object getContent（）：获取该URLConnection的内容。
>String getHeaderField（String name）：获取指定响应头字段的值。
>getlnputStream（）：返回该URLConnection对应的输入流，用于获取URLConnection响应的内容。
>getOutputStream（）：返回该URLConnection 对应的输出流，用于向URLConnection 发送请求参数。

getHeaderField() 方法用于根据响应头字段来返回对应的值。而某些头字段由于经常需要访问，所以Java提供了以下方法来访问特定响应头字段的值。
>getContentEncoding）：获取content-encoding响应头字段的值。
>getContentLength（）：获取content-length响应头字段的值。
>getContentType（）：获取content-type响应头字段的值。
>getDate（）：获取date响应头字段的值。
>getExpiration）：获取expires响应头字段的值。
>getLastModified（）：获取last-modified响应头字段的值。

```java
public class GetPostTest {

    /**
     * 向指定 URL发送 GET方式的请求
     * @param url  发送和请求的URL
     * @param param 请求参数，格式满足name1=value1&name2=value2的形式
     * @return URL代表远程资源的响应
     */
    public static String sendGet(String url,String param){
        String result = "";
        //请求的数据会附在 URL 之后（放在请求行中），以?分割URL和传输数据，多个参数用 & 连接。
        String urlName = url + "?" + param;
        try{
            URL realUrl = new URL(urlName);
            // 打开和URL之间的连接
            URLConnection conn = realUrl.openConnection();
            //这里不填好像是自动帮我们填？，不需要设置
            //conn.setRequestProperty("Accept","*/*");
            //conn.setRequestProperty("Connection","Keep-Alive");
            //conn.setRequestProperty("user-agent","...");
            //建立实际的连接
            conn.connect();
            //获取所有的响应头字段
            Map<String, List<String>> map = conn.getHeaderFields();
            // 遍历所有的响应头字段
            for(String key:map.keySet()){
                System.out.println(key + "--->" + map.get(key));
            }
            try(
                // 定义 BufferedReader 输入流来读取URL的响应内容，不包括响应头
                BufferedReader in = new BufferedReader(
                        new InputStreamReader(conn.getInputStream(), StandardCharsets.UTF_8))){
                String line;
                while((line = in.readLine()) != null){
                    result += "\n" + line;
                }
            }
        } catch (IOException e) {
            System.out.println("发送 GET 请求出现异常！" + e);
            e.printStackTrace();
        }
        return result;
    }

    /**
     * 向指定 URL发送 POST方式的请求
     * @param url  发送和请求的URL
     * @param param 请求参数，格式满足name1=value1&name2=value2的形式
     * @return URL代表远程资源的响应
     */
    public static String sendPost(String url,String param){
        String result = "";
        try{
            URL realUrl = new URL(url);
            // 打开和 URL 之间的连接
            URLConnection conn = realUrl.openConnection();
            // 设置通用的请求属性
            //conn.setRequestProperty("accept","*/*");
            //conn.setRequestProperty("connection","Keep-Alive");
            //conn.setRequestProperty("user-agent","...");
            //若需要向服务器提交数据，需要将doOutput属性设为true，此时请求方法将由GET变为POST。
            conn.setDoOutput(true);
            try(
                // 获取 URLConnection 对象对应的输出流
                PrintWriter out = new PrintWriter(conn.getOutputStream())){
                // 发送请求参数
                out.print(param);
                // flush 输出流的缓冲
                out.flush();
            }
            try(
                //定义 BufferedReader 输入流来读取URL的响应
                BufferedReader in = new BufferedReader(
                        new InputStreamReader(conn.getInputStream(),"utf-8"))){
                String line;
                while((line = in.readLine()) != null){
                    result += "\n" + line;
                }
            }
        } catch (IOException e) {
            System.out.println("发送 POST出现异常！" + e);
            e.printStackTrace();
        }
        return result;
    }
    // 提供主方法，测试发送 GET 请求和 POST 请求
    public static void main(String[] args) {
        // 发送 GET 请求
        String result1 = GetPostTest.sendGet("https://fanyi.baidu.com/?aldtype=16047#zh/en/%E4%BD%A0%E5%A5%BD",null);
        System.out.println(result1);

        // 发送 POST 请求
        String result2 = GetPostTest.sendPost("https://fanyi.baidu.com","query=外星人");
        System.out.println(result2);
    }
}
```

##### 2、基于TCP协议的网络编程

###### 使用 ServerSocket 创建 TCP 服务器端

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211101222112710.png" alt="image-20211101222112710" style="zoom:67%;" />

Java中能接收其他通信实体连接请求的类是 ServerSocket，ServerSocket 对象用于监听来自客户端的Socket连接，如果没有连接，它将一直处于等待状态。ServerSocket包含一个监听来自客户端连接请求的方法。

>Socket accept（）：如果接收到一个客户端Socket的连接请求，该方法将返回一个与客户端 Socket对应的Socket；否则该方法将一直处于等待状态，线程也被阻塞。

为了创建 ServerSocket 对象，ServerSocket类提供了如下几个构造器。

>ServerSocket（int port）：用指定的端口 port来创建一个ServerSocket。该端口应该有一个有效的端口整数值，即0~65535。推荐使用1024以上的端口
>
>ServerSocket（int port，int backlog）：backlog--请求进入连接队列的最大长度。这个队列的大小代表在等待中的客户端请求数，没有被accept。
>
>ServerSocket（int port，int backlog，InetAddress localAddr）：在机器存在多个IP地址的情况下，允许通过localAddr参数来指定将ServerSocket绑定到指定的IP地址。

当ServerSocket 使用完毕后，应使用ServerSocket的 close() 方法来关闭该ServerSocket。在通常情况下，服务器不应该只接收一个客户端请求，而应该不断地接收来自客户端的所有请求，所以Java程序通常会通过循环不断地调用ServerSocket的 accept() 方法。

###### 使用Socket 进行通信

客户端通常可以使用Socket的构造器来连接到指定服务器，Socket通常可以使用如下两个构造器。
>Socket（InetAddress/String remoteAddress，int port）：创建连接到指定远程主机、远程端口的Socket，该构造器没有指定本地地址、本地端口，默认使用本地主机的默认IP地址，默认使用系统动态分配的端口。
>
>Socket（InetAddress/String remoteAddress，int port，InetAddress localAddr，int localPort）：创建连接到指定远程主机、远程端口的Socket，并指定本地IP地址和本地端口，适用于本地主机有多个IP地址的情形。

```java
// 创建连接到本机、30000端口的Socket,通常使用String对象来指定远程IP地址，因为方便？
Socket s = new Socket("127.0.0.1",30000)
// 在创建对象时指定了IP和端口，则已经开始自动请求连接了
```

127.0.0.1 这个IP地址是一个特殊的地址，它总是代表本机的IP地址。

当客户端、服务器端产生了对应的Socket之后，程序无须再区分服务器端、客户端，而是通过各自的Socket进行通信。Socket提供了如下两个方法来获取输入流和输出流。
>InputStream getlnputStream（）：返回该Socket对象对应的输入流，让程序通过该输入流从Socket中取出数据。
>OutputStream getOutputStream（）：返回该Socket对象对应的输出流，让程序通过该输出流向Socket中输出数据。

看到这两个方法返回的 InputStream 和 OutputStream，读者应该可以明白Java在设计IO体系上的苦心了——不管底层的IO流是怎样的节点流：文件流也好，网络Socket产生的流也好，程序都可以将其包装成处理流，从而提供更多方便的处理。

Socket 对象提供了一个 setSoTimeout(int timeout)（单位是毫秒）来设置超时时长，如果在使用Socket 进行读、写操作完成之前超出了该时间限制（这个时间也包括了等待连接的时间），那么这些方法就会抛出 SocketTimeoutException 异常。

如果程序需要在 Socket 连接服务器时指定超时时长，可惜 Socket 的所有构造器里都没有提供超时时长的参数，只能用如下的方法设置：

```java
// 创建一个无连接的socket
Socket s = new Socket();
//如果经过10秒还没有连接上，则认为连接超时
s.connect(new InetAddress(host,post),10000)
```

###### 半关闭的Socket

在前面介绍IO时提到，如果要表示输出已经结束，则可以通过关闭输出流来实现。但在网络通信中则不能通过关闭输出流来表示输出已经结束，因为**当关闭输出流时，该输出流对应的Socket也将随之关闭**，这样导致程序无法再从该Socket的输入流中读取数据了。

在这种情况下，Socket提供了如下两个**半关闭的方法，只关闭Socket的输入流或者输出流，用以表示输出数据已经发送完成。**
>shutdownlnput（）：关闭该Socket的输入流，程序还可通过该Socket的输出流输出数据。shutdownOutput（）：关闭该Scoket的输出流，程序还可通过该Socket的输入流读取数据。（关闭后无法再次打开）

当调用 shutdownlnput() 或 shutdownOutput() 方法关闭Socket的输入流或输出流之后，该Socket处于“半关闭”状态，Socket 可通过 islnputShutdown() 方法、isOutputShutdown() 方法判断该Socket的状态。

即使同一个Socket 实例先后调用 shutdownInput() 、shutdownOutput() 方法，该Socket实例依然没有被关闭，只是该Socket既不能输出数据，也不能读取数据而已。

###### 使用 NIO 实现非阻塞Socket通信

前面介绍的网络通信程序是基于阻塞式API的——即当程序执行输入、输出操作后，在这些操作返回之前会一直阻塞该线程，所以服务器端必须为每个客户端都提供一个独立线程进行处理，当服务器端需要同时处理大量客户端时，这种做法会导致性能下降。使用 NIO API 则可以让服务器端使用一个或有限几个线程来同时处理连接到服务器端的所有客户端。

Java的NIO为非阻塞式Socket通信提供了如下几个特殊类。

Selector：它是 SelectableChannel 对象的多路复用器，所有希望采用非阻塞方式进行通信的Channe l都应该注册到 Selector 对象。可以通过调用此类的 open() 静态方法来创建 Selector实例，该方法将使用系统默认的Selector来返回新的Selector。

Selector 可以同时监控多个 SelectableChannel 的IO状况，是非阻塞IO的核心。一个Selector实例有三个SelectionKey集合。
>所有的SelectionKey集合：代表了注册在该Selector上的Channel，这个集合可以通过 keys()方法返回。
>
>被选择的SelectionKey集合：代表了所有可通过 select() 方法获取的、需要进行IO处理的Channel，这个集合可以通过selectedKeys() 返回。
>
>被取消的SelectionKey集合：代表了所有被取消注册关系的Channel，在下一次执行 select() 方法时，这些Channel对应的 SelectionKey 会被彻底删除，程序通常无须直接访问该集合。

除此之外，Selector 还提供了一系列和 select() 相关的方法，如下所示。
>int select（）：监控所有注册的Channel，当它们中间有需要处理的IO操作时，该方法返回，并将对应的 SelectionKey 加入被选择的 SelectionKey 集合中，该方法返回这些Channel的数量。（没有需要处理的IO操作就一直阻塞，调用该方法的线程被阻塞）
>
>int select（long timeout）：可以设置超时时长的select（）操作。
>
>int selectNow（）：执行一个立即返回的select（）操作，相对于无参数的select（）方法而言，该方法不会阻塞线程。
>
>Selector wakeup（）：使一个还未返回的select（）方法立刻返回。

SelectableChannel（抽象类）：它代表可以支持非阻塞IO操作的Channel对象，它可被注册到Selector上，这种注册关系由 SelectionKey 实例表示。**Selector对象提供了一个 select() 方法，该方法允许应用程序同时监控多个IO Channel**。

应用程序可调用 SelectableChannel 的 register() 方法将其注册到指定 Selector 上，当该Selector上的某些 SelectableChannel 上有需要处理的IO操作时，程序可以调用 Selector 实例的 select() 方法获取它们的数量，并可以通过 selectedKeys() 方法返回它们对应的 SelectionKey 集合——通过该集合就可以获取所有需要进行IO处理的 SelectableChannel 集。

SelectableChannel 对象支持阻塞和非阻塞两种模式（**所有的Channel默认都是阻塞模式**），必须使用非阻塞模式才可以利用非阻塞IO操作。SelectableChannel提供了如下两个方法来设置和返回该Channel的模式状态。
>SelectableChannel configureBlocking（boolean block）：设置是否采用阻塞模式。
>boolean isBlocking（）：返回该Channel是否是阻塞模式。

不同的 SelectableChannel 所支持的操作不一样，例如 ServerSocketChannel 代表一个ServerSocket，它就只支持OP_ACCEPT操作。SelectableChannel 提供了如下方法来返回它支持的所有操作。
>int validOps（）：返回一个整数值，表示这个Channel所支持的IO操作。

在 SelectionKey 中，用静态常量定义了4种IO操作：OP_READ(1)、OP_WRITE (4)、OP_CONNECT(8)、OP_ACCEPT(16)，它们任意2个、3个、4个相加的结果总是互不相同，所
以系统可以根据 validOps() 方法的返回值确定该 SelectableChannel 支持的操作。例如返回5，即可知道它支持读和写。

**SelectionKey**：该对象代表SelectableChannel和Selector之间的**注册关系**。

**ServerSocketChannel**（SelectableChannel 的子类）：支持非阻塞操作，对应于java.net.ServerSocket这个类，只支持OP_ACCEPT操作。该类也提供了 accept() 方法，功能相当于 ServerSocket 提供的 accept() 方法。

**SocketChannel（**SelectableChannel 的子类）：支持非阻塞操作，对应于 java.net.Socket 这个类，支持OP_CONNECT、OP_READ和OP_WRITE操作。这个类还实现了 ByteChannel 接口、ScatteringByteChannel 接口和 GatheringByteChannel 接口，所以可以直接通过SocketChannel来读写 ByteBuffer 对象。

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211102111948141.png" alt="image-20211102111948141" style="zoom:80%;" />

服务器上的所有 Channel 都需要向 Selector 注册。

（看的并不是很懂。。。上面SocketChannel相当于 Socket 和 Channel 的合体。。）

服务器端需要使用 ServerSocketChannel 来监听客户端的连接请求，Java对该类的设计比较难用：
它不像 ServerSocket 可以直接指定监听某个端口；而且不能使用已有的 ServerSocket 的 getChannel() 方法来获取 ServerSocketChannel 实例。程序必须先调用它的 open() 静态方法返回一个 ServerSocketChannel 实例，再使用它的 bind() 方法指定它在某个端口监听。创建一个可用的 ServerSocketChannel 需要采用如下代码片段：

```java
//通过open方法来打开一个未绑定的 ServerSocketChannel实例
ServerSocketChannel server = ServerSocketChannel.open();
InetSocketAddress isa = new InetSocketAddress("127.0.0.1"，30000);
//将该ServerSocketChanne1绑定到指定IP地址
server.bind(isa);
//设置 serverSocket以非阻塞方式工作
server.configureBlocking(false);
//将server注册到指定的Selector对象
server.register(selector，SelectionKey.OP_ACCEPT);
```

##### 3、基于 UDP 协议的网络编程

UDP协议是一种不可靠的网络协议，它在通信实例的两端各建立一个Socket，但这两个Socket之间并没有虚拟链路，这两个Socket只是发送、接收数据报的对象。

###### 使用DatagramSocket 发送、接收

Java 提供了 DatagramSocket 对象作为基于UDP协议的Socket，使用 DatagramPacket 代表 DatagramSocket 发送、接收的数据报。对于基于 UDP 协议的通信双方而言，没有所谓的客户端和服务器端的概念。

DatagramSocket 的构造器：
>DatagramSocket（）：创建一个DatagramSocket 实例，并将该对象绑定到本机默认IP地址、本机所有可用端口中随机选择的某个端口。
>DatagramSocket（int prot）：创建一个DatagramSocket实例，并将该对象绑定到本机默认IP地址、指定端口。
>DatagramSocket（int port，InetAddress laddr）：创建一个DatagramSocket实例，并将该对象绑定到指定IP地址、指定端口。

得到了 DatagramSocket 实例之后，就可以通过如下两个方法来接受和发送数据：

> receive（DatagramPacket p）：从该DatagramSocket中接收数据报。
>
> send（DatagramPacket p）：以该DatagramSocket对象向外发送数据报。

使用 DatagramSocket 发送数据报时，DatagramSocket 并不知道将该数据报发送到哪里，**而是由DatagramPacket 自身决定数据报的目的地**。

下面看一下DatagramPacket的构造器。
>DatagramPacket（byte[] buf，int length）：以一个**空数组**来创建 DatagramPacket对象，该对象的作用是**接收** DatagramSocket 中的数据。
>
>DatagramPacket（byte[] buf，int length，InetAddress addr，int port）：以一个包含数据的数组来创建DatagramPacket对象用于**发送**，创建该DatagramPacket对象时还指定了IP地址和端口——这就决定了该数据报的目的地。
>
>DatagramPacket（byte[] buf，int offset，int length）：以一个**空数组**来创建DatagramPacket 对象，并指定**接收**到的数据放入 buf 数组中时从offset开始，最多放length个字节。
>
>DatagramPacket（byte[] buf，int offset，int length，InetAddress address，int port）：创建一个用于**发送**的DatagramPacket对象，指定发送 buf 数组中从offset开始，总共length个字节。

当服务器端（也可以是客户端）接收到一个 DatagramPacket 对象后，如果想向该数据报的发送者“反馈”一些信息，但由于UDP协议是面向非连接的，所以接收者并不知道每个数据报由谁发送过来，但程序可以**调用 DatagramPacket 的如下三个方法来获取发送者的IP地址和端口。**
>InetAddress getAddress（）：当程序准备发送此数据报时，该方法返回此数据报的目标机器的IP地址；当程序刚接收到一个数据报时，该方法返回该数据报的发送主机的IP地址。
>
>int getPort（）：当程序准备发送此数据报时，该方法返回此数据报的目标机器的端口；当程序刚接收到一个数据报时，该方法返回该数据报的发送主机的端口。
>
>SocketAddress getSocketAddress（）：当程序准备发送此数据报时，该方法返回此数据报的目标SocketAddress；当程序刚接收到一个数据报时，该方法返回该数据报的发送主机的SocketAddress。

DatagramPacket的方法：

- byte[]  getData()：返回数据缓冲区，就是传给其构造器的字节数组
- void  setData(byte[] buf)：设置此数据包的数据缓冲区

###### 使用 MulticastSocket 实现多点广播

DatagramSocket 只允许数据报发送给指定的目标地址，而 MulticastSocket 可以将数据报以广播方式发送到多个客户端。

若要使用多点广播，则需要让一个数据报标有一组目标主机地址，当数据报发出后，整个组的所有主机都能收到该数据报。IP多点广播（或多点发送）实现了将单一信息发送到多个接收者的广播，其思想是**设置一组特殊网络地址作为多点广播地址**，每一个多点广播地址都被看做一个组，当客户端需要发送、接收广播信息时，加入到该组即可。（组播地址）

IP协议为多点广播提供了这批特殊的IP地址，这些IP地址的范围是224.0.0.0至239.255.255.255。

MulticastSocket 有点像 DatagramSocket，事实上MulticastSocket是DatagramSocket的一个子类。MulticastSocket提供了如下三个构造器。
>public MulticastSocket（）：使用本机默认地址、随机端口来创建 MulticastSocket对象。
>public MulticastSocket（int portNumber）：使用本机默认地址、指定端口来创建MulticastSocket对象。
>public MulticastSocket（SocketAddress bindaddr）：使用本机指定IP地址、指定端口来创建MulticastSocket对象。

创建 MulticastSocket 对象后，还需要将该 MulticastSocket 加入到指定的多点广播地址，MulticastSocket 使用 joinGroup() 方法加入指定组；使用 leaveGroup() 方法脱离一个组。（组播地址和上面创建 MulticastSocket 对象的用到的IP地址不一样）
>joinGroup（InetAddress multicastAddr）：将该MulticastSocket加入指定的多点广播地址。
>leaveGroup（InetAddress multicastAddr）：让该MulticastSocket 离开指定的多点广播地址。

在某些系统中，可能有多个网络接口。这可能会给多点广播带来问题，这时候程序需要**在一个指定的网络接口上监听**，通过调用  setlnterface(InetAddress inf)  方法可以强制MulticastSocket使用指定的网络接口；也可以使用 getlnterface() 方法查询MulticastSocket监听的网络接口。

MulticastSocket 用于发送、接收数据报的方法与 DatagramSocket 完全一样。但MulticastSocket 比 DatagramSocket 多了一个setTimeToLive（int ttl）方法，该ttl参数用于设置数据报最多可以跨过多少个网络，当ttl的值为0时，指定数据报应停留在本地主机；当ttl的值为1时，指定数据报发送到本地局域网；当ttl的值为32时，意味着只能发送到本站点的网络上；当ttl的值为64时，意味着数据报应保留在本地区；当ttl的值为128时，意味着数据报应保留在本大洲；当ttl的值为255时，意味着数据报可发送到所有地方；在默认情况下，该ttl的值为1。

##### 4、使用代理服务器

从 Java5 开始，Java 在 java.net 包下提供了 Proxy 和 ProxySelector 两个类，其中Proxy代表一个代理服务器，可以在打开 URLConnection 连接时指定Proxy，创建Socket连接时也可以指定Proxy；而 ProxySelector 代表一个代理选择器，它提供了对代理服务器更加灵活的控制，它可以对HTTP、HTTPS、FTP、SOCKS等进行分别设置，而且还可以设置不需要通过代理服务器的主机和地址。通过使用ProxySelector，可以实现像在Internet Explorer、Firefox等软件中设置代理服务器类似的效果。



**代理服务器的功能**就是代理用户去取得网络信息。当使用浏览器直接连接其他 Internet 站点取得网络信息时，通常需要先发送请求，然后等响应到来。**代理服务器是介于浏览器和服务器之间的一台服务器**，设置了代理服务器之后，浏览器不是直接向Web服务器发送请求，而是向代理服务器发送请求，浏览器请求被先送到代理服务器，由代理服务器向真正的Web服务器发送请求，并取回浏览器所需要的信息，再送回给浏览器。由于大部分代理服务器都具有缓冲功能，它会不断地将新取得的数据存储到代理服务器的本地存储器上，如果浏览器所请求的数据在它本机的存储器上已经存在而且是最新的，那么它就无须从Web服务器取数据，而直接将本地存储器上的数据送回浏览器，这样能显著提高浏览速度。归纳起来，代理服务器主要提供如下两个功能。

- 突破自身IP限制，对外隐藏自身IP地址。**突破IP限制包括访问国外受限站点**，访问国内特定单位、团体的内部资源。
- 提高访问速度，代理服务器提供的缓冲功能可以避免每个用户都直接访问远程主机，从而提高客户端访问速度。

###### 直接使用 Proxy 创建连接

Proxy 有一个构造器：Proxy(Proxy.Type  type，SocketAddress  sa)，用于创建表示代理服务器的Proxy对象。其中sa参数指定代理服务器的地址，type表示该代理服务器的类型，该服务器类型有如下三种。
>Proxy.Type.DIRECT：表示直接连接，不使用代理。
>Proxy.Type.HTTP：表示支持高级协议代理，如HTTP或FTP。
>Proxy.Type.SOCKS：表示SOCKS（V4或V5）代理。

一旦创建了Proxy对象之后，程序就可以在使用URLConnection 打开连接时，或者创建Socket连接时传入一个Proxy对象，作为本次连接所使用的代理服务器。

其中URL包含了一个 URLConnection  openConnection(Proxy proxy)方法，该方法使用指定的代理服务器来打开连接；而Socket则提供了一个 Socket(Proxy proxy) 构造器，该构造器使用指定的代理服务器创建一个没有连接的Socket对象。(其他Socket好像没有可以使用代理的方法)

###### 使用 ProxySelector 自动选择代理服务器

ProxySelector 代表一个代理选择器，它本身是一个抽象类，程序无法创建它的实例，开发者可以考虑继承 ProxySelector 来实现自己的代理选择器。实现 ProxySelector 的步骤非常简单，程序只要定义一个继承 ProxySelector 的类，并让该类实现如下两个抽象方法。
>List<Proxy>   select（URI uri）：根据业务需要返回代理服务器列表，如果该方法返回的集合中只包含一个Proxy，该Proxy将会作为默认的代理服务器。（对于传入的uri来说，返回列表里的 proxy 都可以作为代理服务）
>
>connectFailed（URI uri，SocketAddress sa，IOException ioe）：连接代理服务器失败时回调该方法。

实现了自己的 ProxySelector 类之后，调用 ProxySelector 的 setDefault(ProxySelector ps) 静态方法来注册该代理选择器即可。

注册代理选择器后，在打开URLConnection或Socket时，会默认设置一个代理服务器（不用显式传入）。根据重写的 select 方法返回的代理服务器列表选择合适的。系统实际上已经有了一个默认代理选择器（如下），我们这么设置应该是用自己实现的 ProxySelector 类的实例替代了那个默认代理选择器。

除此之外，Java 为 ProxySelector 提供了一个实现类：sun.net.spi.DefaultProxySelector（这是一个未公开API，应尽量避免直接使用该API），**系统已经将 DefaultProxySelector注册成默认的代理选择器**，因此程序可调用 ProxySelector.getDefault() 方法来获取 DefaultProxySelector 实例。

DefaultProxySelector 继承了 ProxySelector，当然也实现了两个抽象方法，它的实现策略如下。

>connectFailed() ：如果连接失败，DefaultProxySelector 将会尝试不使用代理服务器，直接连接远程资源。
>
>select() ：DefaultProxySelector **会根据系统属性来决定使用哪个代理服务器**。ProxySelector 会检测系统属性与URL之间的匹配，然后决定使用相应的属性值作为代理服务器。关于代理服务器常用的属性名有如下三个。
>
>- http.proxyHost：设置HTTP访问所使用的代理服务器的主机地址。该属性名的前缀可以改为https、ftp等，分别用于设置HTTPS访问和FTP访问所用的代理服务器的主机地址。
>- http.proxyPort：设置HTTP访问所使用的代理服务器的端口。该属性名的前缀可以改为https、ftp等，分别用于设置HTTPS访问和FTP访问所用的代理服务器的端口。
>- http.nonProxyHosts：设置HTTP访问中不需要使用代理服务器的主机，支持使用*通配符；支持指定多个地址，多个地址之间用竖线（|）分隔。

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211103204519197.png" alt="image-20211103204519197" style="zoom:80%;" />

#### 99、类加载机制与反射

##### 1、类的加载、连接和初始化

系统可能在第一次使用某个类时加载该类，也可能采用预加载机制来加载某个类。

###### JVM 

当**调用 java 命令运行某个 Java 程序时，该命令将会启动一个 Java 虚拟机进程**，不管该Java 程序有多么复杂，该程序启动了多少个线程，它们都处于该 Java 虚拟机进程里。正如前面介绍的，同一个 JVM 的所有线程、所有变量都处于同一个进程里，它们都使用该JVM 进程的内存区。当系统出现以下几种情况时，JVM 进程将被终止。
>程序运行到最后正常结束。
>
>程序运行到使用 System.exit() 或 Runtime.getRuntime().exit() 代码处结束程序。
>
>程序执行过程中遇到未捕获的异常或错误而结束。
>
>程序所在平台强制结束了JVM进程。

###### 类的加载

当程序主动使用某个类时，如果该类还未被加载到内存中，则系统会通过加载、连接、初始化三个步骤来对该类进行初始化。如果没有意外，JVM将会连续完成这三个步骤，所以有时也把这三个步骤统称为类加载或类初始化。

类加载指的是将类的class文件读入内存，并为之创建一个java.lang.Class对象，也就是说，当程序中使用任何类时，系统都会为之建立一个 java.lang.Class 对象（类对象）。**系统中所有的类实际上也是实例，它们都是 java.lang.Class 的实例。**

类的加载由类加载器完成，类加载器通常由 JVM 提供，这些类加载器也是前面所有程序运行的基础，JVM 提供的这些类加载器通常被称为系统类加载器。除此之外，开发者可以通过继承 ClassLoader 基类来创建自己的类加载器。

通过使用不同的类加载器，可以从不同来源加载类的二进制数据，通常有如下几种来源。
>从本地文件系统加载class文件，这是前面绝大部分示例程序的类加载方式。
>
>从 JAR 包加载class文件，这种方式也是很常见的，前面介绍JDBC编程时用到的数据库驱动类就放在JAR文件中，JVM可以从JAR文件中直接加载该class文件。
>
>通过网络加载class文件。
>
>把一个Java源文件动态编译，并执行加载。

类加载器通常无须等到“首次使用”该类时才加载该类，Java虚拟机规范允许系统预先加载某些类。

###### 类的连接

当类被加载之后，系统为之生成一个对应的Class对象，接着将会进入连接阶段，连接阶段负责把类的二进制数据合并到 JRE 中。类连接又可分为如下三个阶段。

1. 验证：验证阶段用于检验被加载的类是否有正确的内部结构，并和其他类协调一致。
2. 准备：类准备阶段则负责为类的**类变量分配内存，并设置默认初始值**。
3. 解析：将类的二进制数据中的符号引用替换成直接引用。

###### 类的初始化

在类的初始化阶段，虚拟机负责对类进行初始化，主要就是**对类变量进行初始化**。在 Java类中对类变量指定初始值有两种方式：①声明类变量时指定初始值；②使用静态初始化块为类变量指定初始值。

```java
public class Test{
    //声明变量a时指定初始值
    static int a = 5;
    static int b;
    static{
        //使用静态初始化块为变量b指定初始值
        b = 6;
    }
}
```

JVM初始化一个类包含如下几个步骤：

1. 假如这个类还没有被加载和连接，则程序先加载并连接该类。
2. 假如该类的直接父类还没有被初始化，则先初始化其直接父类。
3. 假如类中有初始化语句，则系统依次执行这些初始化语句。

当执行第2个步骤时，系统对直接父类的初始化步骤也遵循此步骤1～3；如果该直接父类又有直接父类，则系统再次重复这三个步骤来先初始化这个父类……依此类推，所以 JVM最先初始化的总是 java.lang.Object 类。**当程序主动使用任何一个类时，系统会保证该类以及所有父类（包括直接父类和间接父类）都会被初始化。**

**孙**(加载、连接) -> **子**(加载、连接) -> **父**(加载、连接) -> **父**(初始化) -> **子**(初始化) -> **孙**(初始化) 

###### 类初始化的时机

当 Java 程序首次通过下面6种方式来使用某个类或接口时，系统就会初始化该类或接口。（这里的初始化包括了前面的三个步骤）
>**创建类的实例**。为某个类创建实例的方式包括：使用new操作符来创建实例，通过反射来创建实例，通过反序列化的方式来创建实例。
>
>调用某个类的类方法（静态方法）。
>
>访问某个类或接口的类变量，或为该类变量赋值。
>
>使用反射方式来强制创建某个类或接口对应的 java.lang.Class 对象。例如代码：
>Class.forName（"Person"），如果系统还未初始化Person类，则这行代码将会导致该Person类被初始化，并返回Person类对应的java.lang.Class对象。
>
>初始化某个类的子类。当初始化某个类的子类时，该子类的所有父类都会被初始化。
>
>直接使用java.exe命令来运行某个主类。当运行某个主类时，程序会先初始化该主类。

除此之外，需要特别指出的是：

对于一个 final 型的类变量，如果该**类变量的值在编译时就可以确定下来**，那么这个类变量相当于“宏变量”。Java 编译器会在编译时直接把这个类变量出现的地方替换成它的值，因此即使程序使用该静态类变量，也不会导致该类的初始化。例如下面示例程序的结果。

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211103222731458.png" alt="image-20211103222731458" style="zoom: 67%;" />

上面程序中①处的粗体字代码在编译时就会被替换成“疯狂Java讲义”，所以①行代码不会导致初始化MyTest类，这里相当于在使用字符串常量。

反之，如果 final 修饰的类变量的值**不能在编译时确定下来**，则必须等到运行时才可以确定该类变量的值，如果通过该类来访问它的类变量，则**会导致该类被初始化**。

##### 2、类加载器

类加载器负责将.class文件（可能在磁盘上，也可能在网络上）加载到内存中，并为之生成对应的 java.lang.Class 对象。尽管在 Java 开发中无须过分关心类加载机制，但所有的编程人员都应该了解其工作机制，明白如何做才能让其更好地满足我们的需要。

###### 类加载器简介

一旦一个类被载入 JVM 中，同一个类就不会被再次载入了。现在的问题是，怎么样才算“同一个类”？

正如一个对象有一个唯一的标识一样，一个载入 JVM 的类也有一个唯一的标识。**在Java中，一个类用其全限定类名（包括包名和类名）作为标识；但在JVM中，一个类用其全限定类名和其类加载器作为其唯一标识。**例如，如果在 pg 的包中有一个名为 Person 的类，被类加载器 ClassLoader 的实例 kl 负责加载，则该 Person 类对应的Class对象在JVM中表示为（Person、pg、kl）。这意味着两个类加载器加载的同名类：（Person、pg、kl）和（Person、pg、kl2）是不同的、它们所加载的类也是完全不同、互不兼容的。

当 JVM 启动时，会形成由三个类加载器组成的初始类加载器层次结构。
>Bootstrap ClassLoader：根类加载器。
>
>Extension ClassLoader：扩展类加载器。
>
>System ClassLoader：系统类加载器。

**Bootstrap ClassLoader **主要加载 JVM 自身工作需要的类，如java.lang.、java.uti.等； 这些类（如String、System）位于 $JAVA_HOME/jre/lib/rt.jar。Bootstrap ClassLoader不继承自ClassLoader，因为它不是一个普通的Java类，底层由C++编写，已嵌入到了JVM内核当中，当JVM启动后，Bootstrap ClassLoader也随着启动，负责加载完核心类库后，并构造Extension ClassLoader和App ClassLoader类加载器。

**Extension Classloader** 被称为扩展类加载器，它负责加载位于 $JAVA_HOME/jre/lib/ext目录下的扩展 jar 中的类。查找范围为System.getProperty(“java.ext.dirs”)（可能还包括其他目录）

**System Classloader** 被称为系统（也称为应用）类加载器，它负责加载 classpath 下的类，查找范围System.getProperty(“java.class.path”)。程序可以通过ClassLoader的静态方法 getSystemClassLoader() 来获取系统类加载器。如果没有特别指定，则用户自定义的类加载器都以该类加载器作为父加载器。

**系统类加载器是 AppClassLoader 的实例，扩展类加载器是 ExtClassLoader 的实例。**

###### 类加载机制

JVM的类加载机制主要有如下三种。

- 全盘负责。所谓全盘负责，就是当一个类加载器负责加载某个Class时，该Class所依赖的和引用的其他Class也将由该类加载器负责载入，除非显式使用另外一个类加载器来载入。
- 父类委托。所谓父类委托，则是先让parent（父）类加载器试图加载该Class，只有在父类加载器无法加载该类时才尝试从自己的**类路径**中加载该类。
- 缓存机制。缓存机制将会保证所有加载过的Class都会被缓存，当程序中需要使用某个Class时，类加载器先从缓存区中搜寻该Class，只有当缓存区中不存在该Class对象时，系统才会读取该类对应的二进制数据，并将其转换成Class对象，存入缓存区中。这就是为什么修改了Class后，必须重新启动 JVM，程序所做的修改才会生效的原因。

**注意：**类加载器之间的父子关系并不是类继承上的父子关系，**这里的父子关系是类加载器实例之间的关系。**使用组合关系来复用父加载器的代码。

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211104213005700.png" alt="image-20211104213005700" style="zoom: 67%;" />

###### 创建并使用自定义的类加载器

JVM中除根类加载器之外的所有类加载器都是 ClassLoader 子类的实例。

ClassLoader 类有如下两个关键方法。
>loadClass（String name，boolean resolve）：该方法为ClassLoader的入口点，根据指定名称来加载类，系统就是调用 ClassLoader 的该方法来获取指定类对应的Class对象。
>
>findClass（String name）：根据指定名称来查找类。

如果需要实现自定义的ClassLoader，则可以通过重写以上两个方法来实现，通常推荐重写 findClass() 方法，而不是重写 loadClas() 方法。loadClass() 方法的执行步骤如下:

1. 用 findLoadedClass（String）来检查是否已经加载类，如果已经加载则直接返回。
2. 在父类加载器上调用 loadClass() 方法。如果父类加载器为null，则使用根类加载器来加载。
3. 调用findClass（String）方法查找类。（自己来加载）

从上面步骤中可以看出，重写 findClass() 方法可以**避免覆盖默认类加载器的父类委托、缓冲机制两种策略**；如果重写 loadClass() 方法，则实现逻辑更为复杂。

###### URLClassLoader 类

Java为 ClassLoader 提供了一个 URLClassLoader 实现类，该类也是系统类加载器和扩展类加载器的父类（此处的父类，就是指类与类之间的继承关系）。URLClassLoader功能比较强大，它既可以从本地文件系统获取二进制文件来加载类，也可以从远程主机获取二进制文件来加载类。

在应用程序中可以直接使用URLClassLoader加载类，URLClassLoader类提供了如下两个构造器。

>URLClassLoader（URL[]  urls）：使用默认的父类加载器创建一个ClassLoader对象，该对象将从urls所指定的系列路径来查询并加载类。
>
>URLClassLoader（URL[]  urls，ClassLoader parent）：使用指定的父类加载器创建一个ClassLoader对象，其他功能与前一个构造器相同。

一旦得到了URLClassLoader对象之后，就可以调用该对象的 loadClass() 方法来加载指定类。

这里的URL可以以 “file：” 为前缀，表明从本地文件系统加载；可以以 “http：” 为前缀，表明从互联网通过HTTP访问来加载；也可以以 “ftp：” 为前缀，表明从互联网通过FTP访问来加载……功能非常强大。

File 协议，基本的格式如下：**file:///文件路径**，比如要打开F盘flash文件夹中的1.swf文件，那么可以在资源管理器或IE地址栏中键入：file:///f:/flash/1.swf 并回车

##### 3、通过反射查看类信息

Java 程序中的许多对象在运行时都会出现两种类型：编译时类型和运行时类型，例如代码：Person p = new Student()；这行代码将会生成一个p变量，该变量的编译时类型为Person，运行时类型为 Student。

为了解决这些问题，程序需要在运行时发现对象和类的真实信息。解决该问题有以下两种做法。

- 第一种做法是假设在编译时和运行时都完全知道类型的具体信息，在这种情况下，可以先使用 instanceof 运算符进行判断，再利用强制类型转换将其转换成其运行时类型的变量即可。
- 第二种做法是编译时根本无法预知该对象和类可能属于哪些类，程序只依靠运行时信息来发现该对象和类的真实信息，这就必须使用反射。

###### 获得 Class 对象

前面已经介绍过了，每个类被加载之后，系统就会为该类生成一个对应的 Class 对象，通过该 Class 对象就可以访问到 JVM 中的这个类。在Java程序中获得Class对象通常有如下三种方式:

- 使用 Class 类的 forName（String clazzName）静态方法。该方法需要传入字符串参数，该字符串参数的值是某个类的全限定类名（必须添加完整包名）。
- 调用某个类的 class 属性（static）来获取该类对应的Class对象。例如，Person.class将会返回Person类对应的Class对象。
- 调用某个对象的 getClass() 方法。该方法是 java.lang.Object 类中的一个方法，所以所有的 Java 对象都可以调用该方法，该方法将会返回该对象所属类对应的Class对象。

大部分时候都应该使用第二种方式来获取指定类的 Class 对象，优势如下：程序在编译阶段就可以检查需要访问的 Class 对象是否存在；无须调用方法，所以性能更好。

###### 从 Class 中获取信息

Class类提供了大量的实例方法**来获取该 Class 对象所对应类的详细信息**，Class类大致包含如下方法，下面每个方法都可能包括多个重载的版本，读者应该查阅API文档来掌握它们。

String.class 的类型是 Class<String>


下面4个方法用于获取Class对应类所包含的构造器。
>Constructor<T>   getConstructor（Class<?>...parameterTypes）：返回此 Class对象对应类的、带指定形参列表的public构造器。
>
>Constructor<?>[]  getConstructors()：返回此Class对象对应类的所有public构造器。
>
>Constructor<T>   getDeclaredConstructor（Class<?>...parameterTypes）：返回此Class对象对应类的、带指定形参列表的构造器，与构造器的访问权限无关。
>
>Constructor<?>[]  getDeclaredConstructors() ：返回此Class对象对应类的所有构造器，与构造器的访问权限无关。

Constructor<T> 表示的是T类的构造器

```java
Class cl = Person.class;
//获取到 Person(String name,int age) 的构造函数
Constructor con = cl.getConstructor(String.class,int.class);

Object obj = con.newInstance("张三",23);
```

下面4个方法用于获取 Class 对应类所包含的方法。
>Method getMethod（String name，Class<?>...parameterTypes）：返回此Class对象对应类的、带指定形参列表的public方法。(name是方法名)
>
>Method[] getMethods ()：返回此Class对象所表示的类的所有public方法。
>
>Method getDeclaredMethod（String name，Class<?>...parameterTypes）：返回此Class对象对应类的、带指定形参列表的方法，与方法的访问权限无关。
>
>Method[] getDeclaredMethods() ：返回此Class对象对应类的全部方法，与方法的访问权限无关。

如下4个方法用于访问 Class 对应类所包含的成员变量。
>Field  getField（String name）：返回此Class对象对应类的、指定名称为name的public成员变量。
>
>Field[]  getFields() ：返回此Class对象对应类的所有public成员变量。
>
>Field  getDeclaredField（String name）：返回此Class对象对应类的、指定名称的成员变量，与成员变量的访问权限无关。
>
>Field[]  getDeclaredFields() ：返回此Class对象对应类的全部成员变量，与成员变量的访问权限无关。

如下方法用于获取 Class 对象对应类的修饰符、所在包、类名等基本信息。
>int getModifiers() ：返回此类或接口的所有修饰符。修饰符由public、protected、private、final、static、abstract等对应的常量组成，返回的整数应使用Modifier工具类的方法来解码，才可以获取真实的修饰符。
>
>Package getPackage() ：获取此类的包。
>
>String getName() ：以字符串形式返回此Class对象所表示的类的名称，全限定类名
>
>String getSimpleName() ：以字符串形式返回此Class对象所表示的类的简称。

###### Java 8 新增的方法参数反射

Java 8在 java.lang.reflect 包下新增了一个 Executable 抽象基类，该对象代表可执行的类成员，该类派生了Constructor、Method两个子类。

Executable 基类提供了大量方法来获取修饰该方法或构造器的注解信息；还提供了isVarArgs() 方法用于判断该方法或构造器是否包含数量可变的形参，以及通过getModifiers() 方法来获取该方法或构造器的修饰符。除此之外，Executable提供了如下**两个方法来获取该方法或参数的形参个数及形参名**。

>int getParameterCount () ：获取该构造器或方法的形参个数。
>Parameter[]  getParameters ()：获取该构造器或方法的所有形参。

上面第二个方法返回了一个 Parameter[] 数组，Parameter 也是 Java8 新增的API，**每个Parameter 对象代表方法或构造器的一个参数**。Parameter也提供了大量方法来获取声明该参数的泛型信息，还提供了如下常用方法来获取参数信息。
>int getModifiers()：获取修饰该形参的修饰符。(如final)
>
>String getName()：获取形参名。
>
>Type getParameterizedType()：获取带泛型的形参类型。
>
>Class<?>  getType()：获取形参类型。
>
>boolean isNamePresent() ：该方法返回该类的class文件中是否包含了方法的参数名信息。
>
>boolean isVarArgs()：该方法用于判断该参数是否为个数可变的形参。

```java
public class Demo13 {
    public static void main(String[] args) throws NoSuchMethodException {
        Class<Test> clazz = Test.class;
        Method print = clazz.getMethod("print",String.class,List.class);
        System.out.println("print 方法参数个数：" + print.getParameterCount());
        for (Parameter p : print.getParameters()) {
            System.out.println("参数名："+p.getName());
            System.out.println("形参类型："+p.getType());
            System.out.println("泛型类型："+p.getParameterizedType());
            // 出现参数名为arg0 和 修饰符返回值为0 的情况
            // 是由于软件编译的问题，没有在class文件中保存方法的参数信息，可以在设置里更改
            System.out.println(p.getModifiers());
        }
    }
}
class Test {
    public void print(final String str, List<String> list) {}
}
//输出
print 方法参数个数：2
参数名：arg0
形参类型：class java.lang.String
泛型类型：class java.lang.String
0
参数名：arg1
形参类型：interface java.util.List
泛型类型：java.util.List<java.lang.String>
0
```

##### 4、使用反射生成并操作对象

Class 对象可以获得该类里的方法（由Method对象表示）、构造器（由Constructor对象表示）、成员变量（由Field对象表示），这三个类都位于java.lang.reflect包下，并实现了java.lang.reflect.Member接口。程序可以通过Method对象来执行对应的方法，通过Constructor对象来调用对应的构造器创建实例，能通过Field对象直接访问并修改对象的成员变量值。

###### 创建对象

通过反射来生成对象有如下两种方式。

- 使用**Class对象的 newlnstance() 方法**来创建该Class对象对应类的实例，这种方式要求该 Class 对象的对应类有**默认构造器**，而执行newlnstance() 方法时实际上是利用默认构造器来创建该类的实例。（**该类要有空参构造器**）
- 先使用Class对象获取指定的 Constructor 对象，再调用 Constructor 对象的 newInstance() 方法来创建该Class对象对应类的实例。通过这种方式可以选择使用指定的构造器来创建实例。

通过第一种方式来创建对象是比较常见的情形，因为在很多 JavaEE 框架中都需要根据配置文件信息来创建Java对象，从配置文件读取的只是某个类的字符串类名，程序需要根据该字符串来创建对应的实例，就必须使用反射。

###### 调用方法

当获得某个类对应的Class对象后，就可以通过该Class对象的 getMethods() 方法或者 getMethod() 方法来获取全部方法或指定方法——这两个方法的返回值是 Method 数组，或者 Method 对象。

每个 Method 对象对应一个方法，获得 Method 对象后，程序就可通过该 Method 来调用它对应的方法。在Method里包含一个 invoke() 方法，该方法的签名如下。

- Object invoke（Object obj，Object... args）：该方法中的obj是执行该方法的主调（谁来执行这个方法），后面的args是执行该方法时传入该方法的实参。

当通过Method的 invoke() 方法来调用对应的方法时，Java会要求程序（当前类）必须有调用该方法的权限。如果程序确实需要调用某个对象的 private 方法，则可以先调用Method对象的如下方法。

- setAccessible（boolean flag）：将Method对象的 accessible 设置为指定的布尔值。**值为true，指示该Method在使用时应该取消Java语言的访问权限检查**；值为false，则指示该Method在使用时要实施Java语言的访问权限检查。

实际上，setAccessible() 方法并不属于Method，而是属于它的父类AccessibleObject。
**因此Method、Constructor、Field都可调用该方法**，从而实现通过反射来调用private方法、private 构造器和private 成员变量。

###### 访问成员变量值

通过Class对象的 getFields() 或 getField() 方法可以获取该类所包括的全部成员变量或指定成员变量。
Field提供了如下两组方法来读取或设置成员变量值。

>getXxx（Object obj）：获取 obj 对象的该成员变量的值。此处的Xxx对应8种基本类型，如果该成员变量的类型是引用类型，则取消get后面的Xxx。
>
>setXxx（Object obj，Xxx val）：将obj对象的该成员变量设置成val值。此处的Xxx对应8种基本类型，如果该成员变量的类型是引用类型，则取消set后面的Xxx。

###### 操作数组

在 java.lang.reflect 包下还提供了一个 Array 类，Array 对象可以代表所有的数组。程序可以通过使用Array来动态地创建数组，操作数组元素等。
Array提供了如下几类方法。

>static  Object  newInstance（Class<?>  componentType，int... length）：创建一个具有指定的元素类型、指定维度的新数组。
>
>static  xxx  getXxx（Object array，int index）：返回array数组中第index个元素。其中xxx是各种基本数据类型，如果数组元素是引用类型，则该方法变为 **Object** get（Object array，int index）。
>
>static  void  setXxx（Object array，int index，xxx val）：将array 数组中第index个元素的值设为val。
>其中xxx是各种基本数据类型，如果数组元素是引用类型，则该方法变成 set（Object array，int index，Object val）。

```java
// 创建一个元素类型为String，长度为10的数组
Object arr = Array.newInstance(String.class,10);
Array.set(arr,0,"我爱中国");
String str = (String)Array.get(arr,0);
System.out.println(str);
```

##### 5、使用反射生成JDK动态代理

在 Java 的 java.lang.reflect 包下提供了一个 Proxy 类和一个 InvocationHandler 接口，通过使用这个类和接口可以生成JDK动态代理类或动态代理对象。

###### 使用  Proxy 和 InvocationHandler 创建动态代理

Proxy 提供了用于创建动态代理类和代理对象的静态方法，它也是所有动态代理类的父类。如果在程序中为一个或多个接口动态地生成实现类，就可以使用Proxy来创建动态代理类；如果需要为一个或多个接口动态地创建实例，也可以使用Proxy来创建动态代理实例。

Proxy提供了如下两个方法来**创建动态代理类和动态代理实例**。

>static Class<?>  getProxyClass( ClassLoader loader，Class<？>...interfaces)：创建一个动态代理类所对应的Class对象，该代理类将实现interfaces 所指定的多个接口。第一个ClassLoader参数指定生成动态代理类的类加载器。
>
>static Object newProxyInstance（ClassLoader loader，Class<？>[]  interfaces，InvocationHandler h）：直接创建一个动态代理对象，**该代理对象的实现类实现了interfaces 指定的系列接口，执行代理对象的每个方法时都会被替换执行InvocationHandler 对象的 invoke 方法。**

实际上，即使采用第一个方法生成动态代理类之后，如果程序需要通过该代理类来创建对象，依然需要传入一个 InvocationHandler 对象。也就是说，系统生成的每个代理对象都有一个与之关联的 InvocationHandler 对象。

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211115225822529.png" alt="image-20211115225822529" style="zoom: 80%;" />

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211115225053441.png" alt="image-20211115225053441" style="zoom:80%;" />

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211115225120459.png" alt="image-20211115225120459" style="zoom:80%;" />

<img src="C:\Users\奇乐\AppData\Roaming\Typora\typora-user-images\image-20211115225416564.png" alt="image-20211115225416564" style="zoom:80%;" />

实际上，在普通编程过程中，确实无须使用动态代理，但在编写框架或底层基础代码时，动态代理的作用就非常大。

##### 6、反射和泛型

###### 泛型和Class类

从 JDK5 以后，Java 的 Class 类增加了泛型功能，从而允许使用泛型来限制 Class 类，例如，String.class 的类型实际上是 Class<String>。如果Class对应的类暂时未知，则使用Class<?>。**通过在反射中使用泛型，可以避免使用反射生成的对象需要强制类型转换**。

Class<T> 类型的实例调用方法 newInstance() 返回的是一个 T 对象，而不是Object对象。

同理如果Constructor<T> 使用方法 newInstance() 返回的也是一个 T 对象，否则返回Object对象。

###### 使用反射来获取泛型信息

通过某个类对应的Class对象，可以获得该类里包含的所有成员变量，不管该成员变量是使用private修饰，还是使用public修饰。获得了成员变量对应的Field对象后，就可以很容易地获得该成员变量的数据类型：

```java
int age;
List<String> list;
 
Field age = clazz.getField("age");
Field list = clazz.getField("list");
//获取成员变量 f 的类型
Class<?> type = age.getType();
Class<?> type1 = list.getType();
//打印
type:int
type1:interface java.util.List
```

如上，这种方式只对普通类型的成员变量有效。如果该成员变量的类型是有泛型类型的类型，如List<String>类型，则不能准确地得到该成员变量的泛型参数。

为了获得指定成员变量的泛型类型，应先使用如下方法来获取该成员变量的泛型类型。

然后将 Type 对象强制类型转换为 ParameterizedType 对象，**ParameterizedType 表示一个参数化的类型**，如List<String>。ParameterizedType 类提供了如下两个方法。
>Type  getRawType()：返回没有泛型信息的原始类型。
>Type[]  getActualTypeArguments()：返回泛型参数的类型。

```java
public Map<String,Integer> map;

Field map = clazz.getField("map");
Type type = map.getGenericType();
System.out.println(type);
 if(type instanceof ParameterizedType){
            ParameterizedType pType = (ParameterizedType) type;
            System.out.println(pType.getRawType());
            Type[] types = pType.getActualTypeArguments();
            for (Type t : types) {
                System.out.println(t);
            }
        }
//输出
java.util.Map<java.lang.String, java.lang.Integer>
interface java.util.Map
class java.lang.String
class java.lang.Integer
```

