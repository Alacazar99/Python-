## 面试准备
110道python面试真题：https://zhuanlan.zhihu.com/p/54430650 <br>
后端面试题总汇：https://github.com/yongxinz/back-end-interview <br>
【python_developer】:https://github.com/xiandong79/Python_Developer <br>
【Django面试题】：https://www.cnblogs.com/chongdongxiaoyu/p/9403399.html <br>

## 算法思想
排序（七种）：https://www.cnblogs.com/ltchu/p/6610576.html<br>
**动态规划**：https://www.cnblogs.com/xiaoshen666/p/11014954.html<br>
**双指针**：https://blog.csdn.net/weixin_42552135/article/details/82556234<br>

**贪心算法**：用贪心算法只能通过解局部最优解的策略来达到全局最优解。<br>
https://blog.csdn.net/a925907195/article/details/41314549
https://www.cnblogs.com/gavanwanggw/p/7141358.html

**分治**：<br>https://blog.csdn.net/qq_25740691/article/details/78894177

（1）分解，将要解决的问题划分成若干规模较小的同类问题；<br>
（2）求解，当子问题划分得足够小时，用较简单的方法解决；<br>
（3）合并，按原问题的要求，将子问题的解逐层合并构成原问题的解。<br>

**二分查找**：<br>https://blog.csdn.net/Abysscarry/article/details/87388195<br>
搜索：https://blog.csdn.net/qq_42472682/article/details/97512878<br>
**深度优先搜索<br>
广度优先搜索**

## 基础篇
### 一、	问我对哪个语言比较熟悉，问了我python和C++、JAVA的区别？
https://blog.csdn.net/qq_40518671/article/details/89151738<br>
可变数据类型：列表（list）、字典（dict）、集合（set）；<br>
不可变数据类型： 数值型（int）、字符串型（string）、元组（tuple）
### 二、	Python代码执行原理？
https://www.seoxiehui.cn/article-152715-1.html <br>
我们运行python文件程序的时候，python解释器将源代码转换为字节码，然后再由python解释器来执行这些字节码。
### 三、	解释Python的对象？
https://www.cnblogs.com/harvyxu/p/8535930.html<br>
面向对象是一种基于结构分析的，以数据为中心的程序设计思想。
### 四、	python中字典的底层是怎么实现的？
dict的底层是依靠哈希表(Hash Table)进行实现的，使用开放地址法解决冲突.。
哈希表
哈希表是key-value类型的数据结构，通过关键码值直接进行访问。通过散列函数进行键和数组的下标映射从而决定该键值应该放在哪个位置。

### 五、	谈谈super原理？
https://blog.csdn.net/qq_26442553/article/details/81775449<br>
1、 super().__init__相对于类名.__init__，在单继承上用法基本无差.<br>
2、但在多继承上有区别，super方法能保证每个父类的方法只会执行一次，而使用类名的方法会导致方法被执行多次，具体看前面的输出结果<br>
3、多继承时，使用super方法，对父类的传参数，应该是由于python中super的算法导致的原因，必须把参数全部传递，否则会报错<br>
4、单继承时，使用super方法，则不能全部传递，只能传父类方法所需的参数，否则会报错<br>
5、多继承时，相对于使用类名.__init__方法，要把每个父类全部写一遍, 而使用super方法，只需写一句话便执行了全部父类的方法，这也是为何多继承需要全部传参的一个原因<br>
### 六、	不同的父类中存在 同名的方法，子类对象在调用方法时，会调用哪一个父类中的方法呢？

Python 中的 MRO —— **方法搜索顺序**<br>
•	Python 中针对 类 提供了一个内置属性 __mro__ 可以查看方法搜索顺序。<br>
•	MRO 是 method resolution order，主要用于在多继承时判断 方法、属性 的调用 路径。
### 七、	for...in...循环的本质？
【答案】：for item in Iterable 循环的本质就是先通过iter()函数获取可迭代对象Iterable的迭代器，然后对获取到的迭代器不断调用next()方法来获取下一个值并将其赋值给item，当遇到StopIteration的异常后循环结束。
### 八、	简述面向对象中__new__和__init__区别。
https://zhuanlan.zhihu.com/p/54430650
1.	__new__是一个静态方法,而__init__是一个实例方法.
2.	__new__方法会返回一个创建的实例,而__init__什么都不返回.
3.	只有在__new__返回一个cls的实例时后面的__init__才能被调用.
4.	当创建一个新实例时调用__new__,初始化一个实例时用__init__.
分别使用__metaclass__,__new__和__init__来分别在类创建,实例创建和实例初始化

