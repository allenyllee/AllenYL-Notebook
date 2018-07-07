# Latex__快速上手

[toc]
<!-- toc --> 


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
    > \begin{aligned}
    >     &|\vec a| = \sqrt{3^{2}+1^{2}} = \sqrt{10} &\\
    >     &|\vec b| = \sqrt{1^{2}+23^{2}} = \sqrt{530} &\\ 
    >     &\cos v = \frac{26}{\sqrt{10} \cdot \sqrt{530}} &\\
    >     &v = \cos^{-1} \left(\frac{26}{\sqrt{10} \cdot \sqrt{530}}\right) &\\
    > \end{aligned}
    > 
    > ```
    > 
    > $$
    > \begin{aligned}
    >     &|\vec a| = \sqrt{3^{2}+1^{2}} = \sqrt{10} &\\
    >     &|\vec b| = \sqrt{1^{2}+23^{2}} = \sqrt{530} &\\ 
    >     &\cos v = \frac{26}{\sqrt{10} \cdot \sqrt{530}} &\\
    >     &v = \cos^{-1} \left(\frac{26}{\sqrt{10} \cdot \sqrt{530}}\right) &\\
    > \end{aligned}
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
    > \begin{aligned}
    >     x    &= y      & X  &= Y  &
    >       a  &= b+c               \tag{8}\\
    >     x'   &= y'     & X' &= Y' &
    >       a' &= b                 \tag{9}\\
    >   x + x' &= y + y'            &
    >   X + X' &= Y + Y' & a'b &= c'b \tag{10}
    > \end{aligned}
    > $$
    > ```
    > This example has three column-pairs.
    > $$
    > \begin{aligned}
    >     x    &= y      & X  &= Y  &
    >       a  &= b+c               \tag{8}\\
    >     x'   &= y'     & X' &= Y' &
    >       a' &= b                 \tag{9}\\
    >   x + x' &= y + y'            &
    >   X + X' &= Y + Y' & a'b &= c'b \tag{10}
    > \end{aligned}
    > $$
    > 
    > ---
    > ![](https://screenshotscdn.firefoxusercontent.com/images/318030fd-3063-4b41-a38a-65542ffd9990.png)



## symbol

### arrow
- [LaTEX Arrow Symbols](http://garsia.math.yorku.ca/MPWP/LATEXmath/node9.html)

    ![](http://garsia.math.yorku.ca/MPWP/LATEXmath/arrow1.gif)

### bar, overline

- [stacking symbols - The \bar and \overline commands - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/questions/22100/the-bar-and-overline-commands)

    > 
    > ```latex
    > $\bar{\mathbb{R}}$ 
    > $\overbar{\mathbb{R}}$ 
    > $\overline{\mathbb{R}}$
    > ``` 
    >
    > $\bar{\mathbb{R}}$ $\overbar{\mathbb{R}}$ $\overline{\mathbb{R}}$
    > ![](https://i.stack.imgur.com/kN66B.png)


### 方程式標號 numbering

- [numbering - How can you number equations manually? - TeX - LaTeX Stack Exchange](https://tex.stackexchange.com/questions/212559/how-can-you-number-equations-manually)

    > ```
    > $$
    > 1+1=2 \tag{5.23}
    > $$
    > 
    > $$
    > A\ cross-reference\ to\ equation  \eqref{eq:5.23}.
    > $$
    > ```
    > $$
    > 1+1=2 \tag{5.23}
    > $$
    > 
    > $$
    > A\ cross-reference\ to\ equation  \eqref{eq:5.23}.
    > $$
    > 
    > ---
    > 
    > ![](https://i.stack.imgur.com/ZFVDZ.png)


