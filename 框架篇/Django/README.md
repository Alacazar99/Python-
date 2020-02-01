# Django 的认识，面试题
 
 参考自：https://www.cnblogs.com/chongdongxiaoyu/p/9403399.html
## 
 ## 1. 对Django的认识？

```
#1.Django是走大而全的方向，它最出名的是其全自动化的管理后台：只需要使用起ORM，做简单的对象定义，它就能自动生成数据库结构、以及全功能的管理后台。
#2.Django内置的ORM跟框架内的其他模块耦合程度高。
#应用程序必须使用Django内置的ORM，否则就不能享受到框架内提供的种种基于其ORM的便利；
#理论上可以切换掉其ORM模块，但这就相当于要把装修完毕的房子拆除重新装修，倒不如一开始就去毛胚房做全新的装修。
#3.Django的卖点是超高的开发效率，其性能扩展有限；采用Django的项目，在流量达到一定规模后，都需要对其进行重构，才能满足性能的要求。
#4.Django适用的是中小型的网站，或者是作为大型网站快速实现产品雏形的工具。
#5.Django模板的设计哲学是彻底的将代码、样式分离； Django从根本上杜绝在模板中进行编码、处理数据的可能。
```
 

## 2. Django 、Flask、Tornado的对比

```
#1.Django走的是大而全的方向,开发效率高。它的MTV框架,自带的ORM,admin后台管理,自带的sqlite数据库和开发测试用的服务器
#给开发者提高了超高的开发效率
#2.Flask是轻量级的框架,自由,灵活,可扩展性很强,核心基于Werkzeug WSGI工具和jinja2模板引擎
#3.Tornado走的是少而精的方向,性能优越。它最出名的是异步非阻塞的设计方式
#Tornado的两大核心模块：
#    1.iostraem：对非阻塞式的socket进行简单的封装
#    2.ioloop：对I/O多路复用的封装，它实现了一个单例
```
 

## 3. 什么是wsgi,uwsgi,uWSGI？

```
#WSGI:
#    web服务器网关接口,是一套协议。用于接收用户请求并将请求进行初次封装，然后将请求交给web框架
#    实现wsgi协议的模块：
#        1.wsgiref,本质上就是编写一个socket服务端，用于接收用户请求(django)
#        2.werkzeug,本质上就是编写一个socket服务端，用于接收用户请求(flask)
#uwsgi:
#    与WSGI一样是一种通信协议，它是uWSGI服务器的独占协议,用于定义传输信息的类型
#uWSGI:
#    是一个web服务器,实现了WSGI协议,uWSGI协议,http协议,
```
 

## 4. django请求的生命周期？
```
#1.wsgi,请求封装后交给web框架 （Flask、Django）     
#2.中间件，对请求进行校验或在请求对象中添加其他相关数据，例如：csrf、request.session     - 
#3.路由匹配 根据浏览器发送的不同url去匹配不同的视图函数    
#4.视图函数，在视图函数中进行业务逻辑的处理，可能涉及到：orm、templates => 渲染     - 
#5.中间件，对响应的数据进行处理。 
#6.wsgi,将响应的内容发送给浏览器。
 ```

## 5. 简述什么是FBV和CBV？
```
#FBV和CBV本质是一样的
#基于函数的视图叫做FBV，基于类的视图叫做CBV
#在python中使用CBV的优点：
#1.提高了代码的复用性，可以使用面向对象的技术，比如Mixin（多继承）
#2.可以用不同的函数针对不同的HTTP方法处理，而不是通过很多if判断，提高代码可读性
 ```

## 6. 如何给CBV的程序添加装饰器？

```
#引入method_decorator模块
#1.直接在类上加装饰器
#@method_decorator(test,name='dispatch')
#class Loginview(View):
#    pass
#2.直接在处理的函数前加装饰器
#@method_decorator(test)
#    def post(self,request,*args,**kwargs):pass
```
 

## 7. 简述MVC和MTV

