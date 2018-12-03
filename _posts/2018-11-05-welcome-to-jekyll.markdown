---
layout: post
title:  "安装 Jekyll!"
date:   2018-11-07 21:40:36 -0500
categories: jekyll update
author: wangxiaofeng@hualala.com
tags: jekyll markdown
---

# 一、jekyll简介

jekyll是一个简单的免费的Blog生成工具，可以看做一个将markdown文件生成静态网站的工具，并且他可以免费部署在github上，结合github Pages，我们可以在自己的github.io上看我们的markdown“静态网站”

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/


# 二、安装

clone 项目到本地
```
git clone http://git.hualala.com/hualala_mall/jekyllBlog
```
安装启动jekyll
```
gem install jekyll      //没有gem请自行google配置ruby环境

gem install bundler     //Bundler 是管理Gem相依性的工具

gem install minima      //主题

jekyll -v               //查看版本

bundle                  //安装依赖的Gem文件

bundle exec jekyll server           //进入项目目录,启动本地服务
```

启动浏览器，输入 `127.0.0.1：4000` 查看结果

### 安装执行错误排查

运行jekyll 命令报错

```
/System/Library/Frameworks/Ruby.framework/Versions/2.3/usr/lib/ruby/2.3.0/rubygems/core_ext/kernel_require.rb:55:in `require': cannot load such file -- bundler (LoadError)
```
原因未安装bundler
解决方法：

命令需要sudo

```
gem install bundler
```

依然报错

```
/System/Library/Frameworks/Ruby.framework/Versions/2.3/usr/lib/ruby/2.3.0/rubygems/core_ext/kernel_require.rb:55:in `require': cannot load such file -- bundler (LoadError)
```

解决

```
gem install minima
```

运行jekyll serve报错
```
WARN: Unresolved specs during Gem::Specification.reset:
      rouge (< 4, >= 1.7)
WARN: Clearing out unresolved specs.
Please report a bug if this causes problems.
/usr/local/lib/ruby/gems/2.4.0/gems/bundler-1.17.1/lib/bundler/spec_set.rb:91:in `block in materialize': Could not find concurrent-ruby-1.1.3 in any of the sources (Bundler::GemNotFound)
	from /usr/local/lib/ruby/gems/2.4.0/gems/bundler-1.17.1/lib/bundler/spec_set.rb:85:in `map!'
	from /usr/local/lib/ruby/gems/2.4.0/gems/bundler-1.17.1/lib/bundler/spec_set.rb:85:in `materialize'
	from /usr/local/lib/ruby/gems/2.4.0/gems/bundler-1.17.1/lib/bundler/definition.rb:170:in `specs'
	from /usr/local/lib/ruby/gems/2.4.0/gems/bundler-1.17.1/lib/bundler/definition.rb:237:in `specs_for'
	from /usr/local/lib/ruby/gems/2.4.0/gems/bundler-1.17.1/lib/bundler/definition.rb:226:in `requested_specs'
	from /usr/local/lib/ruby/gems/2.4.0/gems/bundler-1.17.1/lib/bundler/runtime.rb:108:in `block in definition_method'
	from /usr/local/lib/ruby/gems/2.4.0/gems/bundler-1.17.1/lib/bundler/runtime.rb:20:in `setup'
	from /usr/local/lib/ruby/gems/2.4.0/gems/bundler-1.17.1/lib/bundler.rb:107:in `setup'
	from /usr/local/lib/ruby/gems/2.4.0/gems/jekyll-3.8.5/lib/jekyll/plugin_manager.rb:50:in `require_from_bundler'
	from /usr/local/lib/ruby/gems/2.4.0/gems/jekyll-3.8.5/exe/jekyll:11:in `<top (required)>'
	from /usr/local/bin/jekyll:22:in `load'
	from /usr/local/bin/jekyll:22:in `<main>'
```

解决方法：
  删除 Gemfile.lock


# 三、使用

1. 添加文章

文章都放在_posts目录下，格式需要严格按照年-月-日-文章名.markdown/md

文件开头参照默认格式

```
---
layout: post
title:  "post title"                          // 文章标题
date:   2018-11-29 09:56:49 +0800
categories: js react react-native             //文章分类信息
tags: markdown
---
```

2. 文章提交：
```
git commit -am 'you new blog title'
git push
```

3. jekyll 使用图片

```
[图片pic1]({{ "/assets/images4post/pic1.jpg" | absolute_url }})
jekyll框架下post中引用asset资源目录的图片语法(绝对路径)如下:
![图片pic1]({{ "/assets/images4post/pic1.jpg" | absolute_url }})
```

4.使用tag（修改于12-3切换h2o主题）
```
---
layout: post
title:  "post title"                          // 文章标题
date:   2018-11-29 09:56:49 +0800
categories: js react react-native             //文章分类信息
tags: markdown
---
```
h2o主题可以自动识别并提取tag分类，照上文添加tag即可

# 四、整合disqus评论（12-3）
现在主流第三方评论系统有gitalk，disqus等

gitalk是国人编写，使用github oauth app获取github中repo的读写权限，使得该repo的issue可以在博客中使用，我们的系统没有放在公有github上，故此插件难以使用。

disqus是国外编写的第三方插件，包含评论功能，但使用时需要翻墙，否则看不见，集成步骤如下：

1. 注册Disqus并拿到你的shortname

    [参照链接](https://damoqiongqiu.github.io/jekyll/2017/07/07/%E5%88%A9%E7%94%A8github%E5%92%8Cjekyll%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BABlog-12.html) 需要翻墙

2. 在jekyll的h2o主题中集成

- _config.yml中
```
# Comments 评论功能
comments:
  disqus: true
  disqus_url: 'https://leginm.disqus.com/embed.js'
```
- _layouts/_post中

```
{% if site.comments.disqus %}
<section class="post-footer-item comment">
    <div id="disqus_thread"></div>
</section>
{% endif %}
```

```
{% if site.comments.disqus %}
<script>
var disqus_config = function () {
this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
*/
(function() { // DON'T EDIT BELOW THIS LINE
  var d = document, s = d.createElement('script');
  s.src = 'https://md-22city-cn.disqus.com/embed.js';
  s.setAttribute('data-timestamp', +new Date());
  (d.head || d.body).appendChild(s);
})();
</script>
{% endif %}
```
文件结构已经写好，只要改相应参数就可

done~

[Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)