### 九、	python的垃圾回收机制（三种方法以及循环引用如何解决）？
Python GC 主要使用**引用计数（reference counting）来跟踪和回收垃圾**。
在引用计数的基础上，通过**“标记-清除”**（mark and sweep）解决容器对象可能产生的循环引用问题。
通过**“分代回收”**（generation collection）以空间换时间的方法提高垃圾回收效率。
#### 1 引用计数
PyObject是每个对象必有的内容，其中ob_refcnt就是做为引用计数。当一个对象有新的引用时，它的ob_refcnt就会增加，当引用它的对象被删除，它的ob_refcnt就会减少.引用计数为0时，该对象生命就结束了。
#### 2 标记-清除机制
基本思路是先按需分配，等到没有空闲内存的时候从寄存器和程序栈上的引用出发，遍历以对象为节点、以引用为边构成的图，把所有可以访问到的对象打上标记，然后清扫一遍内存空间，把所有没标记的对象释放。
#### 3 分代技术
分代回收的整体思想是：将系统中的所有内存块根据其存活时间划分为不同的集合，每个集合就成为一个“代”，垃圾收集频率随着“代”的存活时间的增大而减小，存活时间通常利用经过几次垃圾回收来度量。
### 十、	python的生成器和迭代器？
**迭代器**：https://www.cnblogs.com/wangcoo/p/10018363.html
https://www.cnblogs.com/wj-1314/p/8490822.html
**next()函数调用并不断返回下一个值得对象称为迭代器 (Iterator)**
### 十一、	python里装饰器的作用，本质是什么，怎么去构造一个装饰器？
装饰器：装饰器其实就是一个闭包，把一个函数当做参数后返回一个替代版函数，**闭包是装饰器的核心**。<br>
目的是在不改变原函数的情况下，给被修饰函数增加新的功能。<br>
闭包：<br>
在一个外函数中定义了一个内函数，内函数里运用了外函数的临时变量，并且外函数的返回值是内函数的引用。这样就构成了一个闭包。
### 十二、	数据结构链表、栈、队列、堆的原理以及大体实现过程？
https://www.cnblogs.com/hedeyong/p/7841548.html
### 十三、	数组和链表的区别，优缺点？
https://blog.csdn.net/weibo1230123/article/details/82011889
数组的查询时间复杂度O(1) ，修改的时间复杂度O(n)<br>
链表的查询时间复杂度O(n) ，修改的时间复杂度O(1)<br>
### 十四、	python2和python3区别？列举5个
1、Python3 使用 print 必须要以小括号包裹打印内容，比如 print('hi')。Python2 既可以使用带小括号的方式，也可以使用一个空格来分隔打印内容，比 如 print 'hi' <br>
2、python2  range(1,10)返回列表，python3中返回迭代器，节约内存<br>
3、python2中使用ascii编码，python中使用utf-8编码;<br>
4、python2中unicode表示字符串序列，str表示字节序列；python3中str表示字符串序列，byte表示字节序列；<br>
5、python2中为正常显示中文，引入coding声明，python3中不需要;<br>
6、python2中是raw_input()函数，python3中是input()函数;<br>
### 十五、	解释一下python中的GIL是什么？GIL是单线程的，那么python中多线程的实现有什么用。
GIL 是python的全局解释器锁，同一进程中假如有多个线程运行，一个线程在运行python程序的时候会霸占python解释器（加了一把锁即GIL），使该进程内的其他线程无法运行，等该线程运行完后其他线程才能运行。如果线程运行过程中遇到耗时操作，则解释器锁解开，使其他线程运行。所以在多线程中，线程的运行仍是有先后顺序的，并不是同时进行。
### 十六、	分布式锁的实现（Redis实现分布式锁）？、
- 基于数据库实现分布式锁<br>
- 依赖数据库的一张表，一种是通过表中的记录的存在情况确定当前是否有锁存在，另外一种是通过数据库的排他锁来实现分布式锁。<br>
- 基于缓存（Redis，memcached，tair）实现分布式锁<br>
- 基于Zookeeper实现分布式锁<br>
https://www.cnblogs.com/lice-blog/p/11616429.html
### 十七、	python中的map是怎么实现的，知道java中的hashmap底层是怎么实现的吗？
https://blog.csdn.net/suifeng629/article/details/82179996
### 十八、	关于快排、堆排序、冒泡排序、选择排序等七种算法的掌握。
https://www.cnblogs.com/ltchu/p/6610576.html
### 十九、	深拷贝和浅拷贝的区别？
深拷贝：复制了原来的对象，修改深拷贝的值或者改变原对象的值，另一对象的值不改变；<br>
浅拷贝：只是多了一个引用，改变原对象的值，则浅拷贝对象的值改变。
### 二十、	进程和线程？两个的区别？
##### 	进程：
1、操作系统进行资源分配和调度的基本单位，进程之间相互独立。<br>
2、稳定性好，如果一个进程崩溃，不影响其他进程，但是进程消耗资源大，开启的进程数量有限制<br>
##### 	线程
1、CPU进行资源分配和调度的基本单位，线程是进程的一部分，是比进程更小的能独立运行的基本单位，一个进程下的多个线程可以共享该进程的所有资源<br>
2、如果IO操作密集，则可以多线程运行效率高，缺点是如果一个线程崩溃，都会造成进程的崩溃
##### 	应用
IO密集的用多线程，在用户输入，sleep 时候，可以切换到其他线程执行，减少等待的时间<br>
CPU密集的用多进程，因为假如IO操作少，用多线程的话，因为线程共享一个全局解释器锁，当前运行的线程会霸占GIL，其他线程没有GIL，就不能充分利用多核CPU的优势。
### 二十一、	线程间的通信方式
线程间通信的模型有两种：共享内存和消息传递<br>
1、基于 volatile 关键字<br>
来实现线程间相互通信是使用共享内存的思想，大致意思就是多个线程同时监听一个变量，当这个变量发生变化的时候 ，线程能够感知并执行相应的业务。<br>
2、使用Object类的wait() 和 notify() 方法<br>
3、使用JUC工具类 CountDownLatch<br>
4、使用 ReentrantLock 结合 Condition<br>
5、LockSupport实现线程间的阻塞和唤醒<br>
