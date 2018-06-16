# google_app_script__應用

[toc]
<!-- toc --> 

## google sheet

- [Google Sheet importxml - How to retrieve only the 1st value? - Stack Overflow](https://stackoverflow.com/questions/45750401/google-sheet-importxml-how-to-retrieve-only-the-1st-value)

    > It works fine when there is only 1 title in each result, but returns an error when there are more than 1:
    > 
    >     Error Array result was not expanded because it would overwrite data in C2
    > 
    > How can I limit the result to just the first title tag found, or (probably better) modify the IFERROR to handle this array 'error'?
    > 
    > ---
    > 
    > ```
    > =IFERROR(importxml(B1, "(//title/text())[1]"),A1)
    > ```
    > 
    > Or
    > 
    > ```
    > =ARRAY_CONSTRAIN(IFERROR(importxml(B1, "//title/text()"),A1),1,1)
    > ```