```
#MVC软件系统分为三个基本部分：模型(Model)、视图(View)和控制器(Controller)
#Model：负责业务对象与数据库的映射(ORM)
#View：负责与用户的交互
#Control：接受用户的输入调用模型和视图完成用户的请求
#Django框架的MTV设计模式借鉴了MVC框架的思想,三部分为：Model、Template和View
#Model(模型)：负责业务对象与数据库的对象(ORM)
#Template(模版)：负责如何把页面展示给用户
#View(视图)：负责业务逻辑，并在适当的时候调用Model和Template
#此外,Django还有一个urls分发器,
#它将一个个URL的页面请求分发给不同的view处理,view再调用相应的Model和Template
```
 

## 8. django路由系统中name的作用？
```
#用于反向解析路由,相当于给url取个别名，只要这个名字不变,即使对应的url改变
#通过该名字也能找到该条url
 ```

## 9. 列举django的内置组件？
```
#1.Admin是对model中对应的数据表进行增删改查提供的组件
#2.model组件：负责操作数据库
#3.form组件：1.生成HTML代码2.数据有效性校验3校验信息返回并展示
#4.ModelForm组件即用于数据库操作,也可用于用户请求的验证
 ```

## 10. 说一下Django，MIDDLEWARES中间件的作用和应用场景？
```
#中间件是介于request与response处理之间的一道处理过程,用于在全局范围内改变Django的输入和输出。
#简单的来说中间件是帮助我们在视图函数执行之前和执行之后都可以做一些额外的操作
#例如：
#1.Django项目中默认启用了csrf保护,每次请求时通过CSRF中间件检查请求中是否有正确#token值
#2.当用户在页面上发送请求时，通过自定义的认证中间件，判断用户是否已经登陆，未登陆就去登陆。
#3.当有用户请求过来时，判断用户是否在白名单或者在黑名单里
 ```

##  11. 列举django中间件的5个方法？
```
#1.process_request : 请求进来时,权限认证
#2.process_view : 路由匹配之后,能够得到视图函数
#3.process_exception : 异常时执行
#4.process_template_responseprocess : 模板渲染时执行
#5.process_response : 请求有响应时执行
 ```

## 12. django的request对象是在什么时候创建的？
```
#class WSGIHandler(base.BaseHandler):
#    request = self.request_class(environ)
#请求走到WSGIHandler类的时候，执行__cell__方法，将environ封装成了request
 
```
## 13. Django重定向是如何实现的？用的什么状态码？
```
#1.使用HttpResponseRedirect
#from django.http import HttpResponseRedirect  
#2.使用redirect和reverse
#状态码：301和302
#301和302的区别：
#相同点：都表示重定向，浏览器在拿到服务器返回的这个状态码后会自动跳转到一个新的URL地址
#不同点：
#301比较常用的场景是使用域名跳转。比如，我们访问 http://www.baidu.com 会跳转到 https://www.baidu.com
#表示旧地址A的资源已经被永久地移除了
#302用来做临时跳转，比如未登陆的用户访问用户中心重定向到登录页面。表示旧地址A的资源还在（仍然可以访问），这个重定向只是临时地从旧地址A跳转到地址B
```
## 14. xxss攻击
```
#-- XSS攻击是向网页中注入恶意脚本，用在用户浏览网页时，在用户浏览器中执行恶意脚本的攻击。
#    -- XSS分类，反射型xss ，存储型xss
#    -- 反射型xss又称为非持久型xss，攻击者通过电子邮件等方式将包含注入脚本的链接发送给受害者，
#        受害者通过点击链接，执行注入脚本，达到攻击目的。
#    -- 持久型xss跟反射型的最大不同是攻击脚本将被永久的存放在目标服务器的数据库和文件中，多见于论坛
#        攻击脚本连同正常信息一同注入到帖子内容当中，当浏览这个被注入恶意脚本的帖子的时候，恶意脚本会被执行
#    -- 防范措施 1 输入过滤  2 输出编码  3 cookie防盗
#        1，输入过滤 用户输入进行检测 不允许带有js代码
#        2，输出编码 就是把我们的脚本代码变成字符串形式输出出来
#        3，cookie加密
        
        
        
#向页面注入恶意的代码,这些代码被浏览器执行
#XSS攻击能做些什么：
#    1.窃取cookies
#    2.读取用户未公开的资料，如果：邮件列表或者内容、系统的客户资料，联系人列表
#解决方法:
#    1.客户度端：表单提交之前或者url传递之前,对需要的参数进行过滤
#    2.服务器端：检查用户输入的内容是否有非法内容
```

