# Markdown__快速上手

[toc]
<!-- toc --> 

## Tools

### Paste to Markdown

- [Paste to Markdown](https://euangoddard.github.io/clipboard2markdown/)

### Table Generator

- [Markdown Tables generator - TablesGenerator.com](https://www.tablesgenerator.com/markdown_tables#)


## Usage

### File Path, URL

###### tags: `whitespace`
- [Spaces in path to image file · Issue #54 · alanshaw/markdown-pdf](https://github.com/alanshaw/markdown-pdf/issues/54)

    > [Spaces are illegal in URLs](https://url.spec.whatwg.org/#url-writing).  
[Encode it to `%20`](http://stackoverflow.com/questions/497908/is-a-url-allowed-to-contain-a-space)?

### Comment

- [syntax - Comments in Markdown - Stack Overflow](https://stackoverflow.com/questions/4823468/comments-in-markdown)

    ```
    [//]: # (This may be the most platform independent comment)
    ```

    It may also be prudent to insert a blank line before and after this type of comments, because some Markdown parsers may not like link definitions brushing up against regular text.

### newline

- [newline - How to write one new line in Bitbucket markdown? - Stack Overflow](https://stackoverflow.com/questions/22385334/how-to-write-one-new-line-in-bitbucket-markdown)

    > When you do want to insert a `<br />` break tag using Markdown, you **end a line with two or more spaces, then type `return` or `Enter`**.

### 修改文字顏色

- [如何修改 Markdown 文字顏色 | Niauwu鳥烏](https://niauwu.github.io/2014/06/16/fontColor/)

```html
<font color="white">要反白的文字<font>
```

### 可折疊選單 Collapsible contents (code block)

- [Collapsible contents (code block) in comments / spoiler tag · Issue #166 · dear-github/dear-github](https://github.com/dear-github/dear-github/issues/166)

    > ex1:
    > 
    > <details>
    >   <summary>Click to expand</summary>
    >   whatever
    > </details>
    > 
    > 
    > ex2:
    > 
    > <details><summary>stuff with *mark* **down**</summary><p>
    > 
    > ## _formatted_ **heading** with [a](link)
    > 
    > ---
    > {{standard 3-backtick code block omitted from here due to escaping issues}}
    > ---
    > 
    > Collapsible until here.
    > </p></details>
    > 
    > ex3:
    > 
    > <details>
    >  <summary>Summary</summary>
    > 
    > ```js
    > const x = 1
    > ```
    > </details>
    > 
    > ex5:
    > 
    > <details>
    >   <summary><code>&lt;code&gt;</code>tags work inside summary</summary>
    > 
    > <code>&lt;code&gt;</code>
    > 
    > </details>

### Markdown怎么嵌入图片、音乐、视频(HTML5)

- [Markdown怎么嵌入图片、音乐、视频？ | 大大大大大鹏](https://yaohp.github.io/2015/11/04/Markdown%E6%80%8E%E4%B9%88%E5%B5%8C%E5%85%A5%E5%9B%BE%E7%89%87%E3%80%81%E9%9F%B3%E4%B9%90%E3%80%81%E8%A7%86%E9%A2%91%EF%BC%9F/)

    > 到目前为止，我的博客中几乎清一色的文本，偶尔夹杂图片。但是有些需求要嵌入其他多媒体，于是想了解一下怎样在博文中嵌入音乐、视频、flash等多媒体文件。\
    > 实际上，在hexo中，markdown支持html标签，md文件解析为html时原有的html部分会保留。有基于此，我们只要在文中插入符合html规范的代码即可。下面举例说明。
    > 
    > ### 图片
    > 
    > #### MD语法代码：
    > 
    > ```
    > ![](http://ww4.sinaimg.cn/cmw218/005uPDlbgw1f1drj093cej30zk0qon4d.jpg)
    > ```
    > 
    > 
    > 效果：
    > ![](http://ww4.sinaimg.cn/cmw218/005uPDlbgw1f1drj093cej30zk0qon4d.jpg)
    > 
    > #### HTML代码：
    > 
    > 
    > ```
    > <img src="http://ww4.sinaimg.cn/cmw218/005uPDlbgw1f1drj093cej30zk0qon4d.jpg" alt="美女">
    > ```
    > 
    > 
    > 效果：\
    > ![美女](http://ww4.sinaimg.cn/cmw218/005uPDlbgw1f1drj093cej30zk0qon4d.jpg)
    > 
    > ### 音乐
    > 
    > 以『虾米音乐』为例，歌曲页面有个『转帖』选项，将html代码或javascript代码复制到文中即可。
    > 
    > #### 普通HTML代码：
    > 
    > 
    > ```
    > <embed src="http://www.xiami.com/widget/0_3515679/singlePlayer.swf" type="application/x-shockwave-flash" width="257" height="33" wmode="transparent"></embed>
    > ```
    > 
    > 
    > 效果：
    > 
    > <embed src="http://www.xiami.com/widget/0_3515679/singlePlayer.swf" type="application/x-shockwave-flash" width="257" height="33" wmode="transparent"></embed>
    > 
    > #### HTML5代码：
    > 
    > 
    > ```
    > <audio src="http://www.xiami.com/widget/0_3515679/singlePlayer.swf" controls="controls">Your browser does not support the audio tag.</audio>
    > ```
    > 
    > 
    > 效果：
    > 
    > <audio src="http://www.xiami.com/widget/0_3515679/singlePlayer.swf" controls="controls">Your browser does not support the audio tag.</audio>
    > 
    > ### 视频
    > 
    > 嵌入视频的方法和音乐类似，视频网站每个视频页面都会有一个『分享』或『转帖』按钮，点击可以查看代码。
    > 
    > #### 普通HTML代码：
    > 
    > 
    > ```
    > <iframe height=498 width=510 src="http://lxqncdn.miaopai.com/stream/BvmaXK2X49guVi4ehlOjjQ__.mp4" frameborder=0 allowfullscreen></iframe>
    > ```
    > 
    > 
    > 效果：
    > 
    > <iframe height=498 width=510 src="http://lxqncdn.miaopai.com/stream/BvmaXK2X49guVi4ehlOjjQ__.mp4" frameborder=0 allowfullscreen></iframe>
    > 
    > #### HTML5代码：
    > 
    > 
    > ```
    > <video src="http://lxqncdn.miaopai.com/stream/BvmaXK2X49guVi4ehlOjjQ__.mp4" width="320" height="240" controls="controls">Your browser does not support the video tag.</video>
    > ```
    > 
    > 
    > 效果：
    > 
    > <video src="http://lxqncdn.miaopai.com/stream/BvmaXK2X49guVi4ehlOjjQ__.mp4" width="320" height="240" controls="controls">Your browser does not support the video tag.</video>
    > 
    > ### 万能
    > 
    > 对于有些音乐、视频找不到『转帖』按钮的，可以查看源代码，找到相应的代码块贴在文中。若找不到，说明该文件的确不能放在自己文中了。



## 編輯器

- [marktext/marktext: 📝Next generation markdown editor, running on platforms of MacOS Windows and Linux.](https://github.com/marktext/marktext)

    ![](https://static.oschina.net/uploads/space/2018/0411/185709_WHbk_2720166.gif)

