# Servlet
---
+ ### 什么是Servlet？
  
  >+ __Servlet__ 是 __Java web开发的基石__ ，是与 __平台无关__ 的 __服务器组件__
  >+ 运行在 __Servlet容器/Web应用服务器/Tomcat__
  >+ 负责与 __客户端__ 和 __数据库__ 进行 __通信__

  ##### Servlet的功能：
    >1. 创建并返回基于客户请求的动态HTML页面
    >2. 与客户端和数据库进行通信
   
![](./../images/web/web02.png)

---
+ ### 如何使用Servlet？
  + Servlet本身是一组接口（ *描述功能，在javax.servlet包里面* ）
    自定义一个类，并且实现Servlet接口。
    + 接受客户端请求
    + 根据请求做出响应