## 15. django中csrf的实现机制
```
- #第一步：django第一次响应来自某个客户端的请求时,后端随机产生一个token值，把这个token保存在SESSION状态中;同时,后端把这个token放到cookie中交给前端页面；
- #第二步：下次前端需要发起请求（比如发帖）的时候把这个token值加入到请求数据或者头信息中,一起传给后端；Cookies:{csrftoken:xxxxx}
- #第三步：后端校验前端请求带过来的token和SESSION里的token是否一致；
 ```

## 16. 基于django使用ajax发送post请求时，都可以使用哪种方法携带csrf token？

```
#1.后端将csrftoken传到前端，发送post请求时携带这个值发送
data: {
             csrfmiddlewaretoken: '{{ csrf_token }}'
        },
#2.获取form中隐藏标签的csrftoken值，加入到请求数据中传给后端
 data: {
         csrfmiddlewaretoken:$('[name="csrfmiddlewaretoken"]').val()
         },
#3.cookie中存在csrftoken,将csrftoken值放到请求头中
headers:{ "X-CSRFtoken":$.cookie("csrftoken")}，
```
 

## 17. Django本身提供了runserver，为什么不能用来部署？(runserver与uWSGI的区别)
```
#1.runserver方法是调试 Django 时经常用到的运行方式，它使用Django自带的
#WSGI Server 运行，主要在测试和开发中使用，并且 runserver 开启的方式也是单进程 。
#2.uWSGI是一个Web服务器，它实现了WSGI协议、uwsgi、http 等协议。注意uwsgi是一种通信协议，而uWSGI是实现uwsgi协议和WSGI协议的 Web 服务器。
#uWSGI具有超快的性能、低内存占用和多app管理等优点，并且搭配着Nginx就是一个生产环境了，能够将用户访问请求与应用 app 隔离开，实现真正的部署 。
#相比来讲，支持的并发量更高，方便管理多进程，发挥多核的优势，提升性能。
```

 

## 18. cookie和session的区别： 

```
#1.cookie:
#    cookie是保存在浏览器端的键值对,可以用来做用户认证
#2.session：
#   将用户的会话信息保存在服务端,key值是随机产生的自符串,value值时session的内容
#    依赖于cookie将每个用户的随机字符串保存到用户浏览器上
#Django中session默认保存在数据库中：django_session表
#flask,session默认将加密的数据写在用户的cookie中
```
 

## 19. 列举django orm 中所有的方法（QuerySet对象的所有方法）

```
#<1> all():                  查询所有结果 
#<2> filter(**kwargs):       它包含了与所给筛选条件相匹配的对象。获取不到返回None
#<3> get(**kwargs):          返回与所给筛选条件相匹配的对象，返回结果有且只有一个。获取不到会抱胸
#如果符合筛选条件的对象超过一个或者没有都会抛出错误。
#<4> exclude(**kwargs):      它包含了与所给筛选条件不匹配的对象
#<5> order_by(*field):       对查询结果排序
#<6> reverse():              对查询结果反向排序 
#<8> count():                返回数据库中匹配查询(QuerySet)的对象数量。 
#<9> first():                返回第一条记录 
#<10> last():                返回最后一条记录 
#<11> exists():              如果QuerySet包含数据，就返回True，否则返回False
#<12> values(*field):        返回一个ValueQuerySet——一个特殊的QuerySet，运行后得到的并不是一系 model的实例化对象，而是一个可迭代的字典序列
#<13> values_list(*field):   它与values()非常相似，它返回的是一个元组序列，values返回的是一个字典序列
#<14> distinct():            从返回结果中剔除重复纪录
```
 

