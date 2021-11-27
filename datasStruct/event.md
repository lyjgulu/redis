# 事件

1. 文件事件（file event）：Redis 服务器通过套接字与客户端（或者其他Redis服务器）进行连接，而文件事件就是服务器对套接字操作的抽象。服务器与客户端（或者其他服务器）的通信会产生相应的文件事件，而服务器则通过监听并处理这些事件来完成一系列网络通信操作。
2. 时间事件（time event）：Redis 服务器中的一些操作（比如serverCron函数）需要在给定的时间点执行，而时间事件就是服务器对这类定时操作的抽象。

## 文件事件

- 基于 Reactor 模式开发的网络事件处理器，称为文件事件处理器。
  - 使用 I/O 多路复用程序来同时监听多个套接字，并根据套接字目前执行的任务来为套接字关联不同的事件处理器。
  - 当被监听的套接字准备好执行连接应答（accept）、读取（read）、写人（write）、关闭（close）等操作时，与操作相对应的文件事件就会产生，这时文件事件处理器就会调用套接字之前关联好的事件处理器来处理这些事件。

![fileEventHandler](https://raw.githubusercontent.com/lyjgulu/redis/main/image/fileEventhandler.png)

-  I/O 多路复用程序会将所有产生事件的套接字都放到一个队列里面，以有序、同步、每次一个套接字的方式向文件事件分派器传送套接字。

![taojiezi](https://raw.githubusercontent.com/lyjgulu/redis/main/image/socketlist.png)

![scoketprocess](https://raw.githubusercontent.com/lyjgulu/redis/main/image/scoketprocess.png)

## 时间事件

1. 定时事件
2. 周期性事件

### 实现

- 将所有时间事件放在一个无序列表中，遍历整个链表，查找已到达的时间事件，并调用相应的时间处理器。