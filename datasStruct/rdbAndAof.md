# 持久化

## RDB

### RDB 文件的创建与载入

- 两个命令可以生成 RDB 文件
  - SAVE：阻塞 redis 进程（主线程），直至文件创建完毕。
  - BGSAVE：fork 一个子进程，由子进程去创建文件，不阻塞主进程。
- 服务器载入 RDB 文件会一直阻塞到载入工作完成。

## AOF

### 命令追加

- 客户端发送的写命令被服务端执行后，会以协议格式将被执行的写命令追加到服务器状态的 aof_buf 缓冲区的末尾。

### 命令写入与同步

- 被追加到 aof_buf 缓冲区的内容会调用某个函数判断是否需要写入和保存到 AOF 文件中。

![fsync](https://raw.githubusercontent.com/lyjgulu/redis/main/image/fsync.png)

### AOF 重写

- fork 一个子进程来进行重写。
- 为了同步两个进程间的数据，设置了一个 AOF 重写缓冲区在创建子进程后开始使用，服务端执行完一个写命令会同时将这个写命令发送给 AOF 缓冲区和 AOF 重写缓冲区，当子进程完成创建新 AOF 文件后，将重写缓冲区的所有内容追加到新 AOF 文件的末尾，将新 AOF 替代旧的 AOF。