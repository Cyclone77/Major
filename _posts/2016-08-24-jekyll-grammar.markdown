---
layout:     post
title:      jekyll模板、语法
subtitle:   jekyll是静态网站/博客生成工具，在这里记录一下jekyll的变量及模板语法，jekyll基于Liquid模板进行扩展，大部分可参考Liquid语法
date:       2016-08-24
author:     "Cyclone77"
header-img: "img/post-bg-js-version.jpg"
tags:
    - Jekyll
---
{% if page.description %}
>{{ page.description }}
{% endif %}

## 页面头部

``` yaml
---
layout:   post
title:    title
category: blog #或者categories: [blog, photo]
description: description
published: false # default true
permalink: /photo # 重置当前页面的访问地址
---
```


## 全局变量

- `site` _config.yml 中配置的信息
- `page` 当前页面的配置信息
- `content` 模板中,用于引入子节点的内容
- `paginator` 分页信息

### site下的变量
- `site.time` 运行 jekyll 的时间
- `site.pages` 所有页面
- `site.posts` 所有文章
- `site.related_posts` 类似的10篇文章,默认最新的10篇文章,指定lsi为相似的文章
- `site.static_files` 没有被 jekyll 处理的文章,有属性 path, modified_time 和 extname.
- `site.html_pages` 所有的html页面
- `site.collections` 所有集合
- `site.data` _data 目录下的数据
- `site.documents` 所有集合中的文档
- `site.categories` 所有的category
- `site.tags` 所有的tag

### page下的变量
- `page.content` 页面的内容
- `page.title` 标题
- `page.excerpt` 摘要
- `page.url` 链接
- `page.date` 时间
- `page.id` 唯一标示
- `page.categories` 分类
- `page.tags` 标签
- `page.path` 源代码位置
- `page.next` 下一篇文章
- `page.previous` 上一篇文章

### paginator下的变量
- `paginator.per_page` 每页记录数
- `paginator.posts` 当前页的文章列表
- `paginator.page` 当前页码
- `paginator.total_posts` 文章总数
- `paginator.total_pages` 总页数
- `paginator.previous_page` 上页页码
- `paginator.next_page` 下页页码
- `paginator.previous_page_path` 上页路径
- `paginator.next_page_path` 下页路径

## 模板语法

### 循环
-反向排序并循环输出前10-20条文章

``` liquid
{% raw %}{% for post in site.posts limit:20 offset:10 reversed %}
    {{ post.title }} {{ post.excerpt | remove: 'fuck' }}
{% endfor %}{% endraw %}
```

### 判断
- `and` 且
- `or` 或
- `contains` 包含

``` liquid
{% raw %}{% if page.excerpt %}
    {{ page.excerpt| strip_html }}
{% elsif page.description %}
    {{ page.description }}
{% else %}
    {{ site.description }}
{% endif %}{% endraw %}
```

### 多条件
``` liquid
{% raw %}{% case condition %}
    {% when 1 %}
    here is 1
    {% when 2 or 3 %}
    herer is 2 or 3
    {% else %}
    ... else ...
{% endcase %}{% endraw %}
```

### 赋值

``` liquid
{% raw %}{% assign index = 1 %}{% endraw %}
```

### 代码高亮
-显示行号 linenos
支持的语言参考[Rough Wiki](https://github.com/jneen/rouge/wiki/List-of-supported-languages-and-lexers)

``` liquid
{% raw %}{% highlight js linenos %}
console.log('Hello world!')
{% endhighlight %}{% endraw %}
```

## 常用过滤器

- `| date` 日期格式化 e.g. date: "%Y %h"
- `| size` 输出数组长度
- `| number_of_words` 输出单词个数-按照空格split后的数组长度
- `| array_to_sentence_string` 逗号拼接数组-最后两个使用and拼接
- `| sort:'title'`  排序
- `| remove:'fuck'` 过滤内容
- `| strip_html` 删除html标签
- `| xml_escape` xml转义
- `| escape` 字符串转义
- `| capitalize` 首字符大写
- `| cgi_escape` url转义，from 'x,y;z?' to 'x%2Cy%3Bz%3F'
- `| jsonify` 格式化json数据输出
- `| where:'title', 'today'` 查找title为'today'的数据

### 日期格式化

- `| date_to_string` 07 Nov 2008
- `| date_to_long_string` 07 November 2008
- `| date_to_rfc822` Mon, 07 Nov 2008 13:07:54 -0800
- `| date_to_xmlschema` 2008-11-07T13:07:54-08:00
