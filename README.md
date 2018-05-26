# 总结Python的一些奇技淫巧

### 链式比较操作
```bash
>>> x=8
>>> 1 < x < 10
True
>>> 10 < x < 20
False
>>> x < 10 <x*10 < 100
True
>>> 10 > x <= 9
True
>>> 5 == x > 4
False
```

你可能认为它执行的过程是 `1 < x`, 返回`True`，然后在比较 `True < 10`， 结果返回`True`，因为解释器会把`True`解析成`1`，`False`解析成`0`。但这里的链式比较解析器运行原理则不是这样的，底层会把这些链式比较操作转换成：`1 < x and x < 10` 
### 切片操作中的步长参数
```bash
>>> array=[1,2,3,4,5,6,7,8,9]
>>> array[::2] # 以步长为2遍历整个列表
[1, 3, 5, 7, 9]
```
`x[::-1]`反转列表
```bash
>>> array[::-1] # 反转列表
[9, 8, 7, 6, 5, 4, 3, 2, 1]
```
Python还提供了两个函数：`reverse`,`reversed`。`reverse`是list对象的方法，直接操作list对象，没有返回值；`reversed`是内建函数，可以接收的参数类型包括 `tuple`,`string`,`list`,`unicode`，`不可变原对象`
```bash
>>> array=range(10)
>>> array
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> array.reverse()
>>> array
[9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
>>> array_1=reversed(array)
>>> array_1
<listreverseiterator object at 0x7fe81cfb8cd0>
```
