# 压缩列表

- 压缩列表是列表键（list）和哈希键（hash）的底层实现之一。
  - 列表键：只包含少量列表项，并且列表项要么是小整数值，要么是长度比较短的字符串。
  - 哈希键：只包含少量键值对，且每个键值对的键值对的键和值要么是小整数值，要么是长度比较短的字符串。

![ziplist](https://raw.githubusercontent.com/lyjgulu/redis/main/image/ziplist.png)

