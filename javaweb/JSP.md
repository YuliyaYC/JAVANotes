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

