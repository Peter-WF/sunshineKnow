###javascript和事件 2015/08/03

>[原文](http://yujiangshui.com/javascript-event/)感谢提供答案。

###javascript和事件
>与浏览器进行交互的时候，浏览器就会触发各种事件。比如当我们打开某一个网页的时候，浏览器加载完成了这个网页，就会触发一个load事件；当我们点击页面中的某一个“地方”,浏览器就会在那个地方触发一个click事件。

>这样，我们就可以编写javascript，通过监听某一个事件，来实现某些功能扩展。例如监听load事件，显示欢迎信息，那么当浏览器加载完一个网页之后，就会显示欢迎信息。

>下面就来介绍一下事件。

###基础事件操作

####监听事件

1.HTML内联属性（避免使用）
>HTML元素里面直接填写事件有关属性，属性值为javascript代码，即可在触发该事件的时候，执行属性值的内容。

>例如：
```
	<button onclick="alert('你点击了这个按钮')">点击这个按钮</button>
```
>onclick属性表示触发click，属性值的内容（javascript代码）会在单击该HTML节点时执行。

>显而易见，使用这种方法，javascript代码必须与HTML代码耦合在一起，不便于维护和开发。所以除非在必须使用的情况(例如统计链接点击数据)下，尽量避免使用这种方法。

2.Dom属性绑定
>也可以直接设置Dom属性来指定某个事件对应的处理函数，这个方法比肩简单：
```
	element.onclick=function(event){
		alert("你点击了这个函数");
	}
```
上面代码就是监听element节点的click事件。它比较简单易懂，而且有较好的兼容性。但是也有缺陷，因为直接赋值给对应属性，如果你在后面的代码中再次element绑定一个回调函数，会覆盖之前的回调函数的内容。 

>虽然也可以用一些方法实现多个绑定，但是还是推荐下面的标准事件监听函数。

3.使用事件监听函数
>标准的事件监听函数如下：
```
element.addEventListener(<event-name>,<callback>,<use-captuer>)
```
表示在element这个对象上面添加一个事件监听器，当监听到有<event-name>事件发生的时候，调用<callback>这个回调函数。至于<use-capture>这个参数，表示该事件监听是在“捕获”阶段中监听（设置为ture）还是在冒泡阶段中监听（设置为false）。关于捕获和冒泡，我们会在下面讲解。

>用标准事件监听函数改写上面的例子：
```
var btn=document.getElementsByTayName('button');
btn[0].addEventListener('click',function(){
	alert('你点击了这个按钮');
},false);
```
这里最好是为HTML结构定义个ID或者Class属性，方便选择，在这里只作为显示使用。

4.移除事件监听
>当我们为某个元素绑定了一个事件，每次触发这个事件的时候，都会执行事件绑定的回调函数。如果我们想解除绑定，需要使用removeEventListenet方法
```
element.removeEventListenet(<event-name>,<callback>,<use-capture>);
```
需要注意的是，绑定事件时的回调函数不能是匿名函数，必须是一个声明的函数，因为解除事件绑定时需要传递这个回调函数的引用，才可以断开绑定。例如：
```
var fun=function(){
	//function logic
}
element.addEventListener('click',fun,false);
element.removeEventListener('click',fun,false);
```

####事件触发过程
>在上面大体了解了事件是什么、如何监听并执行某些操作，但我们对事件触发整个过程还不够了解。

>下面就是事件的触发过程，借用了w3c的图片

<svg xmlns="http://www.w3.org/2000/svg"
     xmlns:xlink="http://www.w3.org/1999/xlink"
     width="100%" height="100%" viewBox="0 0 640 690">

  <title>DOM Level 3 Events: Event Flow</title>
  <desc>Alternate description</desc>
    
  
  <defs id="defs-1">
    <path id="arrowhead" d="M-9,-4 L0,0 -9,4 Z" stroke-linejoin="round" stroke-linecap="round"/>
    <marker id="blackArrow" viewBox="-13 -5 14 10" refX="-4" markerWidth="10" markerHeight="20" orient="auto">
      <use xlink:href="#arrowhead" stroke="black" fill="black"  />
    </marker>
    <marker id="redArrow" viewBox="-13 -5 14 10" refX="-4" markerWidth="10" markerHeight="20" orient="auto">
      <use xlink:href="#arrowhead" stroke="red" fill="red"  />
    </marker>
    <marker id="greenArrow" viewBox="-13 -5 14 10" refX="-4" markerWidth="10" markerHeight="20" orient="auto">
      <use xlink:href="#arrowhead" stroke="green" fill="green"  />
    </marker>

    <filter x="-5%" y="-5%" width="120%" height="120%" id="dropShadow">
      <feGaussianBlur stdDeviation="2 2" in="SourceAlpha"/> 
      <feOffset dx="4" dy="4"/>
      <feComponentTransfer result="shadow">
        <feFuncA type="linear" slope=".55" intercept="0"/>
      </feComponentTransfer>
      <feMerge>
        <feMergeNode/>
        <feMergeNode in="SourceGraphic"/>
      </feMerge>
    </filter>

  </defs>
  

  <g id="nodes" font-family="Verdana, sans-serif" font-size="18" fill="black" text-anchor="middle" stroke="none" stroke-width="2">
    <g id="Window-node" transform="translate(310, 10)">
      <a xlink:href="../DOM3-Events.html#glossary-window" target="_parent">
        <rect x="-70" y="0" width="140" height="40" fill="gainsboro" stroke="black" filter="url(#dropShadow)" />
        <text x="0" y="26">Window</text>
      </a>
    </g>

    <g id="document-node" transform="translate(310, 80)">
      <a xlink:href="../DOM3-Events.html#glossary-document" target="_parent">
        <rect x="-60" y="0" width="120" height="40" fill="gainsboro" stroke="black" filter="url(#dropShadow)" />
        <text x="0" y="26">Document</text>
      </a>
    </g>

    <g id="html-node" transform="translate(310, 150)">
      <rect x="-50" y="0" width="100" height="40" rx="5" ry="5" fill="lightskyblue" stroke="black" filter="url(#dropShadow)" />
      <text x="0" y="26">&lt;html&gt;</text>
    </g>

    <g id="body-node" transform="translate(310, 220)">
      <rect x="-50" y="0" width="100" height="40" rx="5" ry="5" fill="lightskyblue" stroke="black" filter="url(#dropShadow)" />
      <text x="0" y="26">&lt;body&gt;</text>
    </g>

    <g id="table-node" transform="translate(310, 290)">
      <rect x="-50" y="0" width="100" height="40" rx="5" ry="5" fill="lightskyblue" stroke="black" filter="url(#dropShadow)" />
      <text x="0" y="26">&lt;table&gt;</text>
    </g>

    <g id="tbody-node" transform="translate(310, 360)">
      <rect x="-50" y="0" width="100" height="40" rx="5" ry="5" fill="lightskyblue" stroke="black" filter="url(#dropShadow)" />
      <text x="0" y="26">&lt;tbody&gt;</text>
    </g>

    <g id="tr_1-node" transform="translate(140, 450)">
      <rect x="-50" y="0" width="100" height="40" rx="5" ry="5" fill="lightskyblue" stroke="black" filter="url(#dropShadow)" />
      <text x="0" y="26">&lt;tr&gt;</text>
    </g>

    <g id="tr_2-node" transform="translate(500, 450)">
      <rect x="-50" y="0" width="100" height="40" rx="5" ry="5" fill="lightskyblue" stroke="black" filter="url(#dropShadow)" />
      <text x="0" y="26">&lt;tr&gt;</text>
    </g>


    <g id="tr_1_td_1-node" transform="translate(70, 540)">
      <rect x="-50" y="0" width="100" height="40" rx="5" ry="5" fill="lightskyblue" stroke="black" filter="url(#dropShadow)" />
      <text x="0" y="26">&lt;td&gt;</text>
    </g>

    <g id="tr_1_td_1_text-node" transform="translate(70, 610)">
      <ellipse cx="0" cy="35" rx="64" ry="35" fill="steelblue" stroke="black" filter="url(#dropShadow)"/>
      <text x="0" y="40" font-size="15" fill="white" text-anchor="middle">Shady Grove</text>
    </g>


    <g id="tr_1_td_2-node" transform="translate(210, 540)">
      <rect x="-50" y="0" width="100" height="40" rx="5" ry="5" fill="lightskyblue" stroke="black" filter="url(#dropShadow)" />
      <text x="0" y="26">&lt;td&gt;</text>
    </g>

    <g id="tr_1_td_2_text-node" transform="translate(210, 610)">
      <ellipse cx="0" cy="35" rx="64" ry="35" fill="steelblue" stroke="black" filter="url(#dropShadow)"/>
      <text x="0" y="40" font-size="15" fill="white" text-anchor="middle">Aeolian</text>
    </g>


    <g id="tr_2_td_1-node" transform="translate(430, 540)">
      <rect x="-50" y="0" width="100" height="40" rx="5" ry="5" fill="blue" stroke="black" filter="url(#dropShadow)" />
      <text x="0" y="26" fill="white">&lt;td&gt;</text>
    </g>

    <g id="tr_2_td_1_text-node" transform="translate(430, 610)">
      <ellipse cx="0" cy="35" rx="64" ry="35" fill="steelblue" stroke="black" filter="url(#dropShadow)"/>
      <text x="0" y="40" font-size="15" fill="white" text-anchor="middle">
        <tspan x="0" y="34">Over the River,</tspan> <tspan x="0" y="54">Charlie</tspan>
      </text>
    </g>


    <g id="tr_2_td_2-node" transform="translate(570, 540)">
      <rect x="-50" y="0" width="100" height="40" rx="5" ry="5" fill="lightskyblue" stroke="black" filter="url(#dropShadow)" />
      <text x="0" y="26">&lt;td&gt;</text>
    </g>

    <g id="tr_2_td_2_text-node" transform="translate(570, 610)">
      <ellipse cx="0" cy="35" rx="64" ry="35" fill="steelblue" stroke="black" filter="url(#dropShadow)"/>
      <text x="0" y="40" font-size="15" fill="white" text-anchor="middle">Dorian</text>
    </g>
  </g>
  
  <g id="edges">
    <line id="window-document" x1="310" y1="50" x2="310" y2="73" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"/>     
    <line id="document-html" x1="310" y1="120" x2="310" y2="143" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"/>     
    <line id="html-body" x1="310" y1="190" x2="310" y2="213" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"/>     
    <line id="body-table" x1="310" y1="260" x2="310" y2="283" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"/>     
    <line id="table-tbody" x1="310" y1="330" x2="310" y2="353" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"/>
    <path id="tbody-tr_1" fill="none" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"
          d="M310,400 Q310,420 260,420 H160 Q140,420 140,443"/>
    <path id="tbody-tr_2" fill="none" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"
          d="M310,400 Q310,420 380,420 H480 Q500,420 500,443"/>
    <path id="tr_1-tr_2_td_1" fill="none" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"
          d="M140,490 Q140,510 120,510 H90 Q70,510 70,533"/>
    <path id="tr_1-tr_2_td_2" fill="none" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"
          d="M140,490 Q140,510 160,510 H190 Q210,510 210,533"/>
    <path id="tr_2-tr_2_td_1" fill="none" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"
          d="M500,490 Q500,510 480,510 H450 Q430,510 430,533"/>
    <path id="tr_2-tr_2_td_2" fill="none" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"
          d="M500,490 Q500,510 540,510 H550 Q570,510 570,533"/>
    <line id="tr_1_td_1-text" x1="70" y1="580" x2="70" y2="603" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"/>
    <line id="tr_1_td_2-text" x1="210" y1="580" x2="210" y2="603" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"/>
    <line id="tr_2_td_1-text" x1="430" y1="580" x2="430" y2="603" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"/>
    <line id="tr_2_td_2-text" x1="570" y1="580" x2="570" y2="603" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"/>
  </g>
  
  <g id="event-flow" stroke-dasharray="10,5">
    <g id="capture_phase">
      <a xlink:href="../DOM3-Events.html#glossary-capture-phase" target="_parent"><text fill="red" font-family="Verdana, sans-serif" font-size="20" font-weight="bold" text-anchor="middle"><tspan x="150" y="220">Capture</tspan> <tspan x="150" y="240">Phase</tspan> <tspan x="150" y="260">(1)</tspan></text></a>

      <path id="capture_phase_arrow" fill="none" stroke="red" stroke-width="3" marker-end="url(#redArrow)" stroke-linecap="round"
            d="M235,28 C195,25 195,75 238,85 "/>
      <use xlink:href="#capture_phase_arrow" x="5" y="70" />
      <use xlink:href="#capture_phase_arrow" x="10" y="140" />
      <use xlink:href="#capture_phase_arrow" x="10" y="210" />
      <use xlink:href="#capture_phase_arrow" x="10" y="280" />
      <path id="capture_phase_arrow2" fill="none" stroke="red" stroke-width="3" marker-end="url(#redArrow)" stroke-linecap="round"
            d="M245,378 C205,375 205,473 428,458 "/>
      <path id="capture_phase_arrow3" fill="none" stroke="red" stroke-width="3" marker-end="url(#redArrow)" stroke-linecap="round"
            stroke-dasharray="none" d="M428,473 C330,470 330,533 363,548 "/>

    </g>
    
    <g id="target_phase">
      <a xlink:href="../DOM3-Events.html#glossary-target-phase" target="_parent"><text fill="blue" font-family="Verdana, sans-serif" font-size="20" font-weight="bold" text-anchor="middle"><tspan x="337" y="580">Target</tspan> <tspan x="337" y="600">Phase</tspan> <tspan x="337" y="620">(2)</tspan></text></a>
      
      <rect x="-50" y="0" width="100" height="40" rx="5" ry="5" fill="none" stroke="black" stroke-width="5" stroke-dasharray="none" 
            transform="translate(430, 540)"/>
    </g>
    
    <g id="bubble_phase">
      <a xlink:href="../DOM3-Events.html#glossary-bubbling-phase" target="_parent"><text fill="green" font-family="Verdana, sans-serif" font-size="20" font-weight="bold" text-anchor="middle"><tspan x="490" y="320">Bubbling</tspan> <tspan x="490" y="340">Phase</tspan> <tspan x="490" y="360">(3)</tspan></text></a>

      <path id="bubble_phase_arrow3" fill="none" stroke="green" stroke-width="3" marker-end="url(#greenArrow)" stroke-linecap="round"
            stroke-dasharray="none" d="M492,548 C630,483 630,470 562,473"/>
      <path id="bubble_phase_arrow2" fill="none" stroke="green" stroke-width="3" marker-end="url(#greenArrow)" stroke-linecap="round"
            d="M565,457 C605,447 605,398 377,388"/>
      <path id="bubble_phase_arrow" fill="none" stroke="green" stroke-width="3" marker-end="url(#greenArrow)" stroke-linecap="round"
            d="M375,375 C415,372 415,332 375,322"/>
      <use xlink:href="#bubble_phase_arrow" x="0" y="-70" />
      <use xlink:href="#bubble_phase_arrow" x="0" y="-140" />
      <path id="bubble_phase_arrow4" fill="none" stroke="green" stroke-width="3" marker-end="url(#greenArrow)" stroke-linecap="round"
            d="M375,165 C425,162 425,122 385,112"/>
      <path id="bubble_phase_arrow" fill="none" stroke="green" stroke-width="3" marker-end="url(#greenArrow)" stroke-linecap="round"
            d="M385,95 C435,92 435,52 395,42"/>
    </g>
  </g>
  
</svg>

1.事件捕获阶段（Captuer Phase）
>当我们在dom树的某个节点发生了一些操作（例如单击、鼠标移动上去），就会有一个事件发射过去。这个事件从Window发出，不断经过下级节点直到，目标节点。在到达目标节点之前的过程，就是捕获阶段（Capture Phase）

>所有经过的节点，都会触发这个事件。捕获阶段的任务就是建立这个事件传递路线，以便后面冒泡阶段顺着这条路线返回window。

>监听某个在捕获阶段触发的事件，需要在事件监听函数传递第三个参数true
```
element.addEventListener(<event-name>,<callback>,true);
```
但一般使用时我们往往传递false，会在后面说明原因。