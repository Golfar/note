# 简介

## 静态资源和动态资源

- 静态资源

  无需在程序运行时通过代码运行生成的资源,在程序运行之前就写好的资源. 例如:html css js img ,音频文件和视频文件

- 动态资源

  需要在程序运行时通过代码运行生成的资源,在程序运行之前无法确定的数据,运行时动态生成,例如Servlet,Thymeleaf ... ...

  动态资源指的不是视图上的动画效果或者是简单的人机交互效果

## Servlet

Servlet  (server applet) 是运行在服务端(tomcat)的Java小程序，是sun公司提供一套定义动态资源规范; 从代码层面上来讲Servlet就是一个接口

用来接收、处理客户端请求、响应给浏览器的动态资源。在整个Web应用中，Servlet主要负责接收处理请求、协同调度功能以及响应数据。我们可以把Servlet称为Web应用中的**控制器**

# Servlet开发流程

## 目标

校验注册时,用户名是否被占用. 通过客户端向一个Servlet发送请求,携带username,如果用户名是'atguigu',则向客户端响应 NO,如果是其他,响应YES

## 开发过程

1. tomcat接收到请求后，会将请求报文信息转换成一个HttpServletRequest对象，该对象中包含了请求中的所有信息
2. tomcat同时创建了一个HttpServletResponse对象，该对象用于承装要响应给客户端的信息
3. tomcat根据请求中的资源路径找到对应的servlet，将servlet实例化，调用service方法， 同时将HttpServletRequest和HttpServletResponse对象传入
4. 我们需要做的就是开发servlet接口，该类实现了servlet接口，重写service方法

```java
public class UserNameServlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //从req对象中获取请求的信息
        String username = req.getParameter("username");
        String info = "YES";
        if("golfar".equals(username)){
            info = "NO";
        }
        PrintWriter writer = resp.getWriter();//返回一个向响应体中打印字符的打印流
        writer.write(info);
    }
}
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee https://jakarta.ee/xml/ns/jakartaee/web-app_5_0.xsd"
         version="5.0">

    <servlet>
        <!--给UserServlet起一个别名-->
        <servlet-name>userServlet</servlet-name>
        <servlet-class>com.atguigu.servlet.UserServlet</servlet-class>
    </servlet>


    <servlet-mapping>
        <!--关联别名和映射路径-->
        <servlet-name>userServlet</servlet-name>
        <!--可以为一个Servlet匹配多个不同的映射路径,但是不同的Servlet不能使用相同的url-pattern-->
        <url-pattern>/userServlet</url-pattern>
       <!-- <url-pattern>/userServlet2</url-pattern>-->
        <!--
            /        表示通配所有资源,不包括jsp文件，请求jsp仍然会定位到jsp页面
            /*       表示通配所有资源,包括jsp文件
            /a/*     匹配所有以a前缀的映射路径
            *.action 匹配所有以action为后缀的映射路径
        -->
       <!-- <url-pattern>/*</url-pattern>-->
    </servlet-mapping>

</web-app>
```