## 20. only和defer的区别？
```
#only:从数据库中只取指定字段的内容
#defer：指定字段的内容不被检索
 ```

## 21. select_related和prefetch_related的区别？
```
#有外键存在时，可以很好的减少数据库请求的次数,提高性能
#select_related通过多表join关联查询,一次性获得所有数据,只执行一次SQL查询
#prefetch_related分别查询每个表,然后根据它们之间的关系进行处理,执行两次查询
 ```

## 22. filter和exclude的区别？
```
#取到的值都是QuerySet对象,filter选择满足条件的,exclude:排除满足条件的.
 
```
## 23. F和Q的作用?
```
#F:对数据本身的不同字段进行操作 如:比较和更新
#Q：用于构造复杂的查询条件 如：& |操作
 
```
## 24. values和values_list的区别？
```
#values : 取字典的queryset
#values_list : 取元组的queryset
 ```

## 25. 如何使用django orm批量创建数据？
```
#bulk_create()
#objs=[models.Book(title="图书{}".format(i+15)) for i in range(100)]
#models.Book.objects.bulk_create(objs)
 ```

## 26. django的Form和ModeForm的作用？
```
#Form作用：

#    1.在前端生成HTML代码
#    2.对数据作有效性校验
#    3.返回校验信息并展示
#ModeForm：根据模型类生成From组件,并且可以操作数据库
 ```

## 27. django的Form组件中,如果字段中包含choices参数，请使用两种方式实现数据源实时更新。
```
#1.重写构造函数
def def __init__(self, *args, **kwargs):
        super().__init__(*args, **kwargs)
        self.fields["city"].widget.choices = models.City.objects.all().values_list("id", "name")
#2.利用ModelChoiceField字段,参数为queryset对象
 

## 28. django的Model中的ForeignKey字段中的on_delete参数有什么作用？

#删除关联表中的数据时,当前表与其关联的field的操作
#django2.0之后，表与表之间关联的时候,必须要写on_delete参数,否则会报异常
 ```

## 29. django如何实现websocket？

列举django orm中三种能写sql语句的方法。
```
#1.使用execute执行自定义的SQL
#2.使用extra方法 
#3.使用raw方法
#    1.执行原始sql并返回模型
#    2.依赖model多用于查询
 ```

## 30. django orm 中如何设置读写分离？

```
#1.手动读写分离:通过.using(db_name)来指定要使用的数据库
#2.自动读写分离:
#    1.定义类：如Router
#    2.配置Router
#        settings.py中指定DATABASE_ROUTERS
#        DATABASE_ROUTERS = ['myrouter.Router',] 
#提高读的性能：多配置几个数据库,并在读取时,随机选取。写的时候写到主库
#实现app之间的数据库分离：分库分表
```

## 31. django中如何实现orm表中添加数据时创建一条日志记录。

## 32. django内置的缓存机制？

```
# 全站缓存
MIDDLEWARE_CLASSES = (
    ‘django.middleware.cache.UpdateCacheMiddleware’, #第一
    'django.middleware.common.CommonMiddleware',
    ‘django.middleware.cache.FetchFromCacheMiddleware’, #最后
)
 
# 视图缓存
from django.views.decorators.cache import cache_page
import time
  
@cache_page(15)          #超时时间为15秒
def index(request):
 t=time.time()      #获取当前时间
 return render(request,"index.html",locals())
 
# 模板缓存
{% load cache %}
 <h3 style="color: green">不缓存:-----{{ t }}</h3>
  
{% cache 2 'name' %} # 存的key
 <h3>缓存:-----:{{ t }}</h3>
{% endcache %}
```

 

 

