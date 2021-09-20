# JSP
<br></br>

+ JSP本质上就是一个Servlet，把各种混合文件自动转换成Servlet
  <br></br>

+ JSP主要负责与用户交互，将最终界面呈现给用户
  <br></br>

+ HTML+JS+CSS+Java的混合文件，页面+数据
  <br></br>


---
<br></br>

##### 如果用Servlet中的doGET()去返回页面会非常麻烦
![](./../images/web/web05.png)

<br></br>

---

<br></br>

+ JSP相当于可以把HTML自动生成Servlet, 而且可以加入Java代码。
  <br></br>
+ 当服务器接收到jsp请求的时候，交给JSP引擎处理，每一个jsp页面第一次被访问时，引擎翻译成Servlet文件，再用Web容器调用Servlet完成响应。

<br></br>

##### 单纯从开发角度，JSP就是html中嵌入java。

<br></br>

---

### 3种嵌入方式：

<br></br>

##### 1. JSP脚本
```jsp
<% Java代码 %>
```
注意这里java代码不会被写入servlet呈现

<br></br>

##### 2. JSP声明
```jsp
<%!
    声明方法
%>
```

<br></br>

##### 3. JSP表达式，java对象直接输出到页面
```jsp
<%=Java变量%>
```
<br></br>

##### 【样例1】
```jsp
<% String str = test(); %>

<%!
    public String test() {
        return "hello";
    }
%>

<%=str%>
```
<br></br>

##### 【样例2】
```jsp
<%@ page import="java.util.List" %>
<%@ page import="java.util.ArrayList" %>
<%@ page contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" %>
<!DOCTYPE html>
<html>
<head>
    <title>JSP - Hello World</title>
</head>
<body>
<h1>Index</h1>
<br/>
<%
    List<String> names = new ArrayList<>();
    names.add("A");
    names.add("B");
    names.add("C");

    List<Integer> ages = new ArrayList<>();
    ages.add(22);
    ages.add(21);
    ages.add(23);
%>
<table>
    <tr>
        <th>姓名</th>
        <th>年龄</th>
    </tr>

    <%
        //java部分是无视html，连续的
        for (int i = 0; i < 3; i++) {
    %>

    <tr>
        <td><%=names.get(i)%></td>
        <td><%=ages.get(i)%></td>
    </tr>

    <%
        }
    %>

</table>

</body>
</html>
```

<br></br>

---

### 九个JSP内置对象

<br></br>

>1. __request__:表示一次请求 HttpSevletRequest
>2. __response__：表示一次响应 HttpSevletResponse
>3. __pageContext__：页面上下文，获取页面信息，PageContext
>4. __session__：表示一次会话,保存用户信息，HttpSession
>5. __application__：表示当前web应用，全局对象，保存所有用户共享信息，ServletContext
>6. __config__：表示当前JSP对应的Servlet的ServletConfig对象，获取当前Servlet的信息，ServletConfig
>7. __out__：向浏览器输出数据，JspWriter
>8. __page__：当前JSP对应的Servlet对象，Servlet
>9. __exception__：表示JSP页面发生的异常，Exception

<br></br>

__常用的是request，response，session，application，pageContext__

<br></br>

---

### request常用方法

<br></br>

---

1. #### String getParameter(String key) 根据key获取客户端发来请求的参数
  
<br></br>

URL: localhost:8080/hello?id=9&name=a&age=20

<br></br>

##### java中用request

```java
String idStr = request.getParameter("id");
//强转
Integer id = Integer.parseInt(idStr);
System.out.println(id);
```
<br></br>


##### jsp中用request

```jsp
    <%
        String id = request.getParameter("id");
    %>
    <%=id%>

```
<br></br>

这里可以直接用request对象是因为Servlet的service方法的参数中已经传进来request对象了，
jsp会自动把代码转给servlet的service方法，当然可以用request对象

<br></br>

---

2. #### void setAttribute(String key, Object value) 通过键值对的形式保存数据
  

3. #### Object getAttribute(String key) 通过key取出value
  
<br></br>

![](./../images/web/web06.png)
<br></br>

getParameter是用于客户端发来的请求中的参数
而get/setAttribute是服务器中数值的存放，把数据存入request中，方便jsp文件间的数据读写

<br></br>

##### test1.jsp
```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>test1</title>
</head>
<body>
    <%
        String idStr = request.getParameter("id");
        Integer id = Integer.parseInt(idStr);
        id++;

        //把数据存入到request中
        request.setAttribute("ID", id);

        //把请求转发给test2.jsp
        request.getRequestDispatcher("test2.jsp").forward(request, response);
    %>
</body>
</html>
```
<br></br>


##### test2.jsp
```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>test2</title>
</head>
<body>
    <%
        //拿过来是Object类型，转型
        Integer id = (Integer) request.getAttribute("ID");
    %>
    <%=id%>


</body>
</html>
```

<br></br>

---

4. #### RequestDispatcher getRequestDispatcher (String path)该对象的forward方法用于请求转发

<br></br>

---

5. #### String[] getParameterValues() 获取客户端请求传来的多个重名参数

<br></br>

localhost:8080/test.jsp?name=a&name=b&name=c
```jsp
    <%
        String[] names = request.getParameterValues("name");

    %>
    <%=Arrays.toString(names)%>
```
<br></br>

---

6. #### void setCharacterEncoding(String charset);
```jsp
    <%
        request.setCharacterEncoding("UTF-8");

    %>
```