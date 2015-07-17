###javascript绑定事件的3种方法 2015/07/16

>[原文](http://www.itxueyuan.org/view/6338.html)感谢提供答案。

###要想让javascript对用户操作做出响应，首先要对DOM元素绑定事件处理函数。所谓事件处理函数，就是处理用户操作的函数，不同的操作对应不同的名称。

###在javascript中，有3中常用的绑定事件方法：
>1.在dom元素中直接绑定。

>2.在javascript代码中绑定。

>3.绑定事件监听函数。

###一.在dom元素中直接绑定。
>这里的dom元素，可以理解为html标签，javascript支持在标签中直接绑定事件。
```
onXXX="javascript Code"
```
>其中：

>1.onXXX为事件的名称。例如，鼠标单击事件onclick，鼠标双击事件ondouble，鼠标移入事件onmouserover,鼠标移出事件onmouseout等。

>2.javascript Code为处理事件的javascript代码，一般是函数。

>例如,单击一个按钮，弹出警告框的代码有如下两种写法：

>1.原生函数
```
<input onclick="alert('谢谢支持')" tyle="buttom" value="点击我，弹出警告框" />
```
>2.自定义函数

    <input onclick="myAlert()" type="button" value="点击我，弹出警告框"/>
    <script tyle="text/javascript>
        function myAlert(){
            alert("谢谢支持");
        }
    </script>

###二.在javascript代码中绑定。
>在javascript代码中(即`<script>`标签内)绑定事件可以使javascript代码与html标签分离，文档结构清晰，便于管理和分开开发。

>在javascript代码中绑定事件的语法为：
    
    elementObject.onXXX=function(){
        //事件处理代码
    }
    
>其中：

>1.elementObject为DOM对象，即DOM元素。

>2.onXXX为事件名称。

    <input id="demo" type="button" value="点击我，显示type属性"/>
    <script type="text/javascript">
        document.getElementById("dome").onclick=function(){
            alert(this.getAttribute("type"));
        }
    </script>
###三.绑定事件监听函数。
>绑定事件的另一种方法是用addEventListener()或attachEvent()

>####addEventListener()函数语法

>elementObject.addEventListener(eventName,handle,useCapture);

<table>
    <tr>
        <td>参数</td>
        <td>说明</td>
    </tr>
    <tr>
        <td>elementObject</td>
        <td>dom元素对象（即dom元素）。</td>
    </tr>
    <tr>
        <td>eventName</td>
        <td>事件名称。注意，这里的事件名称没有“on”，如鼠标单击事件click，鼠标双击事件doubleclick，鼠标移入事件mouseover，鼠标移出事件mouseout等。</td>
    </tr>
     <tr>
        <td>handle</td>
        <td>事件句柄函数，即用来处理事件的函数</td>
    </tr>
     <tr>
        <td>useCapture</td>
        <td>Boolean类型，是否使用捕获，一般用false。</td>
    </tr>
</table>

>####attachEvent()函数语法

>elementObject.attachEvent(eventName,handle);

<table>
	<tr>
		<td>参数</td>
		<td>说明</td>
	</tr>
	<tr>
		<td>elementObject</td>
		<td>DOM对象（即DOM元素）。</td>
	</tr>
	<tr>
		<td>eventName</td>
		<td>事件名称。注意，与addEventListener()不同，这里的事件名称有“ on ”，如鼠标单击事件 onclick ，鼠标双击事件 ondoubleclick ，鼠标移入事件 onmouseover，鼠标移出事件 onmouseout 等。</td>
	</tr>
	<tr>
		<td>handle</td>
		<td>事件句柄函数，即用来处理事件的函数。</td>
	</tr>
</table>

>####注意：事件句柄函数是指“函数名”，不能带小括号。

>addEventListener()是标准的绑定事件监听函数的方法，是W3C所支持的，Chrome、FierFox、Opera、Safari、IE9.0及其以上版本都支持该函数；但是IE8.0及其以下版本不支持该方法，它使用attchEvent()来绑定事件监听函数。所以，这种绑定事件的方法必须要处理浏览器兼容问题。

>下面绑定事件的代码，进行了兼容性处理，能够被所有浏览器支持。

    function addEvent(obj,type,handle){
        try{
            obj.addEventListener(type,handle,false);
        }catch(e){
            try{
                obj.attEvent('on'+type,handle);
            }catch(e){
                obj['on'+type]=handle;
            }
        }
    }

>例如，一个id="demo"的按钮绑定事件，鼠标单击时弹出警告框：

    addEvent(document.ElementById("demo"),"click",myAlert);
    function myAlert(){
        alert("又是一个警告框");
    }
