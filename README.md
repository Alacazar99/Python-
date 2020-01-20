## 面试准备
110道python面试真题：https://zhuanlan.zhihu.com/p/54430650 <br>
后端面试题总汇：https://github.com/yongxinz/back-end-interview <br>
【python_developer】:https://github.com/xiandong79/Python_Developer <br>
【Django面试题】：https://www.cnblogs.com/chongdongxiaoyu/p/9403399.html <br>

### 一、	python中字典的底层是怎么实现的？三个基本操作的平均时间复杂度？
https://blog.csdn.net/junjunba2689/article/details/82814166
### 二、	for...in...循环的本质？
【答案】：for item in Iterable 循环的本质就是先通过iter()函数获取可迭代对象Iterable的迭代器，然后对获取到的迭代器不断调用next()方法来获取下一个值并将其赋值给item，当遇到StopIteration的异常后循环结束。

### 三、	快排、堆排序、冒泡排序、选择排序等七种算法的掌握。
https://www.cnblogs.com/ltchu/p/6610576.html

### 四、	python的垃圾回收机制（三种方法以及循环引用如何解决）？

### 五、	数据结构链表、栈、队列、堆的原理以及大体实现过程？
https://www.cnblogs.com/hedeyong/p/7841548.html
https://www.jianshu.com/p/afbfc784238a
### 六、	http有哪些版本，1.0和1.1有什么区别？
https://blog.csdn.net/elifefly/article/details/3964766

### 七、	进程和线程？多进程与多线程？区别是什么？
##### 	进程：
1、操作系统进行资源分配和调度的基本单位，进程之间相互独立。
2、稳定性好，如果一个进程崩溃，不影响其他进程，但是进程消耗资源大，开启的进程数量有限制
##### 	线程
1、CPU进行资源分配和调度的基本单位，线程是进程的一部分，是比进程更小的能独立运行的基本单位，一个进程下的多个线程可以共享该进程的所有资源
2、如果IO操作密集，则可以多线程运行效率高，缺点是如果一个线程崩溃，都会造成进程的崩溃
##### 	应用
IO密集的用多线程，在用户输入，sleep 时候，可以切换到其他线程执行，减少等待的时间
CPU密集的用多进程，因为假如IO操作少，用多线程的话，因为线程共享一个全局解释器锁，当前运行的线程会霸占GIL，其他线程没有GIL，就不能充分利用多核CPU的优势

### 八、	TCP具体是通过怎样的方式来保证数据的顺序化传输、可靠传输呢？
https://www.nowcoder.com/discuss/297626
### 九、	Get 和Post 的区别？
a)	1. GET使用URL或Cookie传参。而POST将数据放在BODY中。
b)	2. GET的URL会有长度上的限制，则POST的数据则可以非常大。
c)	3. POST比GET安全，因为数据在地址栏上不可见。
d)	get是向服务器发索取数据的一种请求，而Post是向服务器提交数据的一种请求
### 十、	打开了一个浏览器，输入www.baidu.com发生了什么过程？
https://www.nowcoder.com/discuss/297626
### 十一、	三次握手与四次挥手？
### 十二、	关系型数据库与非关系型数据库的区别？
#### 一、关系型数据库
关系型数据库最典型的数据结构是表，由二维表及其之间的联系所组成的一个数据组织
##### 优点：
1、易于维护：都是使用表结构，格式一致；
2、使用方便：SQL语言通用，可用于复杂查询；
3、复杂操作：支持SQL，可用于一个表以及多个表之间非常复杂的查询。
##### 缺点：
1、读写性能比较差，尤其是海量数据的高效率读写；
2、固定的表结构，灵活度稍欠；
3、高并发读写需求，传统关系型数据库来说，硬盘I/O是一个很大的瓶颈。
#### 二、非关系型数据库
非关系型数据库严格上不是一种数据库，应该是一种数据结构化存储方法的集合，可以是文档或者键值对等。
##### 优点：
1、格式灵活：存储数据的格式可以是key,value形式、文档形式、图片形式等等，文档形式、图片形式等等，使用灵活，应用场景广泛，而关系型数据库则只支持基础类型。
2、速度快：nosql可以使用硬盘或者随机存储器作为载体，而关系型数据库只能使用硬盘；
3、高扩展性；
4、成本低：nosql数据库部署简单，基本都是开源软件。
##### 缺点：
1、不提供sql支持，学习和使用成本较高；
2、无事务处理；
3、数据结构相对复杂，复杂查询方面稍欠。
