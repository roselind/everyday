---
layout: default
---
根据阮一峰的这篇文章<<[搭建一个免费的，无限流量的Blog----github Pages和Jekyll入门](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)>>记载的方法, 我通过以下6步成功搭建.

以下是我的记录:

1. 将Github上的blog项目clone到本地:

	git clone git@github.com:googleyufei/everyday.git
	cd everyday

2. 新建_config.yml文件, 在文件中添加如下内容:

	baseurl: /everyday

3. 新建_layouts文件夹, 并在该文件夹内新建默认的layout文件default.html, html内容如下:

```
<!DOCTYPE html>
<html>
<head>
    <meta charset='utf-8'>
    <meta http-equiv="X-UA-Compatible" content="chrome=1">

    <link rel="stylesheet" type="text/css" href="/everyday/stylesheets/stylesheet.css" media="screen">
    <link rel="stylesheet" type="text/css" href="/everyday/stylesheets/pygment_trac.css" media="screen">
    <link rel="stylesheet" type="text/css" href="/everyday/stylesheets/print.css" media="print">
    <meta http-equiv="content-type" content="text/html; charset=utf-8"/>
    <title>{{ page.title }}</title>
</head>
<body>
<header>
    <div class="container">
        <h1>Everyday</h1>

        <h2>余飞的时间统计</h2>

        <section id="downloads">
            <a href="https://github.com/googleyufei/everyday/zipball/master" class="btn">Download as .zip</a>
            <a href="https://github.com/googleyufei/everyday/tarball/master" class="btn">Download as .tar.gz</a>
            <a href="https://github.com/googleyufei/everyday" class="btn btn-github"><span class="icon"></span>View on
                GitHub</a>
        </section>
    </div>
</header>

　　　
<div class="container">
    <section id="main_content">
        　{{ content }}
    </section>
</div>
</body>
</html>
```

4. 创建_posts文件夹, 用于存放博客文件. 新建第一篇博客2014-12-29-hello-world.md:

```md
---
layout: default
title: 你好，世界
---

## {{ page.title }}

我的第一篇文章

{{ page.date | date_to_string }}
```

5. 在everyday文件夹下新建index.html:

```
---
layout: default
title: 余飞的文章列表
---
<h2>{{ page.title }}</h2>
　　<p>最新文章</p>
　　
<ul>
    　　　　{% for post in site.posts %}
    　　　　　　
    <li>{{ post.date | date_to_string }} <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
    　　　　{% endfor %}
</ul>
```