## 33. django的缓存能使用redis吗？如果可以的话，如何配置？

```
#1.安装 pip install django-redis
#2.在stting中配置CACHES,可以设置多个缓存,根据名字使用
        CACHES = {
            "default": {
                "BACKEND": "django_redis.cache.RedisCache",
                "LOCATION": "redis://127.0.0.1:6379",
                "OPTIONS": {
                    "CLIENT_CLASS": "django_redis.client.DefaultClient",
                    "CONNECTION_POOL_KWARGS": {"max_connections": 100}
                    # "PASSWORD": "密码",
                }
            }
        },
        #另添加缓存
        "JERD": { }
#3.根据名字去连接池中获取连接
        from django_redis import get_redis_connection
        conn = get_redis_connection("default")
```
 

 

## 34. django的模板中filter和simple_tag的区别？
```
# 自定义filter：{{ 参数1|filter函数名:参数2 }}
#    1.可以与if标签来连用
#    2.自定义时需要写两个形参
# simple_tag:{% simple_tag函数名 参数1 参数2 %}
#    1.可以传多个参数,没有限制
#    2.不能与if标签来连用
 ```

## 35. django-debug-toolbar的作用？
```
#1.是django的第三方工具包,给django扩展了调试功能
#包括查看sql语句,db查询次数,request,headers等
 ```

## 36. django中如何实现单元测试？

## 37. 解释orm中 db first 和 code first的含义？
```
#数据持久化的方式：
#db first基于已存在的数据库,生成模型
#code first基于已存在的模型,生成数据库库
 ```

## 38. django中如何根据数据库表生成model中的类？
```
#1.在settings中设置要连接的数据库
#2.生成model模型文件
#python manage.py inspectdb
#3.模型文件导入到models中
#    python manage.py inspectdb > app/models.py
 ```

## 39. 使用orm和原生sql的优缺点？
```
#1.orm的开发速度快,操作简单。使开发更加对象化
#执行速度慢。处理多表联查等复杂操作时,ORM的语法会变得复杂
#2.sql开发速度慢,执行速度快。性能强
 ```

## 40. django的contenttype组件的作用？
```
#这个组件保存了项目中所有app和model的对应关系,每当我们创建了新的model并执行数据库迁移后，ContentType表中就会自动新增一条记录
#当一张表和多个表FK关联,并且多个FK中只能选择其中一个或其中n个时,可以利用contenttypes
 ```

## 41. 谈谈你对restful规范的认识？
```
#首先restful是一种软件架构风格或者说是一种设计风格，并不是标准，它只是提供了一组设计#原则和约束条件，主要用于客户端和服务器交互类的软件。     
#就像设计模式一样，并不是一定要遵循这些原则，而是基于这个风格设计的软件可以更简洁，更#有层次，我们可以根据开发的实际情况，做相应的改变。
#它里面提到了一些规范，例如：
#1.restful 提倡面向资源编程,在url接口中尽量要使用名词，不要使用动词             
#2、在url接口中推荐使用Https协议，让网络接口更加安全
#https://www.bootcss.com/v1/mycss？page=3
#（Https是Http的安全版，即HTTP下加入SSL层，HTTPS的安全基础是SSL，
#因此加密的详细内容就需要SSL（安全套接层协议））                          
#3、在url中可以体现版本号
#https://v1.bootcss.com/mycss
#不同的版本可以有不同的接口，使其更加简洁，清晰             
#4、url中可以体现是否是API接口 
#https://www.bootcss.com/api/mycss            
#5、url中可以添加条件去筛选匹配
#https://www.bootcss.com/v1/mycss？page=3             
#6、可以根据Http不同的method，进行不同的资源操作
#（5种方法：GET / POST / PUT / DELETE / PATCH）             
#7、响应式应该设置状态码
#8、有返回值，而且格式为统一的json格式             
#9、返回错误信息
#返回值携带错误信息             
#10、返回结果中要提供帮助链接，即API最好做到Hypermedia
#如果遇到需要跳转的情况 携带调转接口的URL
    　　ret = {
            code: 1000,
            data:{
            id:1,
            name:'小强',
            depart_id:http://www.luffycity.com/api/v1/depart/8/
            }
    }
```
 

