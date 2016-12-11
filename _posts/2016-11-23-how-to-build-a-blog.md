---
layout: post
title: 如何使用Github Pages快速搭建博客网站
description: 如何使用Github Pages快速搭建博客网站
date: '2016-11-23 16:26:01 +0800'
categories: 工具
tags:
  - 搭建博客
  - Github Pages
published: true
---

* content
{:toc}

是什么？
------------------------
***

#### Github
> 十分强大的通过Git进行版本控制的软件源代码托管平台，基本主流开源软件都能在Github上找到源代码。

#### Github Pages
> Github上的面向个人、组织和项目的公共静态页面站点托管服务，支持通常的HTML文档，支持jekyll站点。

#### Markdown
> 一种十分流行的轻量级标记语言，让作者不再为排版烦恼，专注于写作。

#### liquid
> 是由Shopify开发的一种模板语言和与之配套的模版引擎。

#### Jekyll
> 静态博客网站生成器，使用liquid渲染模板，支持markdown、textile、HTML&css。

#### Prose
> 一个基于Github Pages的jekyll内容编辑器。

<br><br>

怎么做？
------------------------
***

### Github Pages

##### **1.注册账号**
在<https://github.com/>上注册账号并验证邮箱。

##### **2.创建仓库**
￼￼￼￼￼![创建仓库]({{site.baseurl}}/images/github.png)

如果仓库名设置成`Github账号名称.github.io(如xiaoli000.github.io)`则是个人主页，其他则是项目主页。
<pre>
个人主页默认使用master分支，访问域名为https://Github账号名称.github.io。

项目主页默认使用gh-pages分支(新建仓库后无该分支，需自己新建)，访问域名为https://Github账号名称.github.io/仓库名。
</pre>
主页所使用的Git分支可以在仓库的`Settings->GitHub Pages->Source`中设置。
![设置]({{site.baseurl}}/images/github_settings.png)

##### **3.站点生成**
  * 1.不想自己从头到尾自己设计页面可以到[http://jekyllthemes.org/](http://jekyllthemes.org/)上下载一个模板使用，将下载内容个性化修改后提交到仓库。

  * 2.也可以用Github自带的`Automatic Page Generator`，在`Settings->GitHub Pages->Overwrite site`中设置。
  ![自动生成器]({{site.baseurl}}/images/github_auto.png)

### Jekyll
1.安装ruby环境（mac os自带）；

2.安装jekyll；

```python
~ $ sudo gem install jekyll
```
3.如果没有下载别人提供的[jekyll模板](http://jekyllthemes.org/)，而是自己搭建jekyll，可以执行下面命令初始化目录：

```python
~ $ cd myblog
~/myblog $ jekyll new .
```
4.进入Git项目目录，执行``jekyll serve``，默认可以检测实时变化，浏览器中访问http://localhost:4000(如果_config.yml中设置了baseurl，那么访问地址为http://localhost:4000/$baseurl)；

如果是首次执行，执行过程中可能需要安装一些组件：

```python
~ $ sudo gem install bundler
~ $ sudo gem install minima
~ $ sudo gem install jekyll-feed
```

5.jekyll基本目录结构和使用方法可参考中文官网[http://jekyllcn.com/docs/structure/](http://jekyllcn.com/docs/structure/)。

### 编辑器
1.编辑器可以使用Atom、Sublime Text等带markdown预览插件的文本编辑器，mac上很多人也喜欢用[Mou](http://25.io/mou/);

2.Prose也是一个不错的选择，打开[http://prose.io](http://prose.io)会自动进入授权页面，授权后可以看到自己在Github中的项目；
![prose]({{site.baseurl}}/images/prose.png)

支持在线编辑、预览、提交和一些jekyll的如草稿和区分头信息的功能。
![prose的草稿功能]({{site.baseurl}}/images/prose_draft.png)

3.一个非常赞的markdown速查表

![prose的草稿功能]({{site.baseurl}}/images/markdownsheet.png)

### 评论系统和访问量统计

评论系统如果是面向国内用户可以使用[多说](http://duoshuo.com/),国际用户可以使用[Disqus](https://disqus.com/)，接入都比较简单，站点中加入一段js即可。

访问量统计可以使用[Google Analytics](https://www.google.com/analytics/)。

### 代码高亮

1. `_config.yml`文件中添加`highlighter: rouge`。

2. 命令行执行

```python
~ $ rougify help style
```

查看有哪些样式可用，如选择base16.monokai可执行

```python
~ $ rougify style base16.monokai >> syntax.css
```

生成css文件，引入博客站点中。

遇到了什么问题？
------------------------
***

#### 1、Github账号验证邮箱接受不到邮件
<pre>
邮箱设置添加邮箱地址白名单support@github.com和域名白名单github.com。
</pre>

#### 2、提交静态网页到Git仓库后访问主页返回404
<pre>
站点生成需要几分钟时间，如果一直未生成可能的原因是项目主页默认使用gh-pages的Git分支，而你提交静态网页的是master分支。
</pre>

#### 3、锚点定位元素被头部html覆盖
<pre>
使用css3伪类target。
</pre>
```css
:target{
    padding-top: 70px;
    margin-top: -70px;
}
```

#### 4、markdown转换html错误
<pre>
基本解决方案都是发生错误的标签前面多加个空行。
</pre>	
比如 `##### 标题` 本应该转换成`<h5>标题</h5>`，但实际未发生转换，`##### 标题`前空一行就可以了。

还遇到过一种情况是

<pre>
```shell
~ $ echo hello
```
</pre>
PC端正常转换成了`<pre><code>~ $ echo hello</code></pre>`，但无线端却转换成了`<code> shell~ $ echo hello</code>`，加空行也能解决该问题。

## 相关资料
* [jekyll结构](http://jekyllcn.com/docs/structure/)
* [liquid语法](http://xiajian.github.io/rhg-zh/zh/liquid/) [liquid官网手册](http://shopify.github.io/liquid/basics/introduction/)
* [YAML语法](http://www.ruanyifeng.com/blog/2016/07/yaml.html)

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
