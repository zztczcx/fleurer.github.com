--- 
layout: post
title: "rails\xE4\xBD\xBF\xE7\x94\xA8paperclip\xE6\x8F\x92\xE4\xBB\xB6\xE4\xB8\x8A\xE4\xBC\xA0\xE6\x97\xB6\xE9\x81\x87\xE5\x88\xB0500 Internal Server Error"
tags: 
- Rails
- ruby
- "\xE5\xA4\x87\xE5\xBF\x98"
status: publish
type: post
published: true
meta: 
  _edit_last: "2"
---
有可能是imageMagick没装利索。找不到imagemagick，显示错误信息的时候试图把上传的文件对象序列化，就505了。

<pre lang="shell">sudo apt-get install imagemagick --fix-missing</pre>

使用三方库就得做好不可预料事件的准备呢。

关于paperclip的使用，这两篇简介好像不错：

- <a href="http://jimneath.org/2008/04/17/paperclip-attaching-files-in-rails/">http://jimneath.org/2008/04/17/paperclip-attaching-files-in-rails/</a>
- <a href="http://thewebfellas.com/blog/2008/11/2/goodbye-attachment_fu-hello-paperclip">http://thewebfellas.com/blog/2008/11/2/goodbye-attachment_fu-hello-paperclip</a>

ps: 又遇到了个没预料的问题，上传validates_attachment_content_type指定的类型之外的文件时候同样会遇到个500 internal server error，未解中。