## 42. 接口的幂等性是什么意思？
```
#1.是系统的接口对外一种承诺(而不是实现)
#2.承诺只要调用接口成功,外部多次调用对系统的影响都是一致的,不会对资源重复操作
 ```

## 43. 什么是RPC？
```
#远程过程调用 (RPC) 是一种协议，程序可使用这种协议向网络中的另一台计算机上的程序请求服务
#1.RPC采用客户机/服务器模式。请求程序就是一个客户机，而服务提供程序就是一个服务器。
#2.首先，客户机调用进程发送一个有进程参数的调用信息到服务进程，然后等待应答信息。
#2.在服务器端，进程保持睡眠状态直到调用信息到达为止。当一个调用信息到达，服务器获得进程参数，计算结果，发送答复信息，然后等待下一个调用信息，
#3.最后，客户端调用进程接收答复信息，获得进程结果，然后调用执行继续进行。
 ```

## 44. 为什么要使用API
```
#系统之间为了调用数据。
#数据传输格式:
#    1.json
#     2.xml 
 ```

## 45. 为什么要使用django rest framework框架？
```
#能自动生成符合 RESTful 规范的 API
#1.在开发REST API的视图中，虽然每个视图具体操作的数据不同，
#但增、删、改、查的实现流程基本一样,这部分的代码可以简写
#2.在序列化与反序列化时，虽然操作的数据不同，但是执行的过程却相似,这部分的代码也可以简写
#REST framework可以帮助简化上述两部分的代码编写，大大提高REST API的开发速度
 ```

## 46. django rest framework框架中都有那些组件？

```
#1.序列化组件:serializers  对queryset序列化以及对请求数据格式校验
#2.路由组件routers 进行路由分发
#3.视图组件ModelViewSet  帮助开发者提供了一些类，并在类中提供了多个方法
#4.认证组件 写一个类并注册到认证类(authentication_classes)，在类的的authticate方法中编写认证逻
#5.权限组件 写一个类并注册到权限类(permission_classes)，在类的的has_permission方法中编写认证逻辑。 
#6.频率限制 写一个类并注册到频率类(throttle_classes)，在类的的allow_request/wait 方法中编写认证逻辑
#7.解析器  选择对数据解析的类，在解析器类中注册(parser_classes)
#8.渲染器 定义数据如何渲染到到页面上,在渲染器类中注册(renderer_classes)
#9.分页  对获取到的数据进行分页处理, pagination_class
#10.版本  版本控制用来在不同的客户端使用不同的行为
#在url中设置version参数，用户请求时候传入参数。在request.version中获取版本，根据版本不同 做不同处理 
```
 

## 47. django rest framework框架中的视图都可以继承哪些类？

```
#class View(object):
#class APIView(View): 封装了view,并且重新封装了request,初始化了各种组件
#class GenericAPIView(views.APIView):
#1.增加了一些属性和方法,如get_queryset,get_serializer
#class GenericViewSet(ViewSetMixin, generics.GenericAPIView)
#父类ViewSetMixin 重写了as_view,返回return csrf_exempt(view)
#并重新设置请求方式与执行函数的关系
#class ModelViewSet(mixins.CreateModelMixin,
#                   mixins.RetrieveModelMixin,
#                   mixins.UpdateModelMixin,
#                   mixins.DestroyModelMixin,
#                   mixins.ListModelMixin,
#                   GenericViewSet):pass
#继承了mixins下的一些类,封装了list,create,update等方法
#和GenericViewSet
```
 

## 48. 简述 django rest framework框架的认证流程
```
#1.用户请求走进来后,走APIView,初始化了默认的认证方法
#2.走到APIView的dispatch方法,initial方法调用了request.user
#3.如果我们配置了认证类,走我们自己认证类中的authentication方法
 ```

