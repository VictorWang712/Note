---
statistics: true
---

# 首页

<center>
<div id="rcorners">
  <script src="https://sdk.jinrishici.com/v2/browser/jinrishici.js" charset="utf-8"></script>
  <div id="poem_sentence"></div>
  <div id="poem_info"></div>
  <script type="text/javascript">
  jinrishici.load(function(result) {
      var sentence = document.querySelector("#poem_sentence")
      var info = document.querySelector("#poem_info")
      sentence.innerHTML = result.data.content
      info.innerHTML =  '《' + result.data.origin.title + '》' + result.data.origin.author + '【' + result.data.origin.dynasty + '】'
  });
  </script>
</div> 
</center>

<center>
  <link href="https://fonts.googleapis.com/css2?family=Long+Cang&display=swap" rel="stylesheet">

  <style>
    #poem_sentence, #poem_info {
      font-family: "Long Cang", sans-serif;
      font-size: 20px;
      line-height: 1.5;
      text-align: center;
    }
  </style>

  <script src="https://sdk.jinrishici.com/v2/browser/jinrishici.js" charset="utf-8"></script>
  <div id="poem_sentence"></div>
  <div id="poem_info"></div>
  <script type="text/javascript">
    jinrishici.load(function (result) {
      var sentence = document.querySelector("#poem_sentence");
      var info = document.querySelector("#poem_info");
      sentence.innerHTML = result.data.content;
      info.innerHTML = "《" + result.data.origin.title + "》" + result.data.origin.author + " · " + result.data.origin.dynasty;
    });
  </script>
</center>

## 简介

这里是 Walker_V 的笔记本。

记录了上大学以来各方面的学习内容，供自己查阅的同时希望能帮助到更多的人。

## 统计

本网站共有 {{pages}} 个页面，{{words}} 字，{{codes}} 行代码，{{images}} 张图片。

## 致谢

本网站的建设使用或参考了以下内容：

- [Material for MkDocs](https://github.com/squidfunk/mkdocs-material)
- [鹤翔万里的笔记本](https://github.com/TonyCrane/note/)
- [Mkdocs-Wcowin 博客主题](https://github.com/Wcowin/Mkdocs-Wcowin)
- [giscus](https://github.com/giscus/giscus)