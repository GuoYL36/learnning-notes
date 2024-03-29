## Java基础



### manage项目下几个文件的意思
	+ controller.groovy：处理前台发送的请求，负责具体模块的业务流程控制，需要调用service逻辑设计层的接口来控制业务流程。
	+ service.java：定义接口(业务逻辑)，给controller层的类提供接口进行调用。一般就是自己写的方法封装起来，声明一下，具体实现在serviceImpl中。
	+ serviceImpl.groovy：对service.java中声明的接口函数进行实现
	+ mapper.java：Mapper接口，方法名与Mapper.xml(UserMapper.xml)中定义的statement的id相同
	+ mapper.xml：写sql语句查询数据库
	+ po.java：持久化对象，由一组属性和属性的get和set方法组成，可以看成与数据库中的表相映射的java对象。

### 目前看明白的这几个文件：主要看controller.groovy，里面可能会调用service.java，service.java里面会调用serviceImpl.groovy，serviceImpl.groovy会调用mapper.java，mapper.java调用mapper.xml。


### @Controller 用于标记在一个类上，使用它标记的类就是一个SpringMVC Controller对象。分发处理器将会扫描使用了该注解的类的方法。通俗来说，被Controller标记的类就是一个控制器，这个类中的方法，就是相应的动作。
### @RequestMapping是一个用来处理请求地址映射的注解，可用于类或方法上。用于类上，表示类中的所有响应请求的方法都是以该地址作为父路径。

### @responseBody一般是作用在方法上的，加上该注解表示该方法的返回结果直接写到Http response Body中，常用在ajax异步请求中，

### @RequestMapping中return返回值默认解析为跳转路径，如果你此时想让Controller返回一个字符串或者对象到前台 就会报404 not response的错误。

### 当加上@ResponseBody注解后不会解析成跳转地址 会解析成相应的json格式的对象 集合字符串或者xml等直接返回给前台 可以通过 ajax 的“success”：fucntion(data){} data直接获取到。

### HttpServletRequest：读取post请求body中的数据

+ request.getSession()可以帮你得到HttpSession类型的对象，通常称之为session对象，session对象的作用域为一次会话，通常浏览器不关闭，保存的值就不会消失，当然也会出现session超时。服务器里面可以设置session的超时时间，web.xml中有一个session time out的地方，tomcat默认为30分钟
+ session.setAttribute("key",value)；是session设置值的方法，原理同java中的HashMap的键值对，意思也就是key现在为“user”；存放的值为userName，userName应该为一个String类型的变量吧？看你自己的定义。
+ 可以使用session.getAttribute("key");来取值，以为着你能得到userName的值。
+ 注意：getAttribute的返回值类型是Object，需要向下转型，转成你的userName类型的，简单说就是存什么，取出来还是什么。
+ setAttribute和getAttribute就是基于HashMap的put方法和get方法实现的，一般叫键值对或者key-value，即通过键找到值。例如你的名字和你的人的关系，只要一叫你的名字，你就会喊到，通过你的名字来找你的人，简单说这就是键值对的概念。


### 关键字transient：让某些被修饰的成员属性变量不被序列化。
+ 以下对象的某些字段不需要被序列化：
	+ 类中的字段值可以根据其它字段推导出来，如一个长方形类有3个属性：长度、宽度、面积，那么在序列化的时候，面积这个属性就不必要被序列化。
	+ 看业务需求，哪些字段不想被序列化。

### 对象序列化
	含义：将对象转换成以字节序列的形式来表示，这些字节序列包含了对象的数据和信息，一个序列化后的对象可以被写到数据库或文件中，也可用于网络传输，一般当我们使用缓存cache（内存空间不够有可能会本地存储到硬盘）或远程调用rpc（网络传输）的时候，经常需要让我们的实体类实现Serializable接口，目的就是为了让其可序列化。
	好处：节省存储空间

### 反序列化：恢复成java对象。

### POJO：普通的java对象，没有继承任何类、实现任何接口、也没有包含特殊的注解
### httpclient请求可能返回一个json格式的数据，也可能发挥POJO对象


### InputStream(FileInputStream)和OutputStream(FileOutputStream)、InputStreamReader和OutputStreamWriter、BufferedReader和BufferedWriter、ByteArrayInputStream和ByteArrayOutputStream关系
    
+ InputStream是字节输入流的所有类的超类，FileInputStream是其子类，BufferedInputStream是FileInputStream的子类，对文件进行数据流的转换(OutputStream、FileOutputStream和BufferedOutputStream类似)
    ```java
    InputStream inputStream = new FileInputStream("fileName")  // 字节流数据
    BufferedInputStream bufferdStream = new BufferedInputStream(inputStream, n)  //带缓冲区的读入
    byte[] buf = new byte[8192];  // 定义内存缓冲区buf,大小8192byte
    int len =0;  // 计算读入缓冲区的字节流
    while((len=inputStream.read(buf)) != -1)
    {
        todo;
    }
    inputStream.close()
    ```

+ InputStreamReader是将字节流转成字符流，OutputStreamWriter是将字符流转换成字节流
    ```java
    InputStream inputStream = new FileInputStream("fileName")  // 字节流数据
    InputStreamReader charStream = new InputStreamReader(inputStream)  // 字符流数据
    
    ```
+ BufferedReader是读取字符流，缓冲各个字符，提供字符、数组和行的高效读取，BufferedWriter是写入字符流，缓冲各个字符，提供字符、数组和行的高效写入。
    ```java
    BufferedReader bufr = new BufferedReader(charStream)  // 创建字符流缓冲区
    
    ```
+ ByteArrayInputStream是字节数组输入流，在内存中创建了一个字节数组，将输入流中读取的数据保存到字节数组的缓冲区。






