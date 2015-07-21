###web-app-变革之rem 2015/07/18

>[原文](http://520ued.com/article/549125815f85b6b44ca20b2b)感谢提供答案。

>rem这是一个低调的css单位，近一两年开始展露头角，许多同学对rem的评价不一，有的在尝试使用，有的在使用过程中遇到坑就弃用了。但是我对rem综合评价是用来做web app它绝对是最合适的人选之一。

###rem是什么？
>rem（font size of the root element）是指相对于根元素的字体大小的单位。简单来说它就是一个相对单位。看到rem大家一定会想起em（font size of the element）是指相对于父元素的字体大小的单位。它们之间其实很相似，只不过计算规则是依赖根元素一个是依赖父元素计算。

###为什么web app要使用rem？
>这里我特别强调web app，web page就不能使用rem吗，其实也当然可以，不过出于兼容性的考虑在web app下使用更加能突显这个单位的价值和能力接下来我们来看看一些企业的web app是怎么做屏幕设配的。

1.实现强大的屏幕设配布局

>iphone6出了两款尺寸的手机，导致移动端的屏幕种类更加的混乱，记得一两年前做web app有一种做法是以320的规格去展示，这种实现方式以淘宝web app为代表作，但是手机淘宝首页进行了改版，采用了rem这个单位，首页以内依旧是和以前一样混乱，有定死宽度的页面，也有那种流式布局的页面。

>我们在做页面布局的使用常用单位是PX，这是一个绝对单位，web app的屏幕适配有很多种做法，例如：流式布局、限死宽度、响应式，但是这些做法都不是最佳的解决方案。

>例如流式布局的解决方案有不少弊端，它虽然可以让各种屏幕都设配，但是显示的效果极其不好，因为只有几个尺寸的手机能够完美的显示极其的不好，因为只有几个尺寸的手机能够完美的显示出视觉效果师和交互最想要的效果，但是目前行业里用流行布局做web app的公司非常多。

>流式布局的技术在页面布局的时候都是通过百分比来定义宽度，但是高度大都是用px来固定住，所以在大屏幕的手机下显示效果会变成有些页面元素宽度被拉长的很长，但是高度还是和原来一样，实际显示非常不协调，这就是流式布局的最致命的缺点，往往只有几个尺寸的手机下看到的效果是令人满意的，其实很多视觉设计师应该无法接受这种效果，因为他们的设计图在大屏幕手机下看到的效果相当于是被横向拉长来一样。

2. 固定宽度做法

>还有一种是固定页面宽度的做法，早期有些网站把页面设置成320的宽度，超出部分留白，这样做视觉，前端都挺开心，视觉在也不用被流布局限制自己的设计灵感了，前端也不用在搞啃爹的流式布局。但是这种解决方案也是存在一些问题，例如在大屏幕手机下两边是留白的，还有一个就是大屏幕下看起来页面会特别小。

3.响应式做法

>响应式这种方式在国内很少有大型企业的复杂性的网站在移动端用这种方法去做，主要原因是工作大，维护性难，所以一般都是中小型的门户或者博客类站点会采用响应式的方法从web page到web app直接一步到位，因为这样反而可以节约成本，不用专门为自己的网站做一个web app的版本。

4.设置viewprot进行缩放

```
<meta name="viewport" content="width=320,maximum-scale=1.3.user-scalable=no">
```

>天猫的web app的首页就是采用这种方式去做的，以320宽度为基准，进行缩放，最大缩放为320*1.3=416，基本缩放到426都可以兼容iphone6 plus的屏幕了，这个方法简单粗暴，又高效、说实话我觉得他和用接下去我们要讲的rem都非常高效，不过有部分同学使用过程中反应缩放过程有些糊，具体我使用没有怎么遇到过这种情况。

5.rem能等比例适配所有屏幕
>上面讲了一大堆目前大部分公司主流的一些web app的适配解决方案，接下来讲rem是如何工作的。

>上面讲过rem是通过根元素进行适配的，网页中的根元素指的是html我们通过设置html的字体大小就可以控制rem的大小。举个例子。

```
html{
	font-size:20px;
}
.btn{
	width:6rem;
	height:3rem;
	line-height:3rem;
	font-size:1.2rem;
	display:inline-block;
	background:#06c;
	color:#fff;
	border-radius:.5rem;
	text-decoration:none;
	text-align:center;
}
```

>我把html设置成10px是为了方便我们计算，为什么6rem等于60px。如果这个时候我们的.btn的样式不变，我们再改变html的font-size的值，看看按钮发生下面的变化。

```
html{
	font-size:40px;
}
```

>上面的width，height变成了上面结果的两倍，我们只改变了html的font-size，但.btn样式的width，height的rem设置的属性不变的情况下就改变了按钮在web中的大小。

>其实从上面的两个案例中我们就可以计算出1px等于多少rem：

>第一个例子：

>120px=6rem*20px(根元素设置大值)

>第二个例子：

>240px=6rem*40px(根元素设置大值)

>推算出：

>10px=1rem在根元素（font-size=10px的时候）；

>20px=1rem在根元素（font-size=20px的时候）；

>40px=1rem在根元素（font-size=40的时候）；

>在上面两个例子中我们发现第一个案例按钮是等比例方法到第二个按钮，html font-size的改变就会导致按钮的大小发生改变，我们并不需要改变先前给按钮设置的高度宽度，其实这就是我们最想看到的。

###到这里肯定很多人会问我是怎么计算出不同分辨率下fnot-size的值。

>首先假设我上面设计稿给我的时候是按照640的标准尺寸给我的前提下,（当然这个尺寸肯定不一定是640，可以是320，或者480，又或是375）来看一组表格

<table>
	<tr>
		<td>宽度</td>
		<td>320</td>
		<td>384</td>
		<td>480</td>
		<td>640</td>
	</tr>
	<tr>
		<td>屏幕对比比例</td>
		<td>0.5</td>
		<td>0.6</td>
		<td>0.75</td>
		<td>1</td>
	</tr>
	<tr>
		<td>Html font-size</td>
		<td>10px</td>
		<td>12px</td>
		<td>15px</td>
		<td>20px</td>
	</tr>
	<tr>
		<td>元素宽度（px）</td>
		<td>100px</td>
		<td>120px</td>
		<td>150px</td>
		<td>200px</td>
	</tr>
	<tr>
		<td>元素宽度（rem）</td>
		<td>10rem</td>
		<td>10rem</td>
		<td>10rem</td>
		<td>10rem</td>
	</tr>
</table>

>页面是以640的宽度去切，怎么计算不同宽度下font-size的值，大家看表格上面的数值变化应该能明白。举个例子：384/640=0.6，384是640的0.6倍，所以384页面宽度下面的font-size也等于它的0.6倍，这时384的font-size就等于12px。在不同设备的宽度计算方式以此类推。

>这样的好处是所有的设备分辨率都能兼容适配，淘宝首页目前就是用的js计算。但其实不用js我们也可以做适配，一般我们在做web app都会先统计自己网站有哪些主流的屏幕设备，然后针对那些设备去做media query设置也可以实现适配，例如下面这样：

```
html{
	font-size:20px;
}
@media only screen and(min-width:401px){
	html{
		font-size:25px!impotrant;
	}
}
@media only screen and(min-width:428px){
	html{
		font-size:26.75px!important;
	}
}
@media only screen and(min-width:481px){
	html{
		font-size:30px!important;
	}
}
@media only screen and(min-width:569px){
	html{
		font-size:35px!important;
	}
}
@media only screen and(min-width:641px){
	html{
	font-size:40px!important;
	}
}

```
>上面的做的设置当然是不能所有设备全适配，但是用JS是可以实现全适配。具体用哪个就要根据自己的实际工作场景去定了。

>下面推荐两个国内用了rem技术的移动站，大家可以上去参考看看他们的做法，手机淘宝目前只有首页用了rem，native app的首页是内嵌的web app首页。

[淘宝首页](http://m.taobao.com)