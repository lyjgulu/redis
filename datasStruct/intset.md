# 整数集合

- 整数集合是 Redis 用于保存整数值的集合，保证集合中不会出现重复元素。

## 升级

- 将新元素添加到整数集合中，且新元素的类型比整数集合现有所有元素的类型都要长，需要进行升级步骤：
  1. 根据新元素的类型，扩展整数集合底层数组的空间大小，并分配空间。
  2. 转换与新元素相同的类型。

## 升级的好处

1. 提升整数集合的灵活性。
2. 尽可能地节约内存。

## 降级

- 不支持降级操作。