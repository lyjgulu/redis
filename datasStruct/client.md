# 客户端

- 输入缓冲区记录了客户端发送的命令请求，大小不能超过1GB。
- 客户端有固定大小接收缓冲区和可变大小接收缓冲区，固定大小缓冲区最大为 16KB，可变大小缓冲区不超过硬件条件即可。