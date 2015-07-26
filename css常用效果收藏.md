###css常用效果收藏 2015/07/26
>将常用的css代码，做个记录，如果忘记可以随时查看。

1.让网站全局快速变灰，css的filter功能。
>
```
html{
	filter: grayscale(100%);//IE浏览器
	-webkit-filter: grayscale(100%);//谷歌浏览器
	-moz-filter: grayscale(100%);//火狐
	-ms-filter: grayscale(100%);
	-o-filter: grayscale(100%);
	filter: progid:DXImageTransform.Microsoft.BasicImage(grayscale=1);
	-webkit-filter: grayscale(1);//谷歌浏览器
}
```
Flash动画的颜色不能被CSS滤镜控制，可以在Flash代码的和之间插入
```
<param name="false" value="menu">
<param name="womde" value="opaque">
```

2.让一个div变成一个类似input输入框的效果
>在div添加contentEditable="true"属性
```
<div contentEditable="true"></div>
```

3.禁止用户复制
>设置div禁止选择功能
```
unselectable="on" onselectstart="return false";
```
具体代码：
```
<div unselectable="on" onselectart="return false">
你好世界
</div>
```

4.让字符间距统一
>css代码
```
.text1{
	text-align: justify;
	text-justify: distribute-all-lines;//*ie6-8
	text-align-last: justify;//ie9
	-moz-text-align-last: justify;//ff
	-webkit-text-align-last: justify;//chrome 20+
		@media screen and(-webkit-min-device-pixel-ratio:0){
			.test:after{
				content:".";
				display: inline-block;
				width: 100%;
				overflow: hidden;
				height: 0;
			}
		}//chrome
}
```
>html
```
<div class="box1">
	<div class="test1">姓 名</div>
	<div class="test1">姓 名 姓 名</div>
	<div class="test1">姓 名 姓</div>
	<div class="test1">姓 名 姓 名 姓 名</div>
	<div class="test1">姓 名 姓 名</div>
</div>
```

5.input声音录入按钮（仅支持谷歌）
>
```
<input type="text" placeholder="请输入关键字" x-webkit-speech/>
```

6.给input的placeholder设置颜色
>css
```
::-webkit-input-placeholder{/* WebKit browsers */
	color: #999;
}
:-moz-placeholder{/* Mozilla Firefox 4 to 18 */
	color: #999;
}
::-moz-placeholder{/* Mozilla Firefox 19+ */
	color: #999;
}
:-ms-placeholder{/* Internet Explorer 10+ */
	color: #999;
}
```

7.透明度
>
```
opacity: .9;
filter:alpha(opacity=90);
```

8.超出长度显示省略号
>一般要指定宽度，然后给出如下四个属性
```
display: block;
overflow: hidden;
white-space: nowrap;
text-overflow: ellipsis;
```
实例:
```
.haorooms{
	width: 200px;
	display: block;
	overflow: hidden;
	white-space: nowrap;
	text-overflow: ellipsis;
}
<div class="haorooms">
你好世界你好世界你好世界你好世界你好世界你好世界你好世界你好世界
</div>
```

9.阴影效果
>
```
-webkit-box-shadow: 0 1px 1px rgba(0,0,0,.2);
-moz-box-shadow: 0 1px 1px rgba(0,0,0,.2);
box-shadow: 0 1px 1px rgba(0,0,0,.2);
```