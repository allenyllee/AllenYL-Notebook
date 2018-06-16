# Xpath__快速上手

[toc]
<!-- toc --> 


## Reference

- [XPath Syntax](https://www.w3schools.com/xml/xpath_syntax.asp)

- [XPath Examples](https://www.w3schools.com/xml/xpath_examples.asp)

## 選擇文字

- [xml - How to get xpath text from element but exclude some of it based on class? - Stack Overflow](https://stackoverflow.com/questions/28903721/how-to-get-xpath-text-from-element-but-exclude-some-of-it-based-on-class)

    > How can I get the text "Show ME, and Show me too" using xpath expression? I need the "OMIT ME" omitted.
    > 
    > ```html
    > <table>
    > <tr>
    > <td>
    > <span class="omitME">OMIT ME</span>
    > Show ME, and
    > <span class="showME"> Show me too</span>
    > </td>
    > </tr>
    > </table>
    > ```
    > 
    > ---
    > In XPath, you could use:
    > 
    > ```html
    > /table/tr/td//text()[not(parent::span[@class='omitME'])]
    > ```
    > 
    > to select all text nodes descendants of the `td` element, except those whose parent is a `span` of the 'omitME' class.
    > 
    > Or perhaps:
    > 
    > ```html
    > //text()[not(parent::span[@class='omitME'])]
    > ```
    > 
    > to select all text nodes descendants of the root node - again, except those whose parent is an "omitted" `span`.
    > 
