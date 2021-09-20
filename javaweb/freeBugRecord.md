# Bug修复记录

---
1. ##### Mac IDEA 中运行web项目Tomcat报错Error13
   
   【解决】
   - terminal中输入
   ```linux
   % chmod -R 777 tomcat文件夹路径
   ```
---

2. ##### Deployment的添加中没有war包选项，项目启动后没有out文件夹，无法自动靠localhost：8080/跳转到index.jps，404报错