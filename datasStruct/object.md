# 对象

## 对象的类型与编码

### 对象的编码

1. long类型的整数
2. embstr 编码的简单动态字符串
3. 简单动态字符串
4. 字典
5. 双端链表
6. 压缩链表
7. 整数集合
8. 跳跃表和字典

### 类型对象

- string：
  - 使用整数值实现的字符串对象
  - 使用 embstr 编码的简单动态字符串
  - 使用简单动态字符串
- list：
  - 压缩链表
  - 双端链表
- hash：
  - 压缩链表
  - 字典
- set：
  - 整数集合实现
  - 字典实现
- zset：
  - 压缩链表
  - 跳跃表加上字典实现

![object]()