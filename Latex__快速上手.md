# Latex__快速上手

[toc]
<!-- toc --> 


## Reference

- [LaTeX - Wikibooks, open books for an open world](https://en.wikibooks.org/wiki/LaTeX)



## Useful Tool
* Math input
    * [Latex Math Symbols](http://web.ift.uib.no/Teori/KURS/WRK/TeX/symALL.html)
    * [Function Support in KaTeX](https://khan.github.io/KaTeX/function-support.html)
    * [Symbols and Functions in KaTeX](https://utensil-site.github.io/available-in-katex/)

- [HackMD – LaTeX 語法與示範 - HackMD](https://hackmd.io/s/B1RwlM85Z#)
- 

## Usage

### 對齊方程式

- [latex - Left align block of equations - Stack Overflow](https://stackoverflow.com/questions/2632628/left-align-block-of-equations)

    > Try this:
    > 
    > ```latex=
    > \begin{align*}
    >     &|\vec a| = \sqrt{3^{2}+1^{2}} = \sqrt{10} &\\
    >     &|\vec b| = \sqrt{1^{2}+23^{2}} = \sqrt{530} &\\ 
    >     &\cos v = \frac{26}{\sqrt{10} \cdot \sqrt{530}} &\\
    >     &v = \cos^{-1} \left(\frac{26}{\sqrt{10} \cdot \sqrt{530}}\right) &\\
    > \end{align*}
    > 
    > ```
    > 
    > $$
    > \begin{align*}
    >     &|\vec a| = \sqrt{3^{2}+1^{2}} = \sqrt{10} &\\
    >     &|\vec b| = \sqrt{1^{2}+23^{2}} = \sqrt{530} &\\ 
    >     &\cos v = \frac{26}{\sqrt{10} \cdot \sqrt{530}} &\\
    >     &v = \cos^{-1} \left(\frac{26}{\sqrt{10} \cdot \sqrt{530}}\right) &\\
    > \end{align*}
    > $$
    > 
    > ---
    > 
    > ![](https://screenshotscdn.firefoxusercontent.com/images/1a4c8de1-ed89-4ce7-92e2-19a63172d701.png)
    > 
    > ---
    > 
    > The `&` sign separates two columns, so an `&` at the beginning of a line means that the line starts with a blank column.

### 對齊多欄方程式

- [LaTeX技巧207：使用align环境输入多行公式的技巧_LaTeX_Fun_新浪博客](http://blog.sina.com.cn/s/blog_5e16f1770100gror.html)

    > ```
    > This example has three column-pairs.
    > $$
    > \begin{align*}
    >     x    &= y      & X  &= Y  &
    >       a  &= b+c               \tag{8}\\
    >     x'   &= y'     & X' &= Y' &
    >       a' &= b                 \tag{9}\\
    >   x + x' &= y + y'            &
    >   X + X' &= Y + Y' & a'b &= c'b \tag{10}
    > \end{align*}
    > $$
    > ```
    > 
    > This example has three column-pairs.
    > $$
    > \begin{align*}
    >     x    &= y      & X  &= Y  &
    >       a  &= b+c               \tag{8}\\
    >     x'   &= y'     & X' &= Y' &
    >       a' &= b                 \tag{9}\\
    >   x + x' &= y + y'            &
    >   X + X' &= Y + Y' & a'b &= c'b \tag{10}
    > \end{align*}
    > $$
    > 
    > ---
    > ![](https://screenshotscdn.firefoxusercontent.com/images/318030fd-3063-4b41-a38a-65542ffd9990.png)

### 方程式標號 numbering

- [numbering - How can you number equations manually? - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/questions/212559/how-can-you-number-equations-manually)

    > ```
    > $$
    > 1+1=2 \tag{5.23} 
    > $$
    > 
    > $$
    > 2+2=4 \tag{5.24} \label{eq:5.24}
    > $$
    > 
    > $$
    > A\ cross-reference\ to\ equation  \eqref{eq:5.24}.
    > $$
    > ```
    > 
    > $$
    > 1+1=2 \tag{5.23} 
    > $$
    > 
    > $$
    > 2+2=4 \tag{5.24} \label{eq:5.24}
    > $$
    > 
    > $$
    > A\ cross-reference\ to\ equation  \eqref{eq:5.24}.
    > $$
    > 
    > ---
    > 
    > ![](https://i.stack.imgur.com/ZFVDZ.png)

### align and align*

- [LaTeX/Advanced Mathematics - Wikibooks, open books for an open world](https://en.wikibooks.org/wiki/LaTeX/Advanced_Mathematics#align_and_align.2A)

    > The align and align* environments, available through the amsmath package, are used for arranging equations of multiple lines. As with matrices and tables, \\ specifies a line break, and & is used to indicate the point at which the lines should be aligned.
    > 
    > The align* environment is used like the displaymath or equation* environment:
    > 
    > ```latex=
    > \begin{align*}
    >  f(x) &= (x+a)(x+b) \\
    >       &= x^2 + (a+b)x + ab
    > \end{align*}
    > ```
    > 
    > $$
    > \begin{align*}
    >  f(x) &= (x+a)(x+b) \\
    >       &= x^2 + (a+b)x + ab
    > \end{align*}
    > $$
    > 
    > ![](https://wikimedia.org/api/rest_v1/media/math/render/svg/05e4336a5cf9dfec390fb4e531249b6a545e3971)
    > 
    > Note that the align environment must not be nested inside an equation (or similar) environment. Instead, align is a replacement for such environments; the contents inside an align are automatically placed in math mode.
    > 
    > align* suppresses numbering. To force numbering on a specific line, use the \tag{...} command before the line break.
    > 
    > align is similar, but automatically numbers each line like the equation environment. Individual lines may be referred to by placing a \label{...} before the line break. The \nonumber or \notag command can be used to suppress the number for a given line:
    > 
    > ```latex=
    > \begin{align}
    >  f(x) &= x^4 + 7x^3 + 2x^2 \nonumber \\
    >       &\qquad {} + 10x + 12
    > \end{align}
    > ```
    > 
    > ![](https://wikimedia.org/api/rest_v1/media/math/render/svg/7369945ec986b2e6fb819409dbd260058a622c91)
    > 

## symbol

### arrow
- [LaTEX Arrow Symbols](http://garsia.math.yorku.ca/MPWP/LATEXmath/node9.html)

    ![](http://garsia.math.yorku.ca/MPWP/LATEXmath/arrow1.gif)

### bar, overline

- [stacking symbols - The \bar and \overline commands - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/questions/22100/the-bar-and-overline-commands)

    > 
    > ```latex
    > $$
    > \newcommand{\overbar}[1]{\mkern 1.5mu\overline{\mkern-1.5mu#1\mkern-1.5mu}\mkern 1.5mu}
    > $$
    > 
    > $\bar{\mathbb{R}}$ 
    > $\overbar{\mathbb{R}}$ 
    > $\overline{\mathbb{R}}$
    > ``` 
    > $$
    > \newcommand{\overbar}[1]{\mkern 1.5mu\overline{\mkern-1.5mu#1\mkern-1.5mu}\mkern 1.5mu}
    > $$
    > 
    > $\bar{\mathbb{R}}$ $\overbar{\mathbb{R}}$ $\overline{\mathbb{R}}$
    > ![](https://i.stack.imgur.com/kN66B.png)





