需求：根据json的对象的某一个key来对json排序。
```
<script type="text/javascript">
	const json=[
		{index:'A01',foodName:'apple',price:'12'},
		{index:'B02',foodName:'banana',price:'3'},
		{index:'A04',foodName:'orange',price:'5'},
		{index:'A03',foodName:'pear',price:'8'},
	];
	//jsonArr：要排序的json
	//indexNum:按对象的第几项排序，默认第0
	function sortJson(jsonArr,indexNum){
		indexNum = indexNum || 0;
		var index = getItem(indexNum);
		console.log(index);
		const arr = [];
		for (let i = 0; i < jsonArr.length; i++) {
			arr.push(jsonArr[i].index);
		}
		//对数组排序
		arr.sort();
		const resultArr =[];
		// 遍历排序后的，找到排序后的每一项所对应的json中得对象,依次添加到新数组中返回。
		for (let j = 0; j < arr.length; j++) {				
			for (let k = 0; k < jsonArr.length; k++) {
				if (arr[j] == jsonArr[k].index) {
					resultArr.push(jsonArr[k])
				}
			}
		}
		return resultArr;
	}
	//根据第几项，来获取对应的键值
	function getItem(index){
		const attr = [];
		for(key in json[0]){
			attr.push(key);
		}
		return attr[index];
	}		
	console.log(sortJson(json));//按照第0个key---index排序json
	console.log(sortJson(json,0));//按照第0个key---index排序json
	console.log(sortJson(json,1));//按照第1个key---foodName排序json
	console.log(sortJson(json,2));//按照第2个key---price排序json
</script>
```
![image.png](https://upload-images.jianshu.io/upload_images/17785871-649e1e798f183cab.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
