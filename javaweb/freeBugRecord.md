# Bug修复记录

 <br></br>

+ ##### <font color=teal>【已解决】</font> Mac IDEA 中无法运行web项目Tomcat报错Error13
   
   
   <br></br>
   >- terminal中输入
   >```linux
   >% chmod -R 777 tomcat文件夹路径
   >```
   <br></br>
---

+ ##### <font color=teal>【已解决】</font>项目启动后没有out文件夹
  
    <br></br>
  >生成的文件夹叫target，和out一样的，可以在project structure->module->path中看

  <br></br>
   
---  
+ ##### <font color=teal>【已解决】</font>无法自动靠localhost：8080跳转到index，404报错
    <br></br>
   Tomcat Run Configuration-Deployment中的Application Context改成/
   <br></br>
---
+ ##### <font color=teal>【已解决】</font>在web.xml中写完servlet和servlet-mapping标签，
   ##### 访问localhost：8080/myservlet，404报错
   ![](./../images/web/web03.png)
<br></br>
Tomcat Run Configuration-Deployment中的Application Context改成/
<br></br>
---

+ ##### <font color=teal>【已解决】</font>用注解同样，访问localhost：8080/myservlet，404报错

<br></br>

Tomcat Run Configuration-Deployment中的Application Context改成/

<br></br>

---

+ ##### <font color=teal>【已解决】</font>LoginServlet中， if (username.equals(myusername) && password.equals(mypassword))报空指针

<br></br>

```java
    //为了跨方法用这两个变量，定义成全局变量,双引号打一下不然空指针

    private String myusername = "";
    private String mypassword = "";
```

<br></br>

---

```xml
<!--在build中配置resources,来防止我们资源导出失败的问题-->
   <build>
       <resources>
           <resource>
               <directory>src/main/resources</directory>
               <includes>
                   <include>**/*.properties</include>
                   <include>**/*.xml</include>
               </includes>
               <filtering>false</filtering>
           </resource>
           <resource>
               <directory>src/main/java</directory>
               <includes>
                   <include>**/*.properties</include>
                   <include>**/*.xml</include>
               </includes>
               <filtering>false</filtering>
           </resource>
       </resources>
   </build>
```

---