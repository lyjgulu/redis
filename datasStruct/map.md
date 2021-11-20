# 字典

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

