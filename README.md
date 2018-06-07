# 总结Python的一些奇技淫巧

_每天持续更新_

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
### for ... else 语法
```python
for item in [0, 1, 2, 3, 4, 5]:
    if item == 6:
        break
else:
    print('item was never 6')
```
如果`for`正常结束，就会执行`else`代码块，如果遇到了`break`则不会再执行`else`代码块，等价于以下代码：
```python
hit = False
for item in [0, 1, 2, 3, 4, 5]:
    if item == 6:
        hit = True
        break
if not hit:
    print('item was never 6')
```
当然还有更简单的写法：
```python
if 6 not in [0, 1, 2, 3, 4, 5]:
    print('item was never 6')
```
### __missing__方法
在dict的子类中实现 `__missing__(self, key)`方法，如果key不在dict中，则会调用`__missing__(self, key)`方法
```python
class CustomDict(dict):
    def __missing__(self, key):
        self[key] = value = []
        return value


m_d = CustomDict()
m_d['a'].append(1)
m_d['a'].append(1)
```

Python2.5 以后增加了`defaultdict`，可完成同上代码相似的功能。
要注意的是，这种形式的默认值(包括`defaultdict`)只有在通过`dict[key]`或者`dict.__getitem__(key)`访问的时候才有效

### 变量值交换
```bash
>>> a=10
>>> b=20
>>> a,b
(10, 20)
>>> a,b = b,a
>>> a,b
(20, 10)
```
多值赋值其实就是元组打包和序列解包的组合的过程


