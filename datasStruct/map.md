# 字典

## 哈希表

- 数据结构定义

```c
typedef struct dictht {
  
  // 哈希表数组
  dictEntry **table;
  
  // 哈希表大小
  unsigned long size;
  
  // 哈希表大小掩码，用于计算索引值
  // 总是等于 size-1
  unsigned long sizemask;
  
  // 该哈希表已有节点的数量
  unsigned long used;
  
} dictht;
```

## 哈希表节点

- 节点数据结构定义

```c
typedef struct dictEntry {
  // 键
  void *key;
  
  // 值
  union{
    void *val;
    uint64_tu64;
    int64_ts64;
  }v;
  
  // 指向下个哈希表节点，形成链表
  struct dictEntry *next; 
} dictEntry;
```

![map](https://raw.githubusercontent.com/lyjgulu/redis/main/image/map.png)

## 字典

- 数据结构定义

```c
typedef struct dict {
  // 键
  dicType *type;
  
  // 值
  void *privdata;
  
  // 哈希表
  dictht ht[2]; 
  
  // rehash 索引
  // 当 rehash 不在进行时，值为 -1
  in trehashidx; /*rehashing not in progress if rehashidx == -1 */ 
} dict;
```

- 普通状态下（没有进行 rehash）的字典

