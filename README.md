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

### 一、	python中字典的底层是怎么实现的？三个基本操作的平均时间复杂度？
https://blog.csdn.net/junjunba2689/article/details/82814166
### 二、	for...in...循环的本质？
【答案】：for item in Iterable 循环的本质就是先通过iter()函数获取可迭代对象Iterable的迭代器，然后对获取到的迭代器不断调用next()方法来获取下一个值并将其赋值给item，当遇到StopIteration的异常后循环结束。

--
## 基础篇
### 一、	问我对哪个语言比较熟悉，问了我python和C++、JAVA的区别？
https://blog.csdn.net/qq_40518671/article/details/89151738
可变数据类型：列表（list）、字典（dict）、集合（set）；
不可变数据类型： 数值型（int）、字符串型（string）、元组（tuple）
### 二、	Python代码执行原理？
https://www.seoxiehui.cn/article-152715-1.html 
我们运行python文件程序的时候，python解释器将源代码转换为字节码，然后再由python解释器来执行这些字节码。
### 三、	解释Python的对象？
https://www.cnblogs.com/harvyxu/p/8535930.html
面向对象是一种基于结构分析的，以数据为中心的程序设计思想。
### 四、	python中字典的底层是怎么实现的？
dict的底层是依靠哈希表(Hash Table)进行实现的，使用开放地址法解决冲突.。
哈希表
哈希表是key-value类型的数据结构，通过关键码值直接进行访问。通过散列函数进行键和数组的下标映射从而决定该键值应该放在哪个位置。

### 五、	谈谈super原理？
https://blog.csdn.net/qq_26442553/article/details/81775449
1、 super().__init__相对于类名.__init__，在单继承上用法基本无差
2、但在多继承上有区别，super方法能保证每个父类的方法只会执行一次，而使用类名的方法会导致方法被执行多次，具体看前面的输出结果
3、多继承时，使用super方法，对父类的传参数，应该是由于python中super的算法导致的原因，必须把参数全部传递，否则会报错
4、单继承时，使用super方法，则不能全部传递，只能传父类方法所需的参数，否则会报错
5、多继承时，相对于使用类名.__init__方法，要把每个父类全部写一遍, 而使用super方法，只需写一句话便执行了全部父类的方法，这也是为何多继承需要全部传参的一个原因
### 六、	不同的父类中存在 同名的方法，子类对象在调用方法时，会调用哪一个父类中的方法呢？

Python 中的 MRO —— 方法搜索顺序
•	Python 中针对 类 提供了一个内置属性 __mro__ 可以查看方法搜索顺序。
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
Python GC 主要使用引用计数（reference counting）来跟踪和回收垃圾。
在引用计数的基础上，通过“标记-清除”（mark and sweep）解决容器对象可能产生的循环引用问题。
通过“分代回收”（generation collection）以空间换时间的方法提高垃圾回收效率。
#### 1 引用计数
PyObject是每个对象必有的内容，其中ob_refcnt就是做为引用计数。当一个对象有新的引用时，它的ob_refcnt就会增加，当引用它的对象被删除，它的ob_refcnt就会减少.引用计数为0时，该对象生命就结束了。
#### 2 标记-清除机制
基本思路是先按需分配，等到没有空闲内存的时候从寄存器和程序栈上的引用出发，遍历以对象为节点、以引用为边构成的图，把所有可以访问到的对象打上标记，然后清扫一遍内存空间，把所有没标记的对象释放。
#### 3 分代技术
分代回收的整体思想是：将系统中的所有内存块根据其存活时间划分为不同的集合，每个集合就成为一个“代”，垃圾收集频率随着“代”的存活时间的增大而减小，存活时间通常利用经过几次垃圾回收来度量。
