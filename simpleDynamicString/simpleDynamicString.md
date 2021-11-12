# 简单动态字符串

- `Redis` 没有直接使用 `c语言`的字符串，自己构建一个简单的字符串（simple dynamic string，SDS）的抽象类型。
- 用处：
  1. 保存数据库字符串值
  2. 用作缓冲区：
     - AOF缓冲区（环型缓冲区）
     - 客户端的输入缓冲区

## SDS定义

```c
struct sdshdr {
  // 记录 buf 数组中已使用字节的数量
  // 等于 SDS 所保存字符串的长度
  int len;
  
  // 记录 buf 数组中未使用字节的数量
  int free;
  
  // 字节数组，用于保存字符串
  char buf[];
}；
```

