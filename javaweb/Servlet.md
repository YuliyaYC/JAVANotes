# Servlet
---
+ ### 什么是Servlet？
  
  <br></br>
  
  >+ __Servlet__ 是 __Java web开发的基石__ ，是与 __平台无关__ 的 __服务器组件__
  >+ 运行在 __Servlet容器/Web应用服务器/Tomcat__
  >+ 负责与 __客户端__ 和 __数据库__ 进行 __通信__

  <br></br>

  ##### Servlet的功能：
    >1. 创建并返回基于客户请求的动态HTML页面
    >2. 与客户端和数据库进行通信

    <br></br>

![](./../images/web/web02.png)

  <br></br>

---
  <br></br>

+ ### 如何使用Servlet？
  + Servlet本身是一组接口（ *描述功能，在javax.servlet包里面* ）
    自定义一个类，并且实现Servlet接口。
    + 接受客户端请求
    + 根据请求做出响应
  
  ##### 【样例】
  
  + 新建一个class叫MyServlet
  
  <br></br>

  ```java
    package com.example.servlet;

    import javax.servlet.*;
    import java.io.IOException;

    public class MyServlet implements Servlet {

        @Override
        public void init(ServletConfig servletConfig) throws ServletException {

        }

        @Override
        public ServletConfig getServletConfig() {
            return null;
        }

        @Override
        public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {

            String id = servletRequest.getParameter("id");
            System.out.println("我是服务端，已经获取到客户端请求,参数是" + id);

            servletResponse.setContentType("text/html;charset=UTF-8");
            servletResponse.getWriter().write("hello client" + id);

        }

        @Override
        public String getServletInfo() {
            return null;
        }

        @Override
        public void destroy() {

        }
    }

  ```
  <br></br>

  + web.xml中添加映射

  <br></br>

  ```xml
    <servlet>
        <servlet-name>MyServlet</servlet-name>
        <servlet-class>com.example.servlet.MyServlet</servlet-class>
    </servlet>

    <servlet-mapping>
        <servlet-name>MyServlet</servlet-name>
        <url-pattern>/myservlet</url-pattern>
    </servlet-mapping>
  ```
  <br></br>

    ##### 【输出结果】

    <br></br>

    ![](./../images/web/web04.png)

    <br></br>

---

