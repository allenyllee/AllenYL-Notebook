# Latex__快速上手

[toc]
<!-- toc --> 


## Useful Tool
* Math input
    * [Latex Math Symbols](http://web.ift.uib.no/Teori/KURS/WRK/TeX/symALL.html)
    * [Function Support in KaTeX](https://khan.github.io/KaTeX/function-support.html)
    * [Symbols and Functions in KaTeX](https://utensil-site.github.io/available-in-katex/)

## Usage

- [latex - Left align block of equations - Stack Overflow](https://stackoverflow.com/questions/2632628/left-align-block-of-equations)

    Try this:

    ```latex=
    \begin{aligned}
        &|\vec a| = \sqrt{3^{2}+1^{2}} = \sqrt{10} &\\
        &|\vec b| = \sqrt{1^{2}+23^{2}} = \sqrt{530} &\\ 
        &\cos v = \frac{26}{\sqrt{10} \cdot \sqrt{530}} &\\
        &v = \cos^{-1} \left(\frac{26}{\sqrt{10} \cdot \sqrt{530}}\right) &\\
    \end{aligned}

    ```
    
    $$
    \begin{aligned}
        &|\vec a| = \sqrt{3^{2}+1^{2}} = \sqrt{10} &\\
        &|\vec b| = \sqrt{1^{2}+23^{2}} = \sqrt{530} &\\ 
        &\cos v = \frac{26}{\sqrt{10} \cdot \sqrt{530}} &\\
        &v = \cos^{-1} \left(\frac{26}{\sqrt{10} \cdot \sqrt{530}}\right) &\\
    \end{aligned}
    $$

    The `&` sign separates two columns, so an `&` at the beginning of a line means that the line starts with a blank column.
