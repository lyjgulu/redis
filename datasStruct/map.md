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

![commonMap](https://raw.githubusercontent.com/lyjgulu/redis/main/image/commonMap.png)

## hash 算法

- 主要通过 hash 算法得出 hash 值，将 hash 值和 sizemask 进行 与操作，并且在 ht[0] 和 ht[1] 不能确定（但没有在 rehash 时只会使用其中一个）。

## 解决键冲突

- 使用**链地址法**。

## rehash

- 使用 ht[0] 和 ht[1] 进行来回扩容收缩。

## 渐进式 rehash

- 参考 JDK 源码中 ConcurrentHashMap，不一定完全相同，相似程度比较高。ConcurrentHashMap 需要新建 map，这个不需要......
- rehash 过程中查找方式也类似。

## 重点

1. 字典用于 redis 数据本身数据结构、哈希键。
2. redis 字典中有两个哈希表，一个平时用，另一个仅在进行 rehash 时使用。
3. 使用链地址法解决键冲突。
4. rehash 操作是渐进式。



