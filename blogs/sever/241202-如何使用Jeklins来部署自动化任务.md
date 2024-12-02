# 如何使用Jeklins来部署自动化任务

Jenkins 是一个流行的开源自动化服务器，主要用于实现 **持续集成 (Continuous Integration, CI)** 和 **持续交付 (Continuous Delivery, CD)**。它通过自动化软件开发的构建、测试和部署流程，大幅提高了开发效率和软件质量。

_简单来说就是可以部署自动任务，它可以实现按照需求来执行_

## 那么该如何首次使用了？

下载jeklins

```bash
java -jar jenkins.war --enable-future-java
```

初始密码

/Users/ethan/.jenkins/secrets/initialAdminPassword

3e74ddb8f1254855ae080395d0c6b427

![image-20241202111519555](./assets/241202-如何使用Jeklins来部署自动化任务/image-20241202111519555.png)

![image-20241202111608765](./assets/241202-如何使用Jeklins来部署自动化任务/image-20241202111608765.png)



![image-20241202111903147](./assets/241202-如何使用Jeklins来部署自动化任务/image-20241202111903147.png)



![image-20241202112541146](./assets/241202-如何使用Jeklins来部署自动化任务/image-20241202112541146.png)

![image-20241202112627786](./assets/241202-如何使用Jeklins来部署自动化任务/image-20241202112627786.png)

![image-20241202114402844](./assets/241202-如何使用Jeklins来部署自动化任务/image-20241202114402844.png)

http://<your-jenkins-url>/restart