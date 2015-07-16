###如何优雅的用js动态的添加html代码 2015/07/16

>[原文](http://segmentfault.com/q/1010000000312781&sa=U&ei=r2deU9qOGM6iyAS79YHIDg&ved=0CGMQFjAK&usg=AFQjC)感谢Tychio提供的答案。

1.使用DOM

    //使用createElement创建元素
    var dialog = document.createElement('div');
    var img = document.createElement('img');
    var btn = document.createElement('input');
    var content = document.createElement('span');
    // 添加class
    dialog.className = 'dialog';
    // 属性
    img.src = 'close.gif';
    // 样式
    btn.style.paddingRight = '10px';
    // 文本
    span.innerHTML = '您真的要GG吗？';
    // 在容器元素中放入其他元素
    dialog.appendChild(img);
    dialog.appendChild(btn);
    dialog.appendChild(span);
    
>关于添加class如果不考虑IE兼容性问题，可以使用classList方法，详细[API在这里](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList)。还有很多方法     用于DOM操作，在[这里](http://www.w3school.com.cn/htmldom/dom_methods.asp)。

2.使用HTML5 template标签

    <template id="dialog_tpl">
      <div class="dialog">
        <img src="" alt="">
        <input type="button" value="确认">
        <span></span>
      </div>
    </template>
>接着还是得使用DOM操作，只是不需要创建元素了，然后复制一份副本放入正文即可。

    var dialog = document.querySelector('#dialog_tpl');
    dialog.content.querySelector('img').src = 'close.gif';
    dialog.content.querySelector('span').innerHTML = '您真的要GG吗？';
    document.body.appendChild(dialog.content.cloneNode(true));
    
>template标签是隐藏的，最多是用在列表中，可以产生多个副本。详细使用方法可以参考[这篇文章](http://www.html5rocks.com/en/tutorials/webcomponents/template/?redirect_from_locale=zh)。如果要兼容不支持template的浏览器，可以把content的部分写一个兼容方法，并且把template用CSS隐藏掉即可。

3.使用HTML模板

>[这里](https://developer.mozilla.org/en-US/docs/JavaScript_templates)有各种模板，并且按语法风格分类。其实模板大同小异，就是动态修改模板文件使之成为一个可用的静态HTML文件，其实你也可以自己在需要的地方加载一部分HTML。只需要使用ajax请求一个情态的HTML文件并把返回的HTML代码放入当前的HTML中即可。