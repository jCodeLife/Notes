循环:
1. for
for(let i=0; i<arr.length; i++)
2. while
...

ES5里面新增一些东西
```
1.arr.forEach()  //  代替普通for
arr.forEach(function(val, index, arr){
  console.log(val, index, arr);
});

2.arr.map()  //  非常有用，做数据交互  "映射"
正常情况下，需要配合return，返回是一个新的数组
若是没有return，相当于forEach
注意：平时只要用map，一定是要有return
场景map重新整理数据结构:[{title:'aaa'}]   ->  [{t:'aaaa'}]
let arr = [
   {title:'aaaaa', read:100, hot:true},
   {title:'bbbb', read:100, hot:true},
   {title:'cccc', read:100, hot:true},
   {title:'dddd', read:100, hot:true}
];
let newArr = arr.map((item, index, arr)=>{
   let json={}
   json.t = `^_^${item.title}-----`;
   json.r = item.read+200;
   json.hot = item.hot == true && '真棒!!!';
   return json;
});
console.log(newArr);

3. arr.filter():  过滤，过滤一些不合格“元素”， 如果回调函数返回true，就留下来
4. arr.some(): 类似查找,  数组里面某一个元素符合条件，返回true
5. arr.every(): 数组里面所有的元素都要符合条件，才返回true

注意：其实他们可以接收两个参数:
arr.forEach/map/filter/some/every...(循环回调函数, this指向谁);
------------------------------------------------------------	
5. arr.reduce()   //从左往右
求数组的和、阶乘
let arr = [1,2,3,4,5,6,7,8,9,10];
let res = arr.reduce((prev, cur, index, arr) =>{
  return prev+cur;
});
 console.log(res);
参数prev上一个的结果，cur当前的值，下标index，arr数组。
		
6.arr.reduceRight()  //从右往左
	
======================================================
ES2017新增一个运算符:**
	幂
	Math.pow(2,3)
	2 ** 3
======================================================
7. for....of....：
arr.keys()	数组下标
arr.entries()	数组某一项

for(let val of arr){
  console.log(val);
}
