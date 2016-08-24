---
layout: post
title:  jQuery滚动条插件
subtitle:   ""
date:       2015-12-30 15:03:21
author:     "Cyclone77"
header-img: "img/post-bg-js-version.jpg"
permalink:  "/1472014171763"
tags:
    - 前端开发
    - JavaScript
    - jQuery
---
偶然发现IE下滚动条显示的太丑了，谷歌火狐还能设置点样式，在加上练习编写jQuery插件，就拿这个来练手，大神们多多指点.
仓库地址：[jQuery滚动条插件仓库][jQuery-cyScroll].

用法（[滚动条Demo][Demo]）：
{% highlight ruby %}
$("#divParent").cyScroll({
    content: $("#divChild"),
    Style: {
        "width": "6px",
        "background": "#BCBCBA"
    },
    BgStyle: {
        "background": "#EDEDEB"
    }
});
{% endhighlight %}
任何一个div都可以调用,说下插件内容：
由于火狐，IE8以下，其他浏览器值得滚动事件不同，首先同化了浏览器的滚动事件的绑定方法：
{% highlight ruby %}
wheel: function (obj, callback) {
    var wheelType = "mousewheel"
    try {
        document.createEvent("MouseScrollEvents")
        wheelType = "DOMMouseScroll"
    } catch (e) { }
    this.addEvent(obj, wheelType, function (event) {
        if ("wheelDelta" in event) {//统一为±120，其中正数表示为向上滚动，负数表示向下滚动
            var delta = event.wheelDelta
            //opera 9x系列的滚动方向与IE保持一致，10后修正
            if (window.opera && opera.version() < 10)
                delta = -delta;
            //由于事件对象的原有属性是只读，我们只能通过添加一个私有属性delta来解决兼容问题
            event.delta = Math.round(delta) / 120; //修正safari的浮点 bug
        } else if ("detail" in event) {
            event.wheelDelta = -event.detail * 40//为FF添加更大众化的wheelDelta
            event.delta = event.wheelDelta / 120  //添加私有的delta
        }
        callback.call(obj, event);//修正IE的this指向
    });
}
{% endhighlight %}
同化了滚动事件后就好办了，然后就是实现模拟滚动了.

既然滚动条是div构成的那么可以发挥所有想的到的，比如滚动条div的背景可以是图片，更可以是动态图……可以用css3来实现炫酷的效果(可以自定义滚动条的样式).

下一篇细说下这个滚动条插件。

[Demo]:      http://cyclone77.github.io/jQuery-cyScroll
[jQuery-cyScroll]:  https://github.com/Cyclone77/jQuery-cyScroll