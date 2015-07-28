###js数组去重方法 2015/07/28

###方法一
>思路：

>1.构建一个新的数组存放结果。

>2.for循环中每次从原数组中取出一个元素，用这个元素循环与结果数组对比。

>3.若结果数组中没有该元素，则存到结果数组中。

```
Array.prototype.unique1=function(){
	var res=[this[0]];
	for(var i=1;i<this.length;i++){
		var repeat = false;
		for(var j=0;j<res.length;j++){
			if(this[i]==res[j]){
				repeat=true;
				break;			
			}
		};
		if(!repeat){
			res.push(this[i]);
		}
	}
	return res;
};
var arr=[1,'a','a','b','d','e','e',1,0];
alert(arr.unique1()); 
```

###方法二
>思路：

>1.先将原数组进行排序

>2.检查原数组中的第i个元素与结果数组中的最后一个元素是否相同，因为已经排序，所以重复元素会在相邻位置

>3.如果不同，则将该元素存入结果数组中

```

```