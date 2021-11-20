# 链表

- 数据结构定义

``` c
typedef struct listNode {
  struct listNode *prev;
  struct listNode *next;
  voie *value;
}
```

## Redis 链表

- 数据结构定义

```c
typedef struct list {
  // 表头节点
  listNode *head;
	// 表尾节点
  listNode *tail;
  // 链表所包含的节点数量
  unsigned long len;
  // 节点值复制函数
  void *(*dup)(void *ptr);
  //  节点值释放函数
	void (*free)(void *ptr);
  // 节点值对比函数
  int (*match)(void *ptr)
}list;
```

![listAndListNode](https://raw.githubusercontent.com/lyjgulu/redis/main/image/listAndListNode.png)

- Redis 链表特性
  1. 双端：链表节点带有`prev`和`next`指针，获取某个节点的前置节点和后置节点的复杂度都是 **O(1)**。
  2. 无环：表头节点的`prev`指针和表尾`next`指针都指向 NULL，对链表的访问已 NULL 为终点。
  3. 带表头指针和表尾指针：通过`list`结构的`head`指针和`tail`指针，程序获取链表的表头节点和表尾节点的复杂度是 **O(1)**。
  4. 带链表长度计数器：程序使用`list`结构的`len`属性来对`list`持有的链表节点进行计数，程序获取链表中节点数量的复杂度为 **O(1)**。
  5. 多态：链表节点使用`void*`指针来保存节点值，并且可以通过`list`结构的`dup`、`free`、`match`三个属性为节点值设置类型特定函数，所以链表可以用于保存各种不同类型的值。
     - `dup`函数用于复制链表节点所保存的值。
     - `free`函数用于释放链表节点所保存的值。
     - `match`函数则用于对比链表节点所保存的值和另一个输入值是否相等。

## 重点

- 链表被用于 Redis 的列表键、发布与订阅、慢查询、监视器等。
- 每个链表节点由一个`listNode`结构来表示，每个节点都有一个指向前置节点和后置节点的指针，链表实际上是双端链表。
- 每个链表使用一个`list`结构来表示，这个结构带有表头节点指针、表尾节点指针，以及链表长度等信息。
- 因为链表表头节点的前置节点和尾巴节点的后置节点都指向 NULL，所以 Redis 的链表实现是无环链表。
- 通过为链表设置不同的类型特定函数，Redis 的链表可以用于保存各种不同类型的值。