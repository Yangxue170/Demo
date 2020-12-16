# 前言
  在工作中,主要使用Springboot,感谢前人的伟大,造就了集装箱,让我们可以在即使什么内部都不了解的情况下,依然可以傲娇的编程,写下一行行代码.
逐渐的,你会发现自己什么也不会,只是一个单纯的工具人,每天操作着CRUD的代码,可能一不小心就会被工作抛弃.
在被工作抛弃之前,还是努力的学一下,探求生命本真的样子 😄😄😄 本自己笑醒,但是生活还要继续

# 历史追溯
为什么会出现Springboot呢,最开始是什么样子的,没有如此优秀的注解之前是怎么做到的呢,不可能一开始就如此完美吧!
Java web的历史:https://www.jianshu.com/p/bec6736dcc3d

# 开荒期 - Servlet时代

Servlet (Server Applet),是Java Servlet的简称,是java编写的服务端程序.
简单的说:Servlet就是一个普通的类,只是这个类能够接受和处理请求,并作出响应.

涉及到Servlet必会提及到Servlet容器,可以简单的看作是字段与枪的关系,子弹包装于枪才会有用,否则就是一个摆件.但是他们是互相独立发展的,没有相互牵制.
目前最流行的Servlet容器软件包括: Tomcat、Jetty、Jboss等。(我们项目中主要使用Tomcat,在接下来的篇幅中,所说的Servlet容器倾向于Tomcat)

# Servlet Demo
本文的项目就是最简单的Servlet项目

> 疑问🤔️: 为什么创建的Web项目默认访问index.jsp文件?
  答疑: Tomcat在启动的时候,会读取项目的web.xml文件及Tomcat自带的web.xml文件(位置：apache-tomcat-8.5.43\conf\web.xml),Tomcat的web.xml文件中定义了两个servlet.
  
##  Tomcat web.xml

**DefaultServlet**

```xml
    <servlet>
        <servlet-name>default</servlet-name>
        <servlet-class>org.apache.catalina.servlets.DefaultServlet</servlet-class>
        <init-param>
            <param-name>debug</param-name>
            <param-value>0</param-value>
        </init-param>
        <init-param>
            <param-name>listings</param-name>
            <param-value>false</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
```

**JspServlet**

```xml
<servlet>
        <servlet-name>jsp</servlet-name>
        <servlet-class>org.apache.jasper.servlet.JspServlet</servlet-class>
        <init-param>
            <param-name>fork</param-name>
            <param-value>false</param-value>
        </init-param>
        <init-param>
            <param-name>xpoweredBy</param-name>
            <param-value>false</param-value>
        </init-param>
        <load-on-startup>3</load-on-startup>
    </servlet>
```

Servlet 的映射规则:

```xml
<!-- The mapping for the default servlet -->
    <servlet-mapping>
        <servlet-name>default</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>

    <!-- The mappings for the JSP servlet -->
    <servlet-mapping>
        <servlet-name>jsp</servlet-name>
        <url-pattern>*.jsp</url-pattern>
        <url-pattern>*.jspx</url-pattern>
    </servlet-mapping>
```

对于Tomcat的web.xml中有**welcome-file**标签,默认访问页面,项目中配置该标签时会覆盖掉Tomcat自带的

```xml
    <welcome-file-list>
        <welcome-file>index.html</welcome-file>
        <welcome-file>index.htm</welcome-file>
        <welcome-file>index.jsp</welcome-file>
    </welcome-file-list>
```

或者我们定义一个默认的Servlet,请求URl(/*),表示默认请求处理的Servlet.

