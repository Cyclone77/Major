---
layout: 	post
title:  	CSS优先级
date:   	2016-01-13 16:33:07
subtitle:   ""
author:     "Cyclone77"
header-img: "img/post-bg-js-version.jpg"
permalink:  "/1472014256629"
tags:
    - 前端开发
    - CSS
---

**CSS优先级[^footNote0]**

[^footNote0]: 参考资料:[MDN][1]

>如果优先级相同，靠后的 CSS 会应用到元素上。
>元素在文档树中的位置是不会影响优先级的。

**优先级顺序**

下列是一份优先级逐级增加的选择器列表：

- **内联样式[^footNote1]**
- **ID选择器[^footNote2]**
- **伪类[^footNote3]**
- **属性选择器[^footNote4]**
- **类选择器[^footNote5]**
- **元素(类型)选择器[^footNote6]**
- **通用选择器（*）[^footNote7]**

[^footNote1]:```<span style="color: #000;">Text</span>```

[^footNote2]:```#test { color: yellow; }```

[^footNote3]:```a:hover{ background-color:yellow; }```

[^footNote4]:```span[attr="age"]{ color: red; }```

[^footNote5]:```.bgcolor{ background-color: blue; }```

[^footNote6]:```span{ color: red; }```

[^footNote7]:```*{ color: red; }```

**!important 规则例外**

当 !important 规则被应用在一个样式声明中时,该样式声明会覆盖CSS中任何其他的声明, 无论它处在声明列表中的哪里.

- **Never 永远不要在全站范围的 css 上使用 !important**
- **Only 只在需要覆盖全站或外部 css（例如引用的 ExtJs 或者 YUI ）的特定页面中使用   !important**
- **Never 永远不要在你的插件中使用 !important**
- **Always 要优化考虑使用样式规则的优先级来解决问题而不是 !important**

>怎样覆盖掉 !important: 应用到更高优先级的选择器

**:not 伪类例外**

{% highlight ruby %}
div.outer p {
    color:orange;
}
div:not(.outer) p {
    color: blue;
}
<div class="outer">
    <p>字体颜色为orange</p>
    <div class="inner">
        <p>字体颜色为blue</p>
    </div>
</div>
{% endhighlight %}
  [1]: https://developer.mozilla.org/zh-CN/docs/Web/CSS