+ Servlet并不是文件系统中实际存在的文件或者目录,所以为了能够请求到该资源,我们需要为其配置映射路径
+ servlet的请求映射路径配置在web.xml中
+ servlet-name作为servlet的别名,可以自己随意定义,见名知意就好
+ url-pattern标签用于定义Servlet的请求映射路径
+ 一个servlet可以对应多个不同的url-pattern
+ 多个servlet不能使用相同的url-pattern
+ url-pattern中可以使用一些通配写法
  + /        表示通配所有资源,不包括jsp文件
  + /*      表示通配所有资源,包括jsp文件
  + /a/*     匹配所有以a前缀的映射路径
  + *.action 匹配所有以action为后缀的映射路径

# 注解方式配置servlet

## @WebServlet注解源码

```java
public @interface WebServlet {
    String name() default "";//相当于 servlet-name

    String[] value() default {};//和下面的urlPatterns相同，数组类型，可以定义多个路径。默认为value

    String[] urlPatterns() default {};

    int loadOnStartup() default -1;

    WebInitParam[] initParams() default {};

    boolean asyncSupported() default false;

    String smallIcon() default "";

    String largeIcon() default "";

    String description() default "";

    String displayName() default "";
}
```



## @WebServlet注解使用

使用@WebServlet注解替换Servlet配置

注意使用注解之后就不要在web.xml中配置路径了

```java
@WebServlet("/userServlet")
public class UserNameServlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //从req对象中获取请求的信息
        String username = req.getParameter("username");
        String info = "YES";
        if("golfar".equals(username)){
            info = "NO";
        }
        PrintWriter writer = resp.getWriter();//返回一个向响应体中打印字符的打印流
        writer.write(info);
    }
}
```

# Servlet生命周期

Servlet对象是Servlet容器创建的，生命周期方法都是由容器(目前我们使用的是Tomcat)调用的。这一点和我们之前所编写的代码有很大不同。在今后的学习中我们会看到，越来越多的对象交给容器或框架来创建，越来越多的方法由容器或框架来调用，开发人员要尽可能多的将精力放在业务逻辑的实现上。

| 生命周期 | 对应方法                                                 | 执行时机               | 执行次数 |
| -------- | -------------------------------------------------------- | ---------------------- | -------- |
| 构造对象 | 构造器                                                   | 第一次请求或者容器启动 | 1        |
| 初始化   | init()                                                   | 构造完毕后             | 1        |
| 处理服务 | service(HttpServletRequest req,HttpServletResponse resp) | 每次请求               | 多次     |
| 销毁     | destory()                                                | 容器关闭               | 1        |

```xml
    <servlet>
        <servlet-name>servletLifeCycle</servlet-name>
        <servlet-class>com.atguigu.servlet.ServletLifeCycle</servlet-class>
        <!--load-on-startup
            如果配置的是正整数则表示容器在启动时就要实例化Servlet,
            数字表示的是实例化的顺序
        -->
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>servletLifeCycle</servlet-name>
        <url-pattern>/servletLiftCycle</url-pattern>
    </servlet-mapping>
```

- 通过生命周期测试我们发现Servlet对象在容器中是单例的

  如果要在servlet中定义成员变量，则**尽量不要在service中更改。否则会出现线程安全问题**

- 容器是可以处理并发的用户请求的,每个请求在容器中都会开启一个线程

- 多个线程可能会使用相同的Servlet对象,所以在Servlet中,我们不要轻易定义一些容易经常发生修改的成员变量

- load-on-startup中定义的正整数表示实例化顺序,如果数字重复了,容器会自行解决实例化顺序问题,但是应该避免重复

- Tomcat容器中,已经定义了一些随系统启动实例化的servlet,我们自定义的servlet的load-on-startup尽量不要占用数字1-5

**default-servlet**

当请求资源为静态资源，且路径不能匹配到任何一个servlet时，会将请求交给default-servlet处理，根据路径寻找静态文件，并返回。

# Servlet继承结构

## Servlet接口

```java
//最底层的servlet接口
public interface Servlet {
    
    //初始化方法，构造完毕后，由tomcat自动调用完成初始化功能
    void init(ServletConfig var1) throws ServletException;
	
    //获得ServletConfig对象的方法
    ServletConfig getServletConfig();
	
    //接收用户请求，向用户相应信息
    void service(ServletRequest var1, ServletResponse var2) throws ServletException, IOException;
	
    //返回Servlet字符串形式的描述信息方法
    String getServletInfo();
	
    //销毁方法，在Servlet实例回收前，由tomcat调用的销毁方法，用于资源的释放工作
    void destroy();
}
```

```java
public abstract class GenericServlet implements Servlet, ServletConfig, Serializable {//抽象类
    private static final long serialVersionUID = 1L;
    private transient ServletConfig config;

    public GenericServlet() {
    }

    public void destroy() {
        //将抽象方法重写为普通方法，在方法内部没有任何实现代码
        //成为平庸实现，继承GenericServlet的类不必强制重写该方法
    }

    public String getInitParameter(String name) {
        return this.getServletConfig().getInitParameter(name);
    }

    public Enumeration<String> getInitParameterNames() {
        return this.getServletConfig().getInitParameterNames();
    }

    //返回ServletConfig方法
    public ServletConfig getServletConfig() {
        return this.config;
    }

    public ServletContext getServletContext() {
        return this.getServletConfig().getServletContext();
    }

    public String getServletInfo() {
        return "";
    }
	
    //tomcat在调用init方法时，会读取配置信息并写入一个ServletConfig对象，传入init方法
    public void init(ServletConfig config) throws ServletException {
        this.config = config;//写入成员ServletConfig变量
        this.init();//调用了重载的无参init对象
    }
	
    //重载的初始化方法，用户重写的init方法就是这个方法，这样用户就不需要处理ServletConfig参数
    public void init() throws ServletException {
    }

    public void log(String message) {
        ServletContext var10000 = this.getServletContext();
        String var10001 = this.getServletName();
        var10000.log(var10001 + ": " + message);
    }

    public void log(String message, Throwable t) {
        this.getServletContext().log(this.getServletName() + ": " + message, t);
    }

    //再次抽象生命service方法，由继承该类的子类实现
    public abstract void service(ServletRequest var1, ServletResponse var2) throws ServletException, IOException;

    public String getServletName() {
        return this.config.getServletName();
    }
}
```

```java
public abstract class HttpServlet extends GenericServlet {//也是一个抽象类，主要是service方法的处理
    
    public void service(ServletRequest req, ServletResponse res) throws ServletException, IOException {
        HttpServletRequest request;
        HttpServletResponse response;
        try {//将父类参数转换成Http子类
            request = (HttpServletRequest)req;
            response = (HttpServletResponse)res;
        } catch (ClassCastException var6) {
            throw new ServletException(lStrings.getString("http.non_http"));
        }
		
        //调用重载的方法
        this.service(request, response);
    }
    
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String method = req.getMethod();//获取请求方式
        long lastModified;
        
        //根据请求方式调用对应的请求方法
        if (method.equals("GET")) {
            lastModified = this.getLastModified(req);
            if (lastModified == -1L) {
                this.doGet(req, resp);
            } else {
                long ifModifiedSince;
                try {
                    ifModifiedSince = req.getDateHeader("If-Modified-Since");
                } catch (IllegalArgumentException var9) {
                    ifModifiedSince = -1L;
                }

                if (ifModifiedSince < lastModified / 1000L * 1000L) {
                    this.maybeSetLastModified(resp, lastModified);
                    this.doGet(req, resp);
                } else {
                    resp.setStatus(304);
                }
            }
        } else if (method.equals("HEAD")) {
            lastModified = this.getLastModified(req);
            this.maybeSetLastModified(resp, lastModified);
            this.doHead(req, resp);
        } else if (method.equals("POST")) {
            this.doPost(req, resp);
        } else if (method.equals("PUT")) {
            this.doPut(req, resp);
        } else if (method.equals("DELETE")) {
            this.doDelete(req, resp);
        } else if (method.equals("OPTIONS")) {
            this.doOptions(req, resp);
        } else if (method.equals("TRACE")) {
            this.doTrace(req, resp);
        } else {
            String errMsg = lStrings.getString("http.method_not_implemented");
            Object[] errArgs = new Object[]{method};
            errMsg = MessageFormat.format(errMsg, errArgs);
            resp.sendError(501, errMsg);
        }
        
        protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException 		{
        	String msg = lStrings.getString("http.method_get_not_supported");
        	this.sendMethodNotAllowed(req, resp, msg);
    	}
        
        protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        	String msg = lStrings.getString("http.method_post_not_supported");
        	this.sendMethodNotAllowed(req, resp, msg);
    	}
		
        private void sendMethodNotAllowed(HttpServletRequest req, HttpServletResponse resp, String msg) throws IOException {//响应405，请求方式不允许
        	String protocol = req.getProtocol();
        	if (protocol.length() != 0 && !protocol.endsWith("0.9") && !protocol.endsWith("1.0")) {
            	resp.sendError(405, msg);
        	} else {
            	resp.sendError(400, msg);
        	}

    	}
    }
}

```

因此，如果用户自定义的Servlet不重写service方法，则无论客户端如何请求都会响应405

![1682299663047](./servlet.assets/1682299663047.png)

# ServletConfig和ServletContext

## ServletConfig

为Servlet提供初始配置参数的一种对象,每个Servlet都有自己独立唯一的ServletConfig对象

容器会为每个Servlet实例化一个ServletConfig对象,并通过Servlet生命周期的init方法传入给Servlet作为属性

### 通过xml配置

```xml
<servlet>
        <servlet-name>servletConfig</servlet-name>
        <servlet-class>com.golfar.ServletConfig</servlet-class>
        <!--配置servlet的初始参数，以下键值对都会被tomcat读取并写入到ServletConfig类实例中-->
        <init-param>
            <param-name>keyA</param-name>
            <param-value>valueA</param-value>
        </init-param>
        <init-param>
            <param-name>keyB</param-name>
            <param-value>valueB</param-value>
        </init-param>
    </servlet>
    <servlet-mapping>
        <servlet-name>servletConfig</servlet-name>
        <url-pattern>/servletconf</url-pattern>
    </servlet-mapping>
```

### 通过注解方式配置

```java
@WebServlet(
        urlPatterns = "/serletconf",
        initParams = {@WebInitParam(name="keyA", value = "valueA"), @WebInitParam(name="keyB", value = "valueB")}
)
public class ServletConfig extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        jakarta.servlet.ServletConfig servletConfig = getServletConfig();
        System.out.println(servletConfig.getInitParameter("keyA"));
        System.out.println(servletConfig.getInitParameter("keyB"));

        //获取所有参数名字
        Enumeration<String> initParameterNames = servletConfig.getInitParameterNames();

        //判断有没有下一个参数，如果有返回true
        while(initParameterNames.hasMoreElements()){
            //获取下一个元素并向下移动一次
            System.out.println(servletConfig.getInitParameter(initParameterNames.nextElement()));
        }
    }
}
```

## ServletContext

+ ServletContext对象有称呼为上下文对象,或者叫应用域对象(后面统一讲解域对象)
+ 容器会为每个app创建一个独立的唯一的ServletContext对象
+ ServletContext对象为所有的Servlet所共享
+ ServletContext可以为所有的Servlet提供初始配置参数

![1682303205351](./servlet.assets/1682303205351.png)

ServletContext对象在一个tomcat容器中是单例的

### 配置参数

```xml
<context-param>
        <param-name>encoding</param-name>
        <param-value>UTF-8</param-value>
    </context-param>
    <context-param>
        <param-name>username</param-name>
        <param-value>golfar</param-value>
    </context-param>
```

### 在Servlet中获取ServletContext并获取参数

```java
//获取ServletConfig对象
        //1.直接获取
        ServletContext servletContext = getServletContext();
        //2.通过ServletConfig获取
        servletContext = servletConfig.getServletContext();
        //3.通过请求体获取
        servletContext = req.getServletContext();

        System.out.println(servletContext.getInitParameter("encoding"));
        Enumeration<String> initParameterNames1 = servletContext.getInitParameterNames();
        while(initParameterNames1.hasMoreElements()){
            System.out.println(servletConfig.getInitParameter(initParameterNames1.nextElement()));
        }
```

### 域对象的相关API

域对象: 一些用于存储数据和传递数据的对象,传递数据不同的范围,我们称之为不同的域,不同的域对象代表不同的域,共享数据的范围也不同

ServletContext代表应用,所以ServletContext域也叫作应用域,是webapp中最大的域,可以在本应用内实现数据的共享和传递

webapp中的三大域对象,分别是应用域,会话域,请求域

三大域对象都具有的API如下

| API                                         | 功能解释            |
| ------------------------------------------- | ------------------- |
| void setAttribute(String key,Object value); | 向域中存储/修改数据 |
| Object getAttribute(String key);            | 获得域中的数据      |
| void removeAttribute(String key);           | 移除域中的数据      |

### ServletContext其他重要API

```java
@WebServlet("/context")
public class ServletContext_ extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext servletContext = getServletContext();
        //获得一个指向项目部署位置下的某个文件目录的磁盘真实路径
        String path = servletContext.getRealPath("upload");
        System.out.println(path);
        //C:\workspace4idea\javaweb\out\artifacts\demo03_servletConfigContext_war_exploded\upload

        //获取项目的上下文路径，也就是访问路径
        System.out.println(servletContext.getContextPath());///demo03
    }
}
```

# HttpServletRequest

+ HttpServletRequest是一个接口,其父接口是ServletRequest
+ HttpServletRequest是Tomcat将请求报文转换封装而来的对象,在Tomcat调用service方法时传入
+ HttpServletRequest代表客户端发来的请求,所有请求中的信息都可以通过该对象获得

![image-20240903165046283](./servlet.assets/image-20240903165046283.png)

## 常见API

+ 获取请求行信息相关(方式,请求的url,协议及版本)

| API                           | 功能解释                                           |
| ----------------------------- | -------------------------------------------------- |
| StringBuffer getRequestURL(); | 获取客户端请求的url                                |
| String getRequestURI();       | 获取客户端请求项目中的具体资源（项目内的资源路径） |
| int getServerPort();          | 获取客户端发送请求时的端口                         |
| int getLocalPort();           | 获取本应用所在容器的端口                           |
| int getRemotePort();          | 获取客户端程序的端口                               |
| String getScheme();           | 获取请求协议                                       |
| String getProtocol();         | 获取请求协议及版本号                               |
| String getMethod();           | 获取请求方式                                       |

*url和uri的区别：uri：统一资源标识符，/demo03/context	url：统一资源定位符，http://localhost:8080/demo03/context*

+ 获得请求头信息相关

| API                                   | 功能解释               |
| ------------------------------------- | ---------------------- |
| String getHeader(String headerName);  | 根据头名称获取请求头   |
| Enumeration<String> getHeaderNames(); | 获取所有的请求头名字   |
| String getContentType();              | 获取content-type请求头 |

+ 获得请求参数相关

| API                                                     | 功能解释                             |
| ------------------------------------------------------- | ------------------------------------ |
| String getParameter(String parameterName);              | 根据请求参数名获取请求单个参数值     |
| String[] getParameterValues(String parameterName);      | 根据请求参数名获取请求多个参数值数组 |
| Enumeration<String> getParameterNames();                | 获取所有请求参数名                   |
| Map<String, String[]> getParameterMap();                | 获取所有请求参数的键值对集合         |
| BufferedReader getReader() throws IOException;          | 获取读取请求体的字符输入流           |
| ServletInputStream getInputStream() throws IOException; | 获取读取请求体的字节输入流           |
| int getContentLength();                                 | 获得请求体长度的字节数               |

+ 其他API

| API                                          | 功能解释                    |
| -------------------------------------------- | --------------------------- |
| String getServletPath();                     | 获取请求的Servlet的映射路径 |
| ServletContext getServletContext();          | 获取ServletContext对象      |
| Cookie[] getCookies();                       | 获取请求中的所有cookie      |
| HttpSession getSession();                    | 获取Session对象             |
| void setCharacterEncoding(String encoding) ; | 设置请求体字符集            |

# HttpServletResponse

+ HttpServletResponse是一个接口,其父接口是ServletResponse
+ HttpServletResponse是Tomcat预先创建的,在Tomcat调用service方法时传入
+ HttpServletResponse代表对客户端的响应,该对象会被转换成响应的报文发送给客户端,通过该对象我们可以设置响应信息

## 常见API

+ 设置响应行相关

| API                        | 功能解释       |
| -------------------------- | -------------- |
| void setStatus(int  code); | 设置响应状态码 |


+ 设置响应头相关

| API                                                    | 功能解释                                         |
| ------------------------------------------------------ | ------------------------------------------------ |
| void setHeader(String headerName, String headerValue); | 设置/修改响应头键值对                            |
| void setContentType(String contentType);               | 设置content-type响应头及响应字符集(设置MIME类型) |

+ 设置响应体相关

| API                                                       | 功能解释                                                |
| --------------------------------------------------------- | ------------------------------------------------------- |
| PrintWriter getWriter() throws IOException;               | 获得向响应体放入信息的字符输出流                        |
| ServletOutputStream getOutputStream() throws IOException; | 获得向响应体放入信息的字节输出流                        |
| void setContentLength(int length);                        | 设置响应体的字节长度,其实就是在设置content-length响应头 |

+ 其他API

| API                                                          | 功能解释                                            |
| ------------------------------------------------------------ | --------------------------------------------------- |
| void sendError(int code, String message) throws IOException; | 向客户端响应错误信息的方法,需要指定响应码和响应信息 |
| void addCookie(Cookie cookie);                               | 向响应体中增加cookie                                |
| void setCharacterEncoding(String encoding);                  | 设置响应体字符集                                    |

> MIME类型

+ MIME类型,可以理解为文档类型,用户表示传递的数据是属于什么类型的文档
+ 浏览器可以根据MIME类型决定该用什么样的方式解析接收到的响应体数据
+ 可以这样理解: 前后端交互数据时,告诉对方发给对方的是 html/css/js/图片/声音/视频/... ...
+ tomcat/conf/web.xml中配置了常见文件的拓展名和MIMIE类型的对应关系
+ 常见的MIME类型举例如下

| 文件拓展名                  | MIME类型               |
| --------------------------- | ---------------------- |
| .html                       | text/html              |
| .css                        | text/css               |
| .js                         | application/javascript |
| .png /.jpeg/.jpg/... ...    | image/jpeg             |
| .mp3/.mpe/.mpeg/ ... ...    | audio/mpeg             |
| .mp4                        | video/mp4              |
| .m1v/.m1v/.m2v/.mpe/... ... | video/mpeg             |

p82