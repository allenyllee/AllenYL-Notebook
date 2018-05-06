# Regular_Expression__快速上手

[toc]
<!-- toc --> 


## Tools
- [Online regex tester and debugger: PHP, PCRE, Python, Golang and JavaScript](https://regex101.com/)

## Usage

```
\d 數字 [0-9] 
\D 非數字 [^0-9] 
\w 數字、字母、底線 [a-zA-Z0-9_] 
\W 非 \w [^a-zA-Z0-9_] 
\s 空白字元 [ \r\t\n\f] 
\S 非空白字元 [^ \r\t\n\f]
```

- [regex - Regular Expression "Matching" vs "Capturing" - Stack Overflow](https://stackoverflow.com/questions/21200514/regular-expression-matching-vs-capturing)

    > Matching:
    > 
    > When engine matches a part of string or the whole but does return nothing.
    > Capturing:
    > 
    > When engine matches a part of string or the whole and does return something.
    > 
    > -- What's the meaning of returning?
    > 
    > When you need to check/store/validate/work/love a part of string that your regex matched it before you need capturing groups (...)
    > 
    > At your example this regex .*?\d+ just matches the dates and years See here
    > 
    > And this regex .*?(\d+) matches the whole and captures the year See here
    > 
    > And (.*?(\d+)) will match the whole and capture the whole and the year respectively See here
    > 
    > *Please notice the bottom right box titled Match groups


- [java - Getting the text that follows after the regex match - Stack Overflow](https://stackoverflow.com/questions/5006716/getting-the-text-that-follows-after-the-regex-match)

    > You can do this with "just the regular expression" as you asked for in a comment:
    > 
    > (?<=sentence).*
    > 
    > (?<=sentence) is a positive lookbehind assertion. This matches at a certain position in the string, namely at a position right after the text sentence without making that text itself part of the match. Consequently, (?<=sentence).* will match any text after sentence.


- [regex - What is a non-capturing group? What does (?:) do? - Stack Overflow](https://stackoverflow.com/questions/3512471/what-is-a-non-capturing-group-what-does-do)

    > Let me try to explain this with an example.
    > 
    > Consider the following text:
    > 
    > https://stackoverflow.com/
    > https://stackoverflow.com/questions/tagged/regex
    > 
    > Now, if I apply the regex below over it...
    > 
    > (https?|ftp)://([^/\r\n]+)(/[^\r\n]*)?
    > 
    > ... I would get the following result:
    > 
    > Match "https://stackoverflow.com/"
    >      Group 1: "http"
    >      Group 2: "stackoverflow.com"
    >      Group 3: "/"
    > 
    > Match "https://stackoverflow.com/questions/tagged/regex"
    >      Group 1: "http"
    >      Group 2: "stackoverflow.com"
    >      Group 3: "/questions/tagged/regex"
    > 
    > But I don't care about the protocol -- I just want the host and path of the URL. So, I change the regex to include the non-capturing group (?:).
    > 
    > (?:https?|ftp)://([^/\r\n]+)(/[^\r\n]*)?
    > 
    > Now, my result looks like this:
    > 
    > Match "https://stackoverflow.com/"
    >      Group 1: "stackoverflow.com"
    >      Group 2: "/"
    > 
    > Match "https://stackoverflow.com/questions/tagged/regex"
    >      Group 1: "stackoverflow.com"
    >      Group 2: "/questions/tagged/regex"
    > 
    > See? The first group has not been captured. The parser uses it to match the text, but ignores it later, in the final result.


- [regex - Regular Expression Lookbehind doesn't work with quantifiers ('+' or '*') - Stack Overflow](https://stackoverflow.com/questions/9030305/regular-expression-lookbehind-doesnt-work-with-quantifiers-or)

    > Many regular expression libraries do only allow strict expressions to be used in look behind assertions like:
    > 
    >     only match strings of the same fixed length: (?<=foo|bar|\s,\s) (three characters each)
    >     only match strings of fixed lengths: (?<=foobar|\r\n) (each branch with fixed length)
    >     only match strings with a upper bound length: (?<=\s{,4}) (up to four repetitions)
    > 
    > The reason for these limitations are mainly because those libraries can’t process regular expressions backwards at all or only a limited subset.
    > 
    > Another reason could be to avoid authors to build too complex regular expressions that are heavy to process as they have a so called [pathological behavior](http://swtch.com/~rsc/regexp/regexp1.html) (see also [ReDoS](http://en.wikipedia.org/wiki/ReDoS)).
    > 
    > See also [section about limitations of look-behind assertions](http://www.regular-expressions.info/lookaround.html#limitbehind) on [Regular-Expressions.info](http://www.regular-expressions.info/).


## negate (unsolved)

- [How to negate the whole regex? - Stack Overflow](https://stackoverflow.com/questions/2637675/how-to-negate-the-whole-regex)

    > I have a regex, for example (ma|(t){1}). It matches ma and t and doesn't match bla.
    > 
    > I want to negate the regex, thus it must match bla and not ma and t, by adding something to this regex.

- [regex - how to negate any regular expression in Java - Stack Overflow](https://stackoverflow.com/questions/8610743/how-to-negate-any-regular-expression-in-java)

    > I have a regular expression which I want to negate, e.g.
    > 
    > /(.{0,4})
    > 
    > which String.matches returns the following
    > 
    > "/1234" true
    > "/12" true
    > "/" true
    > "" false
    > "1234" false
    > "/12345" false
    > 
    > Is there a way to negate (using regx only) to the above so that the results are:
    > 
    > "/1234" false
    > "/12" false
    > "/" false
    > "" true
    > "1234" true
    > "/12345" true
    > 
    > I'm looking for a general solution that would work for any regx without re-writing the whole regex.


## 練習解說

- https://regex101.com/r/oK6iB8/17

    ```
    ( (?<=, ))
    ```

    選取逗號後面的空白


- https://regex101.com/r/mh9zgC/1

    ![](https://screenshotscdn.firefoxusercontent.com/images/61a80f64-6c92-45b5-9e32-0049d425edb2.png)

    ```
    [^']+(?<!\S)\s|\b\w+\b
    ```

    解說:
    
    1. `[^']` : 選擇沒有 `'` 的部分
    2. `[^']+` : 將沒有 `'` 的連續部分連起來
    3. `[^']+\s `: 在沒有 `'` 的連續部分中，選擇最後一個字元為空白的字串
    4. `[^']\+(?<!\S)\s` : 在沒有 `'` 且最後一個字元為空白的連續字串中，從後往前找，空白字元後接的不是非空白字元的字串
    5. `\b` : 定位單字邊界
    6. `\b\w+\b` : 單字邊界中，夾的任何非符號的字



- https://regex101.com/r/mh9zgC/4

    ![](https://screenshotscdn.firefoxusercontent.com/images/08fc3389-0c5f-49d7-9622-7f1b75437b98.png)

    ```
    (?=\[)\[|\](?<=\])|\s(?<=\,\s)|(?=\'(\w+|\s+))\'|\'(?<=(\w|\s)\')
    ```

    解說:

    1. `(?=\[)\[` : 從前往後找出現 `[` 的條件下，選擇`[`
    2. `\](?<=\])` : 從後往前找出現 `]` 的條件下，選擇 `]` 
    3. `\s(?<=\,\s)` : 從後往前找出現 `, ` (逗號空格) 的條件下，選擇 ` ` (空格) 
    4. `(?=\'(\w+|\s+))\'` : 從前往後找出現 `\'(\w+|\s+)` ( `'` 後接連續文字或連續空白) 的條件下，選擇 `'`
    5. `\'(?<=(\w|\s)\')` : 從後往前找出現 `(\w|\s)\'` (單個文字或單個空白後接 `'` ，因為向後找不支援未定長度) 的條件下，選擇 `'`


- [Regex for checking if a string between quotes has spaces - Stack Overflow](https://stackoverflow.com/questions/30706465/regex-for-checking-if-a-string-between-quotes-has-spaces)

    You can use this regex to find text inside " with at least a space:
    ```
    (?=(?:(?:[^"]*"){2})*[^"]*$)"(?=[^"]* )[^"]+"
    ```
    Just remember this doesn't account for escaped and unbalanced quotes.

    [Demo](https://regex101.com/r/jZ3qE4/2)

    ![](https://screenshotscdn.firefoxusercontent.com/images/63181561-2001-41e1-a360-9144745b331c.png)

    解說:

    1. `(?:[^"]*)` : 沒有出現 `"` 的連續字串群組

        ![](https://screenshotscdn.firefoxusercontent.com/images/c75fa1cc-ed49-4271-b9ed-7497eef72997.png)

    3. `(?:[^"]*")` : 沒有出現 `"` 的字串群組後加上一個`"`

        ![](https://screenshotscdn.firefoxusercontent.com/images/6bb63220-f48e-40c4-a88e-c4da49c681b5.png)

    4. `(?:[^"]*"){2}` : 取上述模式重複兩次

        ![](https://screenshotscdn.firefoxusercontent.com/images/f332fff4-802c-47b2-9cf5-0b1bf3066f4f.png)

    5. `(?:(?:[^"]*"){2})` : 將上述模式變成群組。如此，每一群組中就包含了兩個 `"` (雙引號)，能夠選出被兩個雙引號包含的詞。

    6. `(?:(?:[^"]*"){2})[^"]` : 上述群組後接一個非`"` 字元

        ![](https://screenshotscdn.firefoxusercontent.com/images/a23cdcda-505f-4bcc-964e-fa7536c4f5e8.png)

    7. `(?:(?:[^"]*"){2})[^"]*` : 上述群組後接多個非`"` 字元。如此選擇邊界就移到下個群組的`"` 之前。

        ![](https://screenshotscdn.firefoxusercontent.com/images/697f35ed-5ee6-4c94-b94b-b0d9b7dd61ab.png)

    8. `(?=(?:(?:[^"]*"){2})[^"]*)"` : 上述樣式出現的群組中，選擇其中的`"`

        ![](https://screenshotscdn.firefoxusercontent.com/images/9ad954d3-2a3f-46e9-b045-405f5161fcd3.png)

    9. `(?=(?:(?:[^"]*"){2})[^"]*)"[^"]` : 從上述選中的`"` 開始，往前增加一個非`"` 字元

        ![](https://screenshotscdn.firefoxusercontent.com/images/6144656a-3f4d-44f6-b3b6-ed4f1ecec25a.png)

    10. `(?=(?:(?:[^"]*"){2})[^"]*)"[^"]+` : 從上述選中的`"` 開始，往前增加多個非`"` 字元

        ![](https://screenshotscdn.firefoxusercontent.com/images/70ba93ba-abf8-4d72-97c8-ee837eb061d4.png)

    11. `(?=(?:(?:[^"]*"){2})[^"]*)"[^"]+"` : 上述樣式後接一個`"`。如此，就把一對雙引號跟其中包含的詞都選出來了。

        ![](https://screenshotscdn.firefoxusercontent.com/images/38165765-9e52-48b4-9e9f-bc4f21f110a0.png)

    12. `(?=(?:(?:[^"]*"){2})[^"]*)"(?=[^"]* )[^"]+"` : 從上述樣式中，加上條件 `(?=[^"]* )` 在兩個引號之間，希望能選到中間至少包含一個空格的字串，但是結果卻選到另外一群.....

        ![](https://screenshotscdn.firefoxusercontent.com/images/45e9a868-c7bd-457a-82d0-ec891e0121bd.png)



    13. `(?=(?:(?:[^"]*"){2}){6}[^"]*)"(?=[^"]* )[^"]+"` : 之所以出現上述問題，是因為預設總是從前面開始搜尋樣式，一有符合的就挑出來，但有可能因為前面沒有符合樣式的字串，就跳過一個雙引號，直接跟下一個雙引號match，結果就抓錯了...。

        為了解決這個問題，先把第一組改成符合的字串，然後在 `(?:(?:[^"]*"){2})` 這個樣式後面接上一個重複出現次數`{6}`，表示必須重複出現該樣式6次才會被選取。可以看到符合的只有第一組雙引號括起來的字串：

        ![](https://screenshotscdn.firefoxusercontent.com/images/a80ace25-8099-4064-8331-7df5da4da706.png)

        如果改成 `{5}`，就會出現兩組符合的情況，這是因為我們只算重複次數，並沒有算到哪裡結束。所以第一組本身最多可重複6次，但這裡只算了5次，後面還有一次才會遇到文章結尾；但第二組是最多就只能重複5次，然後就到文章結尾了。

        ![](https://screenshotscdn.firefoxusercontent.com/images/2cdc4b3d-1361-4c67-af83-f0d5a7c952f1.png)


    14. `(?=(?:(?:[^"]*"){2}){5}[^"]*$)"(?=[^"]* )[^"]+"` : 因此，藉由在 `(?:(?:[^"]*"){2}){5}[^"]*` 後面接上 `$` ，表示符合的樣式後面必須接上文章結尾，來限制第一組被選中的情況，如此就可以只選出第二組。

        ![](https://screenshotscdn.firefoxusercontent.com/images/7185d5b0-8ce5-4ee5-876d-b2e6eec7ed37.png)

        依此類推，改成`{4}` 可以選出第三組:

        ![](https://screenshotscdn.firefoxusercontent.com/images/fa16d3a9-06fd-40e2-8ea2-0edf0b8f2d3c.png)

        改成`{3}`，可以發現到第四組時，並沒有被選中，這是因為第四組沒有符合 `(?=[^"]* )` 此必須要出現多個非`"` 字串接一個空格的條件，由此可知，他是真的只會去match 雙引號之間我們要的字串:
        ![](https://screenshotscdn.firefoxusercontent.com/images/6dd26316-93dc-47e5-8dd2-c1470bf2bda7.png)

        改成`{2}`，倒數第二組:

        ![](https://screenshotscdn.firefoxusercontent.com/images/326907e8-d15c-4e9e-8222-7e29eeb21fc3.png)

        改成`{1}`，倒數第一組:

        ![](https://screenshotscdn.firefoxusercontent.com/images/f0c16d5c-0c39-4647-a42e-6bc9cbefa1c2.png)

        切記，文章任何地方都不能有不成對的雙引號出現，否則就會選錯：
        ![](https://screenshotscdn.firefoxusercontent.com/images/8e88f43b-f554-420d-b654-0ef0da764eb6.png)


    14. `(?=(?:(?:[^"]*"){2})*[^"]*$)"(?=[^"]* )[^"]+"` : 如果想要一次選取所有組，只要把上述的 `{N}` 重複次數改成 `*` 符合重複0到多次，

        ![](https://screenshotscdn.firefoxusercontent.com/images/40bf9566-96f9-4e64-910f-5a05de6f4b55.png)
        


