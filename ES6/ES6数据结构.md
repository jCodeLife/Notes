ES6中新出现的Set、WeakSet、Map、WeakMap
- **Set**
```
Set 类似于数组，是一种集合的数据结构
 和 Array 之间最大的区别是：
Set中所有的成员都是唯一的。
可以把Set想象成是一个既没有重复元素，也没有顺序概念的数组。

Set 本身是一个构造函数，用来生成 Set 数据结构
const s1 = new Set()
s1.add(1)
s1.add(2)
s1.add(1)
// s1 的值为 {1, 2}
Set 函数可接受一个可循环的数据结构（如数组、类数组、含有 iterable 接口的其他数据结构）作为参数来初始化：
const s2 = new Set([1,2,1,4,3,4])
// s2 的值为 {1, 2, 3, 4}

1 Set属性及操作方法
（1） size
    const s2 = new Set(['a','b','c','d']);
    // s2 的值为 {"a", "b", "c", "d"}
    s2.size // 4
（2） add(value)
    向 Set 中添加一个值，返回 Set 结构本身，所以可以使用链式调用
（3） delete(value)
    删除一个值，返回布尔值表示是否成功删除
（4） has(value)
    Set 中是否包含某个值，返回布尔值
（5） clear()
    清除所有成员，无返回值

2.Set循环
Set结构的实例可以用如下方式循环成员:
keys()：返回键名 
values()：返回键值 
entries()：返回所有键值对成员
Set结构没有键名，只有键值（或者说键名和键值是同一个值），所以key方法和value方法的行为完全一致。
entries方法返回的同时包括键名和键值，所以每次输出一个数组，它的两个成员完全相等。

3.Set应用
（1） 数组去重
let array = [1,2,1,4,5,3,'1'];
[...new Set(array)]     // [1, 2, 4, 5, 3, "1"]
（2） 实现并集、交集、差集
let a = new Set([1, 2, 3]);
let b = new Set([4, 3, 2]);
// 并集
let union = new Set([...a, ...b]);// Set {1, 2, 3, 4}
// 交集
let intersect = new Set([...a].filter(x => b.has(x)));// set {2, 3}
// 差集
let difference = new Set([...a].filter(x => !b.has(x)));// Set {1}

```
- **WeakSet**
```
WeakSet 结构与 Set 类似，也是不重复的值的集合。但是，它与 Set 有两个区别。
1. WeakSet 的成员只能是对象，而不能是其他类型的值。
2.WeakSet 中的对象都是弱引用，即垃圾回收机制不考虑 WeakSet 对该对象的引用，
也就是说，如果其他对象都不再引用该对象，
那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象还存在于 WeakSet 之中。

```
- **Map**
```
类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值都可以当作键。
1.Map属性及操作方法
（1） size
（2） set(key, value)、get(key)
    设置一个键名为 key 键值为 value 的成员，并返回整个 Map 结构，
    如果已经存在该键名，则会更新键值
    读取这个 key 对应的值，如果没有则返回 undefined
（3） has(key) 、 delete(key) 、clear()
    和 Set 的 has、delete、clear 使用方式十分类似

2. Map循环
Map实例的循环方式和Set类似，可以用 keys、values、entries、forEach 等方式循环成员
Map实例的循环方式与Set的不同点在于：Map实例的键名和键值是不同的。

3.Map应用
（1） Map 转为 Array，使用扩展运算符 ...
（2）Array 转为 Map
```
- **WeakMap**
```
WeakMap结构与Map结构类似，也是用于生成键值对的集合。
不同之处在于，WeakMap 不会阻止它的键值被垃圾回收。
那意味着你可以把数据和对象关联起来不用担心内存泄漏。
```
```
Set 与 Map
在使用的过程中明显的Set和Map比我们之前经常使用的Array和Object是有明显的便捷优势的。在后续的开发过程中，我们可以根据场景需要来通过Set和Map来替代Array和Object来使用。
如果对数据结构存储的唯一性有要求，考虑使用Set。
如果数据的复杂程度高，考虑使用Map，在一些构建工具中是非常喜欢使用Map这种数据结构来进行配置，因为map是一种灵活、高效性、适合一对一查找的数据结构。
Set和Map有着类似的API，主要的不同是Set没有set方法，因为它不能存储键值对，剩下的几乎相同。

 WeakMap 与 WeakSet
WeakMap 与 WeakSet 作为一个比较新颖的概念，其主要特点在于弱引用。
相比于 Map 与 Set 的强引用，弱引用可以令对象在 “适当” 情况下正确被垃圾回收，减少内存资源浪费。

```
