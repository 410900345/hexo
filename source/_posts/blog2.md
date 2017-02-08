---
title: GitHub + Hexo 搭建博客总结(二)
date: 2017-02-07 17:34:35
tags:
categories: 
  tools
---
### 1.创建分类
建立分类文件夹
	
	hexo new page categories
xxx.md 头部写成这样

	title: GitHub + Hexo 搭建博客总结(二)
	date: 2017-02-07 17:34:35
	tags:
	categories: 
 	  tools	
 	  
### 2.底部统计
安装脚本（必选）,[参考链接](http://wangcaiyong.com/2015/06/26/busuanzi/)
打开themes/你的主题/layout/_partial/footer.pejs添加如下脚本即可。

	<script async src="https://dn-lbstatics.qbox.me/	busuanzi/2.3/busuanzi.pure.mini.js">
	</script>
### 3.为Hexo 添加 Swiftype 站内搜索
1.去 Swiftype[官网](https://swiftype.com/)注册好账号，然后点击 Create Engine，输入网址并填好名称，配置好后 Swiftype 会自动开始抓取网站数据，点击 Manage 下面的 Content ，就能看到抓取到的网站数据。
2.打开 Hexo 主题配置，以 jacman 为例，打开 jacman 目录下的 _config.yml 文件，在末尾添加
	
	swift_search:     ## https://swiftype.com/
	enable: true
	id: ## 这里填写前面记下的 Swiftype id
3.替换文件,在到 jacman\layout\/_partial 目录，打开 header.ejs 这个文件

	<% } else if(theme.baidu_search.enable){ %>
	<form class="search" action="<%- theme.baidu_search.site %>" target="_blank">
	<label>Search</label>
	<input name="s" type="hidden" value= <%= theme.baidu_search.id %> ><input type="text" name="q" size="30" placeholder="<%= __('search') %>"><br>
	</form>
	
在这段代码后边添加

	<% } else if(theme.swift_search.enable){ %>
	<form class="search" action="<%- config.root %>search/index.html" method="get" accept-charset="utf-8">
	<label>Search</label>
	<input type="text" id="search" class="st-default-search-input" maxlength="20" placeholder="Search" />
	
	</form>
最后在文件最后一个</div>前添加

	<script type="text/javascript">
	(function(w,d,t,u,n,s,e){w['SwiftypeObject']=n;w[n]=w[n]||function(){
	(w[n].q=w[n].q||[]).push(arguments);};s=d.createElement(t);
	e=d.getElementsByTagName(t)			[0];s.async=1;s.src=u;e.parentNode.insertBefore(s,e);
		  })(window,document,'script','//s.swiftypecdn.com/install/v2/	st.js','_st');
	_st('install','<%- theme.swift_search.id %>','2.0.0');
	</script>	
### 4.图片处理
用七牛为 Hexo 存储图片[链接](http://clarkky.org/post/Hexo-Qiniu-Image-CDN/)
### 5开启统计
hexo安装统计插件,[链接](http://www.cnblogs.com/tengj/p/5365434.html)