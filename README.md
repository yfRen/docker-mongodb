# docker-mongodb
什么是MongoDB？
    MongoDB是一个基于分布式文件存储的数据库。由C++语言编写。旨在为WEB应用提供可扩展的高性能数据存储解决方案。
MongoDB是一个介于关系数据库和非关系数据库之间的产品，是非关系数据库当中功能最丰富，最像关系数据库的。他支持的数据结构非常松散，是类似json的bson格式，因此可以存储比较复杂的数据类型。Mongo最大的特点是他支持的查询语言非常强大，其语法有点类似于面向对象的查询语言，几乎可以实现类似关系数据库单表查询的绝大部分功能，而且还支持对数据建立索引。
https://zh.wikipedia.org/wiki/MongoDB
 
MongoDB Version.
mongodb:2.6.12

如何使用此镜像。
运行MongoDB服务器
运行镜像并绑定到27017和28017端口：
docker run -d -p 27017:27017 -p 28017:28017 mongodb:2.6.12

运行容器的第一次，会随机生成一个新的密码，要获得密码，运行检查容器日志命令：
docker logs <CONTAINER_ID>

您将看到以下的输出：
    ======================================================================
    You can now connect to this MongoDB server using:
        mongo admin -u admin -p 5elsT6KtjrqV --host <host> --port <port>
    Please remember to change the above password as soon as possible!
    ======================================================================
在这种情况下，5elsT6KtjrqV是密码组。然后，您可以连接到MongoDB的：
mongo admin -u admin -p 5elsT6KtjrqV
完成！

为管理员账户设置一个特定的密码
如果您想要使用预设的密码，而不是一个随机生成的密码，你可以在运行容器时环境变量设置MONGODB_PASS您的特定密码：
docker run -d -p 27017:27017 -p 28017:28017 -e MONGODB_PASS=mypass mongodb:2.6.12

您现在可以测试你的新的管理员密码：
mongo admin -u admin -p mypass
curl --user admin:mypass --digest http://localhost:28017/

没有密码执行MongoDB
如果你想，没有密码执行MongoDB，你可以在容器运行时设置环境变量AUTH
docker run -d -p 27017:27017 -p 28017:28017 -e AUTH=no mongodb:2.6.12
在默认情况下是”yes”。

设置特定用户：数据库
如果你想使用其他数据库与其他用户
docker run -d -p 27017:27017 -p 28017:28017 -e MONGODB_USER=user -e MONGODB_DATABASE=mydatabase -e MONGODB_PASS=mypass mongodb:2.6.12

您现在可以测试您的新的凭据：
mongo mydatabase -u user -p mypass
 