## 49. django rest framework如何实现的用户访问频率控制
```
#使用IP/用户账号作为键，每次的访问时间戳作为值，构造一个字典形式的数据，存起来，每次访问时对时间戳列表的元素进行判断，
#把超时的删掉，再计算列表剩余的元素数就能做到频率限制了 
#匿名用户：使用IP控制，但是无法完全控制，因为用户可以换代理IP登录用户：使用账号控制，但是如果有很多账号，也无法限制
 ```

## 50. rest_framework序列化组件的作用,以及一些外键关系的钩子方法
```
#作用：帮助我们序列化数据
#1.choices  get_字段名_display
#2.ForeignKey source=orm 操作
#3.ManyToManyFiled  SerializerMethodField()
#                    def get_字段名():
#                    return 自定义
 ```

## 51. 给用户提供一个接口之前需要提前做什么
```
#1.跟前端进行和交互,确定前端要什么
#2.把需求写个文档保存
 ```

## 52. PV和UV
```
#1.pv:页面访问量,没打开一次页面PV计算+1,页面刷新也是
#2.UV：独立访问数,一台电脑终端为一个访客
 ```

## 53. 什么是跨域以及解决方法:

```
#跨域：
# 浏览器从一个域名的网页去请求另一个域名的资源时,浏览器处于安全的考虑,不允许不同源的请求
#同源策略：
#  协议相同
#  域名相同
#  端口相同
#处理方法：
# 1.通过JSONP跨域
# JSON是一种数据交换格式
# JSONP是一种非官方的跨域数据交互协议
# jsonp是包含在函数调用中的json
# script标签不受同源策略的影响，手动创建一个script标签,传递URL,同时传入一个回调函数的名字
# 服务器得到名字后,返回数据时会用这个函数名来包裹住数据,客户端获取到数据之后，立即把script标签删掉
# 2.cors：跨域资源共享
# 使用自定义的HTTP头部允许浏览器和服务器相互通信
# 1.如果是简单请求,直接设置允许访问的域名：
#   允许你的域名来获取我的数据                         
#   response['Access-Control-Allow-Origin'] = "*"
# 2.如果是复杂请求,首先会发送options请求做预检,然后再发送真正的PUT/POST....请求
#   因此如果复杂请求是PUT等请求,则服务端需要设置允许某请求
#   如果复杂请求设置了请求头，则服务端需要设置允许某请求头
#简单请求：
#    一次请求 
#非简单请求：
#    两次请求，在发送数据之前会先发一次请求用于做“预检”，
#    只有“预检”通过后才再发送一次请求用于数据传输。

#只要同时满足以下两大条件，就属于简单请求。                             
# (1) 请求方法是以下三种方法之一：HEAD  GET POST
# (2)HTTP的头信息不超出以下几种字段：                                     
#   Accept                                     
#   Accept-Language                                     
#   Content-Language
#   Last-Event-ID
#  Content-Type：只限于三个值application/x-www-form-urlencoded、multipart/form-data、 text/plain 
#JSONP和CORS：
#   1.JSONP只能实现GET请求，而CORS支持所有类型的HTTP请求
#   2.jsonp需要client和server端的相互配合
#   3.cors在client端无需设置，server端需要针对不同的请求，来做head头的处理
```
 

## 54. 如何实现用户的登陆认证
```
#1.cookie session
#2.token 登陆成功后生成加密字符串
#3.JWT：json wed token缩写 它将用户信息加密到token中,服务器不保存任何用户信息
#服务器通过使用保存的密钥来验证token的正确性
 ```

## 55. 如何将dict转换成url的格式：
```
#使用urlencode
#from urllib.parse import urlencode
#post_data={"k1"："v1","k2":"v2"}
#ret=urlencode(post_data)
#print(ret,type(ret))  #k1=v1&k2=v2 <class 'str'>
```
