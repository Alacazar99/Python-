## 网络篇
## [-  传输层](https://github.com/Alacazar99/Python-/blob/master/%E7%BD%91%E7%BB%9C%E7%AF%87/%E4%BC%A0%E8%BE%93%E5%B1%82/README.md)
## [-  应用层 ](https://github.com/Alacazar99/Python-/blob/master/%E7%BD%91%E7%BB%9C%E7%AF%87/%E5%BA%94%E7%94%A8%E5%B1%82/README%20.md)
## [-  数据链路层](https://github.com/Alacazar99/Python-/blob/master/%E7%BD%91%E7%BB%9C%E7%AF%87/%E6%95%B0%E6%8D%AE%E9%93%BE%E8%B7%AF%E5%B1%82/README.md)
## [-  物理层](https://github.com/Alacazar99/Python-/blob/master/%E7%BD%91%E7%BB%9C%E7%AF%87/%E7%89%A9%E7%90%86%E5%B1%82/REMADE.md)
## [-  网络层](https://github.com/Alacazar99/Python-/blob/master/%E7%BD%91%E7%BB%9C%E7%AF%87/%E7%BD%91%E7%BB%9C%E5%B1%82/README.md)

#### 一、	TCP具体是通过怎样的方式来保证数据的顺序化传输、可靠传输呢？
##### 	顺序化传输
偏移量（依靠，IP地址中的字节序列）
##### 	可靠传输
超时重传：如果一个已经发送的报文段在超时时间内没有收到确认，那么就重传这个报文段。
#### 二、	HTTPs和HTTP的区别，HTTPS实现的原理过程，SSL加密，非对称加密和对称加密在HTTPS中是怎么用到的。
https://www.cnblogs.com/jesse131/p/9080925.html
#### 三、	http有哪些版本，1.0和1.1有什么区别？
https://blog.csdn.net/elifefly/article/details/3964766
#### 四、	cookie和session了解吗？
这篇写的非常好：https://www.cnblogs.com/wswang/p/6062461.html<br><br>
•	Cookies是服务器在本地机器上存储的小段文本并随每一个请求发送至同一个服务器，是一种在客户端保持状态的方案。
•	Cookie是访问某些网站以后在本地存储的一些与网站相关的信息
#####  创建过程
服务器发送的响应报文包含 Set-Cookie 首部字段，客户端得到响应报文后把 Cookie 内容保存到浏览器中。<br>
客户端之后对同一个服务器发送请求时，会从浏览器中取出 Cookie 信息并通过 Cookie 请求首部字段发送给服务器。<br>
•	会话状态管理（如用户登录状态、购物车、游戏分数或其它需要记录的信息）<br>
•	个性化设置（如用户自定义设置、主题等）<br>
•	浏览器行为跟踪（如跟踪分析用户行为等）<br>
##### Session
Session是存在服务器的一种用来存放用户数据的类HashTable结构。
当浏览器 第一次发送请求时，服务器自动生成了一个HashTable和一个Session ID用来唯一标识这个HashTable，并将其通过响应发送到浏览器。当浏览器第二次发送请求，会将前一次服务器响应中的Session ID放在请求中一并发送到服务器上，服务器从请求中提取出Session ID，并和保存的所有Session ID进行对比，找到这个用户对应的HashTable。
一个在客户端一个在服务端
#### 五、	Socket了解吗？
socket通常也称作"套接字"，用于描述IP地址和端口，是一个通信链的句柄，应用程序通常通过"套接字"向网络发出请求或者应答网络请求。<br>
socket可以实现在不同的计算机之间传输数据，也就是网络传输数据。<br>
https://blog.csdn.net/weixin_39634961/article/details/80236161
http://www.360doc.com/content/11/0609/15/5482098_122692444.shtml
#### 六、	HTTP状态码，都说说有哪些吧？
#### 七、	数据链路层三大特性？
封装成帧，透明传输，差错检验（循环冗余校验(CRC)）。
#### 八、	Get 和Post 的区别？
a)	1. GET使用URL或Cookie传参。而POST将数据放在 请求头 中。<br>
b)	2. GET的URL会有长度上的限制（没有明确规定，但是不同浏览器有不同的限制），则POST的数据则可以非常大。（小数据量:GET  大数据量：POST）<br>
c)	3. POST比GET安全，因为数据在地址栏上不可见。
#### 九、	Python的IO多路复用是怎么实现的？
https://blog.csdn.net/bird73/article/details/79793308
#### 十、	并发与并行？
并发：（多线程就是并发），多个事件轮流交替执行。（吃一口饭，喝一口水）<br>
并行：（多进程是并行），应用能够同时执行不同的任务。（吃饭并打电话）<br>
https://blog.csdn.net/u013945548/article/details/50988456/
#### 十一、	同步与异步？
同步是指：当程序1调用程序2时，程序1停下不动，直到程序2完成回到程序1来，程序1才继续执行下去。  （停下等待）<br>
异步是指：当程序1调用程序2时，程序1径自继续自己的下一个动作，不受程序2的的影响。（不等待）<br>
同步是指：发送方发出数据后，等接收方发回响应以后才发下一个数据包的通讯方式。  <br>
异步是指：发送方发出数据后，不等接收方发回响应，接着发送下个数据包的通讯方式。<br>
#### 十二、	域名解析的过程？

#### 十三、	打开了一个浏览器，输入www.baidu.com发生了些什么过程，中间问到了ARP的过程？
事件顺序：
1.	浏览器获取输入的域名 www.baidu.com
2.	浏览器向DNS请求解析（域名）www.baidu.com的IP地址
3.	域名系统DNS解析出百度服务器的IP地址
4.	浏览器与该服务器建立TCP连接(默认端口号80)
5.	浏览器发出HTTP请求，请求百度首页
6.	服务器通过HTTP响应把首页文件发送给浏览器
7.	TCP连接释放。
8.	浏览器将首页文件进行解析，并将Web页显示给用户。
