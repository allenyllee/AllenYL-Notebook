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



## 編輯器

- [marktext/marktext: 📝Next generation markdown editor, running on platforms of MacOS Windows and Linux.](https://github.com/marktext/marktext)

    ![](https://static.oschina.net/uploads/space/2018/0411/185709_WHbk_2720166.gif)

