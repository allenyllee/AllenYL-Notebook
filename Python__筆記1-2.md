# Python__筆記1-2

[toc]
<!-- toc --> 


# Exception Handling

## print Exception

- [How to print an error in Python? - Stack Overflow](https://stackoverflow.com/questions/1483429/how-to-print-an-error-in-python)

    > For Python 2.6 and later and Python 3.x:
    > 
    > ```python
    > except Exception as e: print(e)
    > ```
    > 
    > For Python 2.5 and earlier, use:
    > 
    > ```python
    > except Exception,e: print str(e)
    > ```

## Built-in Exceptions

- [Built-in Exceptions — Python 3.7.1 documentation](https://docs.python.org/3/library/exceptions.html#bltin-exceptions)

    > ```
    > BaseException
    >  +-- SystemExit
    >  +-- KeyboardInterrupt
    >  +-- GeneratorExit
    >  +-- Exception
    >       +-- StopIteration
    >       +-- StopAsyncIteration
    >       +-- ArithmeticError
    >       |    +-- FloatingPointError
    >       |    +-- OverflowError
    >       |    +-- ZeroDivisionError
    >       +-- AssertionError
    >       +-- AttributeError
    >       +-- BufferError
    >       +-- EOFError
    >       +-- ImportError
    >       |    +-- ModuleNotFoundError
    >       +-- LookupError
    >       |    +-- IndexError
    >       |    +-- KeyError
    >       +-- MemoryError
    >       +-- NameError
    >       |    +-- UnboundLocalError
    >       +-- OSError
    >       |    +-- BlockingIOError
    >       |    +-- ChildProcessError
    >       |    +-- ConnectionError
    >       |    |    +-- BrokenPipeError
    >       |    |    +-- ConnectionAbortedError
    >       |    |    +-- ConnectionRefusedError
    >       |    |    +-- ConnectionResetError
    >       |    +-- FileExistsError
    >       |    +-- FileNotFoundError
    >       |    +-- InterruptedError
    >       |    +-- IsADirectoryError
    >       |    +-- NotADirectoryError
    >       |    +-- PermissionError
    >       |    +-- ProcessLookupError
    >       |    +-- TimeoutError
    >       +-- ReferenceError
    >       +-- RuntimeError
    >       |    +-- NotImplementedError
    >       |    +-- RecursionError
    >       +-- SyntaxError
    >       |    +-- IndentationError
    >       |         +-- TabError
    >       +-- SystemError
    >       +-- TypeError
    >       +-- ValueError
    >       |    +-- UnicodeError
    >       |         +-- UnicodeDecodeError
    >       |         +-- UnicodeEncodeError
    >       |         +-- UnicodeTranslateError
    >       +-- Warning
    >            +-- DeprecationWarning
    >            +-- PendingDeprecationWarning
    >            +-- RuntimeWarning
    >            +-- SyntaxWarning
    >            +-- UserWarning
    >            +-- FutureWarning
    >            +-- ImportWarning
    >            +-- UnicodeWarning
    >            +-- BytesWarning
    >            +-- ResourceWarning
    > ```

### KeyError

- [Python Exception Handling - KeyError](https://airbrake.io/blog/python-exception-handling/python-keyerror)

    > the **KeyError**, which is the close sibling of the [`IndexError`](https://airbrake.io/blog/python-exception-handling/python-indexerror) we looked at last week. Whereas the [`IndexError`](https://airbrake.io/blog/python-exception-handling/python-indexerror) is raised when trying to access an invalid `index` within a `list`, the `KeyError` is raised when accessing an invalid `key` within a `dict`.


- [Catch KeyError in Python - Stack Overflow](https://stackoverflow.com/questions/16154032/catch-keyerror-in-python)


    > I am using Python 3.6 and using a comma between Exception and e does not work. I need to use the following syntax (just for anyone wondering)
    > 
    > ```python
    > try:
    >     connection = manager.connect("I2Cx")
    > except KeyError as e:
    >     print(e.message)
    > ```
    > 

### ZeroDivisionError

- [Python Exception Handling - ZeroDivisionError](https://airbrake.io/blog/python-exception-handling/zerodivisionerror-2)

    > the **ZeroDivisionError**. As you may suspect, the `ZeroDivisionError` in Python indicates that the second argument used in a division (or modulo) operation was zero.

- [python - Make division by zero equal to zero - Stack Overflow](https://stackoverflow.com/questions/27317517/make-division-by-zero-equal-to-zero)

    > You can use a `try`/`except` block for this.
    > 
    > ```python
    > def foo(x,y):
    >     try:
    >         return x/y
    >     except ZeroDivisionError:
    >         return 0
    > ```
    > 


# Regular Expresion(re)

- [6.2. re — Regular expression operations — Python 3.3.7 documentation](https://docs.python.org/3.3/library/re.html?highlight=re#re.compile)
    - __re.compile(_pattern_, _flags=0_)[](https://docs.python.org/3.3/library/re.html?highlight=re#re.compile "Permalink to this definition")__
        Compile a regular expression pattern into a regular expression object, which can be used for matching using its [match()](https://docs.python.org/3.3/library/re.html?highlight=re#re.match "re.match") and [search()](https://docs.python.org/3.3/library/re.html?highlight=re#re.search "re.search") methods, described below.


- [[Python] 正規表示法 Regular Expression](https://zwindr.blogspot.com/2016/01/python-regular-expression.html)

    > **re.split(pattern, string, maxsplit=0, flags=0)**
    > ```py
    > import re
    > # >> ['ab', 'cd', 'd']
    > match = re.split(r'\d',  'ab2cd5d')
    > ```


## line continuation with a long regex

- [Python: How do I do line continuation with a long regex? - Stack Overflow](https://stackoverflow.com/questions/33211404/python-how-do-i-do-line-continuation-with-a-long-regex)

    > If you use the `re.VERBOSE` flag, you can split your regular expression up as much as you like to make it more readable:
    > 
    > ```py
    > pattern = r"""
    >     \d\s+
    >     \d+\s+
    >     ([A-Z0-9-]+)\s+
    >     ([0-9]+.\d\(\d\)[A-Z0-9]+)\s+
    >     ([a-zA-Z\d-]+)"""
    > 
    > REGEX = re.compile(pattern, re.VERBOSE)
    > ```
    > 
    > This approach is explained in [Dive Into Python - Verbose Regular Expressions](http://www.diveintopython.net/regular_expressions/verbose.html).

## re.compile

- [re — Regular expression operations — Python 3.7.1 documentation](https://docs.python.org/3/library/re.html#re.compile)

    > Compile a regular expression pattern into a [regular expression object](https://docs.python.org/3/library/re.html#re-objects), which can be used for matching using its [`match()`](https://docs.python.org/3/library/re.html#re.Pattern.match "re.Pattern.match"), [`search()`](https://docs.python.org/3/library/re.html#re.Pattern.search "re.Pattern.search") and other methods, described below.
    > 
    > The expression's behaviour can be modified by specifying a *flags* value. Values can be any of the following variables, combined using bitwise OR (the `|` operator).
    > 
    > The sequence
    > ```
    > prog = re.compile(pattern)
    > result = prog.match(string)
    > ```
    > is equivalent to
    > ```
    > result = re.match(pattern, string)
    > ```
    > but using [`re.compile()`](https://docs.python.org/3/library/re.html#re.compile "re.compile") and saving the resulting regular expression object for reuse is more efficient when the expression will be used several times in a single program.
    > 
    > Note
    > 
    > The compiled versions of the most recent patterns passed to [`re.compile()`](https://docs.python.org/3/library/re.html#re.compile "re.compile") and the module-level matching functions are cached, so programs that use only a few regular expressions at a time needn't worry about compiling regular expressions.

## search() vs. match()

- [re — Regular expression operations — Python 3.7.1 documentation](https://docs.python.org/3/library/re.html#search-vs-match)

    > Python offers two different primitive operations based on regular expressions: [`re.match()`](https://docs.python.org/3/library/re.html#re.match "re.match") checks for a match only at the beginning of the string, while [`re.search()`](https://docs.python.org/3/library/re.html#re.search "re.search") checks for a match anywhere in the string (this is what Perl does by default).
    > 
    > For example:
    > 
    > 
    > ```
    > >>> re.match("c", "abcdef")    # No match
    > >>> re.search("c", "abcdef")   # Match
    > <re.Match object; span=(2, 3), match='c'>
    > ```
    > Regular expressions beginning with `'^'` can be used with [`search()`](https://docs.python.org/3/library/re.html#re.search "re.search") to restrict the match at the beginning of the string:
    > 
    > 
    > ```
    > >>> re.match("c", "abcdef")    # No match
    > >>> re.search("^c", "abcdef")  # No match
    > >>> re.search("^a", "abcdef")  # Match
    > <re.Match object; span=(0, 1), match='a'>
    > ```
    > Note however that in [`MULTILINE`](https://docs.python.org/3/library/re.html#re.MULTILINE "re.MULTILINE") mode [`match()`](https://docs.python.org/3/library/re.html#re.match "re.match") only matches at the beginning of the string, whereas using [`search()`](https://docs.python.org/3/library/re.html#re.search "re.search") with a regular expression beginning with `'^'` will match at the beginning of each line.
    > 
    > 
    > ```
    > >>> re.match('X', 'A\nB\nX', re.MULTILINE)  # No match
    > >>> re.search('^X', 'A\nB\nX', re.MULTILINE)  # Match
    > <re.Match object; span=(4, 5), match='X'>
    > ```





# functions/passing varibles/return/yield/Generator/lambda



## how to passed by reference

- [python - How do I pass a variable by reference? - Stack Overflow](https://stackoverflow.com/questions/986006/how-do-i-pass-a-variable-by-reference)

    > Arguments are [passed by assignment](http://docs.python.org/3/faq/programming.html#how-do-i-write-a-function-with-output-parameters-call-by-reference). The rationale behind this is twofold:
    > 
    > 1.  the parameter passed in is actually a *reference* to an object (but the reference is passed by value)
    > 2.  some data types are mutable, but others aren't
    > 
    > So:
    > 
    > -   If you pass a *mutable* object into a method, the method gets a reference to that same object and you can mutate it to your heart's delight, but if you rebind the reference in the method, the outer scope will know nothing about it, and after you're done, the outer reference will still point at the original object.
    > 
    > -   If you pass an *immutable* object to a method, you still can't rebind the outer reference, and you can't even mutate the object.
    > 
    > ---
    > 
    > How do we get around this?
    > --------------------------
    > 
    > As @Andrea's answer shows, you could return the new value. This doesn't change the way things are passed in, but does let you get the information you want back out:
    > 
    > ```
    > def return_a_whole_new_string(the_string):
    >     new_string = something_to_do_with_the_old_string(the_string)
    >     return new_string
    > 
    > # then you could call it like
    > my_string = return_a_whole_new_string(my_string)
    > ```
    > 
    > If you really wanted to avoid using a return value, you could create a class to hold your value and pass it into the function or use an existing class, like a list:
    > 
    > ```
    > def use_a_wrapper_to_simulate_pass_by_reference(stuff_to_change):
    >     new_string = something_to_do_with_the_old_string(stuff_to_change[0])
    >     stuff_to_change[0] = new_string
    > 
    > # then you could call it like
    > wrapper = [my_string]
    > use_a_wrapper_to_simulate_pass_by_reference(wrapper)
    > 
    > do_something_with(wrapper[0])
    > ```


## yield & Generator

- [python yield 語法與 generator 物件介紹 - 程式的窩](http://blog.blackwhite.tw/2013/05/python-yield-generator.html)

    事實上，yield 和 return 很像，只是當函數呼叫 return 時，該函數 call stack (python 中是 frame) 就會被清除，程式主導權回到呼叫該函數的手上。 而 yield 會把程式主導權交給呼叫該函數的手上，但是他不會把函數的 call stack 清除，因此下次呼叫時，可以從上次未執行的部分開始執行，而不是重新建立一個新 stack。  

    ```python
    def return_fun():
        a = 1
        b = 1
        return a

    print return_fun()
    print return_fun()
    ```

    上面這段程式碼，每次呼叫 return_fun 時，都是從 a = 1 開始執行，然後遇到 return 就結束了。所以執行流程像這樣  


    [![](http://2.bp.blogspot.com/-4xhZATG4L40/UYSkX4r6ulI/AAAAAAAAG1E/vNnwf0yRWTE/s1600/function+flow.png)](http://2.bp.blogspot.com/-4xhZATG4L40/UYSkX4r6ulI/AAAAAAAAG1E/vNnwf0yRWTE/s1600/function+flow.png)

    當有函數裡面有用到 yield 這個關鍵字時，事情就變得很不一樣了。  


    ```python
    def yield_fun():
        a = 1
        b = 1
        yield a
    ```

    ```python
        yield b

    print yield_fun()
    ```

    當你執行上面這段程式碼時，你會發現他回傳給你的居然是 generator 物件。那要怎麼執行 yield_fun 裡面的 code 呢? 答案是使用 generator 的 next 方法。  


    ```python
    def yield_fun():
        a = 3
        b = 2
        yield a
        c = 4
        yield b

    generator = yield_fun()
    print generator.next()
    print generator.next()
    ```

    當使用者第一次呼叫 generator 的  next 方法時，他會從 a = 3 開始執行，直到遇到 yield。python 會回傳 yield 後面接的東西(就像 return )，之後再把現在的 call stack( python 中是 frame)，儲存在 generator 的 gi_frame 屬性中。  

    當使用者第二次呼叫 generator 的  next 方法時，他不會建立一個新的 call stack，而是從  generator 的 gi_frame 屬性中取出之前的 call stack。因此，程式會從 c = 4 開始執行(不是從 a = 3喔，如果是 function 的話，是從 a = 3 開始執行)。直到遇到 yield 或是 return 為止。遇到 yield 表示下次還可以再呼叫一次 next 方法。遇到 return 則表示 這個 generator 已經沒東西了。無法再呼叫 next 了。執行流程像這樣。  


    [![](http://1.bp.blogspot.com/-BaSDSFqkAYQ/UYSqFQbDXlI/AAAAAAAAG1U/wBQg_tugBfE/s1600/yield+function.png)](http://1.bp.blogspot.com/-BaSDSFqkAYQ/UYSqFQbDXlI/AAAAAAAAG1U/wBQg_tugBfE/s1600/yield+function.png)

    事實上， yield 除了可以把資料回傳給呼叫者外，他也可以從呼叫者接受資料。向下面的程式碼。  



    ```python
    def yield_fun():
        a = 3
        b = 2

        b = yield a
        yield b


    generator = yield_fun()
    print generator.next()
    print generator.send(8)
    ```

    上面這段程式碼， yield 除了把 a 的值回傳給呼叫者外，他還會從呼叫者那邊接受一個值，把 b 的值指派成呼叫者給的參數。  

    generator 打破函數執行完後， call stack 就會被清除的限制(因為 generator 把 call stack 存在 gi_frame 屬性，所以下次執行時，還知道之前的狀態)。


- [python - What does the "yield" keyword do? - Stack Overflow](https://stackoverflow.com/questions/231767/what-does-the-yield-keyword-do?page=1&tab=active#tab-top)

    > To understand what `yield` does, you must understand what _generators_ are. And before generators come _iterables_.
    > 
    > Iterables
    > ---------
    > 
    > When you create a list, you can read its items one by one. Reading its items one by one is called iteration:
    > 
    > ```python
    > >>> mylist = [1, 2, 3]
    > >>> for i in mylist:
    > ...    print(i)
    > 1
    > 2
    > 3
    > ```
    > 
    > `mylist` is an _iterable_. When you use a list comprehension, you create a list, and so an iterable:
    > 
    > ```python
    > >>> mylist = [x*x for x in range(3)]
    > >>> for i in mylist:
    > ...    print(i)
    > 0
    > 1
    > 4
    > ```
    > 
    > Everything you can use "`for... in...`" on is an iterable; `lists`, `strings`, files...
    > 
    > These iterables are handy because you can read them as much as you wish, but you store all the values in memory and this is not always what you want when you have a lot of values.
    > 
    > Generators
    > ----------
    > 
    > Generators are iterators, a kind of iterable **you can only iterate over once**. Generators do not store all the values in memory, **they generate the values on the fly**:
    > 
    > ```python
    > >>> mygenerator = (x*x for x in range(3))
    > >>> for i in mygenerator:
    > ...    print(i)
    > 0
    > 1
    > 4
    > ```
    > 
    > It is just the same except you used `()` instead of `[]`. BUT, you **cannot** perform `for i in mygenerator` a second time since generators can only be used once: they calculate 0, then forget about it and calculate 1, and end calculating 4, one by one.
    > 
    > Yield
    > -----
    > 
    > `yield` is a keyword that is used like `return`, except the function will return a generator.
    > 
    > ```python
    > >>> def createGenerator():
    > ...    mylist = range(3)
    > ...    for i in mylist:
    > ...        yield i*i
    > ...
    > >>> mygenerator = createGenerator() # create a generator
    > >>> print(mygenerator) # mygenerator is an object!
    > <generator object createGenerator at 0xb7555c34>
    > >>> for i in mygenerator:
    > ...     print(i)
    > 0
    > 1
    > 4
    > ```
    > 
    > Here it's a useless example, but it's handy when you know your function will return a huge set of values that you will only need to read once.
    > 
    > To master `yield`, you must understand that **when you call the function, the code you have written in the function body does not run.** The function only returns the generator object, this is a bit tricky :-)
    > 
    > Then, your code will be run each time the `for` uses the generator.
    > 
    > Now the hard part:
    > 
    > The first time the `for` calls the generator object created from your function, it will run the code in your function from the beginning until it hits `yield`, then it'll return the first value of the loop. Then, each other call will run the loop you have written in the function one more time, and return the next value, until there is no value to return.
    > 
    > The generator is considered empty once the function runs but does not hit `yield` anymore. It can be because the loop had come to an end, or because you do not satisfy an `"if/else"` anymore.
    > 
    > ---
    > 
    > Your code explained
    > -------------------
    > 
    > Generator:
    > 
    > ```python
    > # Here you create the method of the node object that will return the generator
    > def _get_child_candidates(self, distance, min_dist, max_dist):
    > 
    >     # Here is the code that will be called each time you use the generator object:
    > 
    >     # If there is still a child of the node object on its left
    >     # AND if distance is ok, return the next child
    >     if self._leftchild and distance - max_dist < self._median:
    >         yield self._leftchild
    > 
    >     # If there is still a child of the node object on its right
    >     # AND if distance is ok, return the next child
    >     if self._rightchild and distance + max_dist >= self._median:
    >         yield self._rightchild
    > 
    >     # If the function arrives here, the generator will be considered empty
    >     # there is no more than two values: the left and the right children
    > ```
    > 
    > Caller:
    > 
    > ```python
    > # Create an empty list and a list with the current object reference
    > result, candidates = list(), [self]
    > 
    > # Loop on candidates (they contain only one element at the beginning)
    > while candidates:
    > 
    >     # Get the last candidate and remove it from the list
    >     node = candidates.pop()
    > 
    >     # Get the distance between obj and the candidate
    >     distance = node._get_dist(obj)
    > 
    >     # If distance is ok, then you can fill the result
    >     if distance <= max_dist and distance >= min_dist:
    >         result.extend(node._values)
    > 
    >     # Add the children of the candidate in the candidates list
    >     # so the loop will keep running until it will have looked
    >     # at all the children of the children of the children, etc. of the candidate
    >     candidates.extend(node._get_child_candidates(distance, min_dist, max_dist))
    > 
    > return result
    > ```
    > 
    > This code contains several smart parts:
    > 
    > -   The loop iterates on a list but the list expands while the loop is being iterated :-) It's a concise way to go through all these nested data even if it's a bit dangerous since you can end up with an infinite loop. In this case, `candidates.extend(node._get_child_candidates(distance, min_dist, max_dist))` exhausts all the values of the generator, but `while` keeps creating new generator objects which will produce different values from the previous ones since it's not applied on the same node.
    >     
    > -   The `extend()` method is a list object method that expects an iterable and adds its values to the list.
    >     
    > 
    > Usually we pass a list to it:
    > 
    > ```python
    > >>> a = [1, 2]
    > >>> b = [3, 4]
    > >>> a.extend(b)
    > >>> print(a)
    > [1, 2, 3, 4]
    > ```
    > 
    > But in your code it gets a generator, which is good because:
    > 
    > 1.  You don't need to read the values twice.
    > 2.  You may have a lot of children and you don't want them all stored in memory.
    > 
    > And it works because Python does not care if the argument of a method is a list or not. Python expects iterables so it will work with strings, lists, tuples and generators! This is called duck typing and is one of the reason why Python is so cool. But this is another story, for another question...
    > 
    > You can stop here, or read a little bit to see an advanced use of a generator:
    > 
    > Controlling a generator exhaustion
    > ----------------------------------
    > 
    > ```python
    > >>> class Bank(): # let's create a bank, building ATMs
    > ...    crisis = False
    > ...    def create_atm(self):
    > ...        while not self.crisis:
    > ...            yield "$100"
    > >>> hsbc = Bank() # when everything's ok the ATM gives you as much as you want
    > >>> corner_street_atm = hsbc.create_atm()
    > >>> print(corner_street_atm.next())
    > $100
    > >>> print(corner_street_atm.next())
    > $100
    > >>> print([corner_street_atm.next() for cash in range(5)])
    > ['$100', '$100', '$100', '$100', '$100']
    > >>> hsbc.crisis = True # crisis is coming, no more money!
    > >>> print(corner_street_atm.next())
    > <type 'exceptions.StopIteration'>
    > >>> wall_street_atm = hsbc.create_atm() # it's even true for new ATMs
    > >>> print(wall_street_atm.next())
    > <type 'exceptions.StopIteration'>
    > >>> hsbc.crisis = False # trouble is, even post-crisis the ATM remains empty
    > >>> print(corner_street_atm.next())
    > <type 'exceptions.StopIteration'>
    > >>> brand_new_atm = hsbc.create_atm() # build a new one to get back in business
    > >>> for cash in brand_new_atm:
    > ...    print cash
    > $100
    > $100
    > $100
    > $100
    > $100
    > $100
    > $100
    > $100
    > $100
    > ...
    > ```
    > 
    > **Note:** For Python3 use`print(corner_street_atm.__next__())` or `print(next(corner_street_atm))`
    > 
    > It can be useful for various things like controlling access to a resource.
    > 
    > Itertools, your best friend
    > ---------------------------
    > 
    > The itertools module contains special functions to manipulate iterables. Ever wish to duplicate a generator? Chain two generators? Group values in a nested list with a one liner? `Map / Zip` without creating another list?
    > 
    > Then just `import itertools`.
    > 
    > An example? Let's see the possible orders of arrival for a 4 horse race:
    > 
    > ```python
    > >>> horses = [1, 2, 3, 4]
    > >>> races = itertools.permutations(horses)
    > >>> print(races)
    > <itertools.permutations object at 0xb754f1dc>
    > >>> print(list(itertools.permutations(horses)))
    > [(1, 2, 3, 4),
    >  (1, 2, 4, 3),
    >  (1, 3, 2, 4),
    >  (1, 3, 4, 2),
    >  (1, 4, 2, 3),
    >  (1, 4, 3, 2),
    >  (2, 1, 3, 4),
    >  (2, 1, 4, 3),
    >  (2, 3, 1, 4),
    >  (2, 3, 4, 1),
    >  (2, 4, 1, 3),
    >  (2, 4, 3, 1),
    >  (3, 1, 2, 4),
    >  (3, 1, 4, 2),
    >  (3, 2, 1, 4),
    >  (3, 2, 4, 1),
    >  (3, 4, 1, 2),
    >  (3, 4, 2, 1),
    >  (4, 1, 2, 3),
    >  (4, 1, 3, 2),
    >  (4, 2, 1, 3),
    >  (4, 2, 3, 1),
    >  (4, 3, 1, 2),
    >  (4, 3, 2, 1)]
    > ```
    > 
    > Understanding the inner mechanisms of iteration
    > -----------------------------------------------
    > 
    > Iteration is a process implying iterables (implementing the `__iter__()` method) and iterators (implementing the `__next__()` method). Iterables are any objects you can get an iterator from. Iterators are objects that let you iterate on iterables.
    > 
    > More about it in this article about [how does the for loop work](http://effbot.org/zone/python-for-statement.htm).
    > 

## yield, next(), iter()

- [生成器(Generators) · Python进阶](https://eastlakeside.gitbooks.io/interpy-zh/content/Generators/Generators.html)

    > 下面是一个计算斐波那契数列的生成器：
    > 
    > ```python
    > # generator version
    > def fibon(n):
    >     a = b = 1
    >     for i in range(n):
    >         yield a
    >         a, b = b, a + b
    > 
    > ```
    > 
    > 函数使用方法如下：
    > 
    > ```python
    > for x in fibon(1000000):
    >     print(x)
    > 
    > ```
    > 
    > 用这种方式，我们可以不用担心它会使用大量资源。然而，之前如果我们这样来实现的话：
    > 
    > ```python
    > def fibon(n):
    >     a = b = 1
    >     result = []
    >     for i in range(n):
    >         result.append(a)
    >         a, b = b, a + b
    >     return result
    > 
    > ```
    > 
    > 这也许会在计算很大的输入参数时，用尽所有的资源。我们已经讨论过生成器使用一次迭代，但我们并没有测试过。在测试前你需要再知道一个Python内置函数：`next()`。它允许我们获取一个序列的下一个元素。那我们来验证下我们的理解：
    > 
    > ```python
    > def generator_function():
    >     for i in range(3):
    >         yield i
    > 
    > gen = generator_function()
    > print(next(gen))
    > # Output: 0
    > print(next(gen))
    > # Output: 1
    > print(next(gen))
    > # Output: 2
    > print(next(gen))
    > # Output: Traceback (most recent call last):
    > #            File "<stdin>", line 1, in <module>
    > #         StopIteration
    > 
    > ```
    > 
    > 我们可以看到，在`yield`掉所有的值后，`next()`触发了一个`StopIteration`的异常。基本上这个异常告诉我们，所有的值都已经被`yield`完了。你也许会奇怪，为什么我们在使用`for`循环时没有这个异常呢？啊哈，答案很简单。`for`循环会自动捕捉到这个异常并停止调用`next()`。你知不知道Python中一些内置数据类型也支持迭代哦？我们这就去看看：
    > 
    > ```python
    > my_string = "Yasoob"
    > next(my_string)
    > # Output: Traceback (most recent call last):
    > #      File "<stdin>", line 1, in <module>
    > #    TypeError: str object is not an iterator
    > 
    > ```
    > 
    > 好吧，这不是我们预期的。这个异常说那个`str`对象不是一个迭代器。对，就是这样！它是一个可迭代对象，而不是一个迭代器。这意味着它支持迭代，但我们不能直接对其进行迭代操作。那我们怎样才能对它实施迭代呢？是时候学习下另一个内置函数，`iter`。它将根据一个可迭代对象返回一个迭代器对象。这里是我们如何使用它：
    > 
    > ```python
    > my_string = "Yasoob"
    > my_iter = iter(my_string)
    > next(my_iter)
    > # Output: 'Y'
    > 
    > ```
    > 
    > 现在好多啦。我肯定你已经爱上了学习生成器。一定要记住，想要完全掌握这个概念，你只有使用它。确保你按照这个模式，并在生成器对你有意义的任何时候都使用它。你绝对不会失望的！


## get one value from a generator

- [How to get one value from a generator in Python? - Stack Overflow](https://stackoverflow.com/questions/2419770/how-to-get-one-value-from-a-generator-in-python)

    > In Python <= 2.5, use `gen.next()`. This will work for all Python 2.x versions, but not Python 3.x
    > 
    > In Python >= 2.6, use `next(gen)`. This is a built in function, and is clearer. It will also work in Python 3.
    > 
    > Both of these end up calling a specially named function, `next()`, which can be overridden by subclassing. In Python 3, however, this function has been renamed to `__next__()`, to be consistent with other special functions.



## Passing a function into another function

- [Python - Passing a function into another function - Stack Overflow](https://stackoverflow.com/questions/1349332/python-passing-a-function-into-another-function)

    > Just pass it in like any other parameter:
    > 
    > ```python
    > def a(x):
    >     return "a(%s)" % (x,)
    > 
    > def b(f,x):
    >     return f(x)
    > 
    > print b(a,10)
    > ```
    > 

## pass a default argument value of an instance member(self.xxx) to a method (def abc(self, format=self.xxx))

- [python - How to pass a default argument value of an instance member to a method? - Stack Overflow](https://stackoverflow.com/questions/8131942/how-to-pass-a-default-argument-value-of-an-instance-member-to-a-method/8131960)

    > You can't really define this as the default value, since the default value is evaluated when the method is defined which is before any instances exist. An easy work-around is to do something like this:
    > 
    > ```python
    > class C:
    >     def __init__(self, format):
    >         self.format = format
    > 
    >     def process(self, formatting=None):
    >         formatting = formatting if formatting is not None else self.format
    >         print(formatting)
    > ```
    > 
    > `self.format` will only be used if `formatting` is `None`.
    > 
    > * * * * *
    > 
    > To demonstrate the point of how default values work, see this example:
    > 
    > ```python
    > def mk_default():
    >     print("mk_default has been called!")
    > 
    > def myfun(foo=mk_default()):
    >     print("myfun has been called.")
    > 
    > print("about to test functions")
    > myfun("testing")
    > myfun("testing again")
    > ```
    > 
    > And the output here:
    > 
    > ```python
    > mk_default has been called!
    > about to test functions
    > myfun has been called.
    > myfun has been called.
    > ```
    > 
    > Notice how `mk_default` was called only once, and that happened before the function was ever called!
    > 
    > ---
    > 
    > In Python, the name `self` is **not** special. It's just a convention for the parameter name, which is why there is a `self` parameter in `__init__`. (Actually, `__init__` is not very special either, and in particular it does **not** actually create the object... that's a longer story)
    > 
    > `C("abc").process()` creates a `C` instance, looks up the `process` method in the `C` class, and calls that method with the `C` instance as the first parameter. So it will end up in the `self` parameter if you provided it.
    > 
    > Even if you had that parameter, though, you would not be allowed to write something like `def process(self, formatting = self.formatting)`, because `self` is not in scope yet at the point where you set the default value. In Python, the default value for a parameter is calculated when the function is compiled, and "stuck" to the function. (This is the same reason why, if you use a default like `[]`, that list will remember changes between calls to the function.)
    > 
    > > How could I make this work?
    > 
    > The traditional way is to use `None` as a default, and check for that value and replace it inside the function. You may find it is a little safer to make a special value for the purpose (an `object` instance is all you need, as long as you hide it so that the calling code does not use the same instance) instead of `None`. Either way, you should check for this value with `is`, not `==`.
    > 

## pass self to referenced function (functools.partial)

- [python pass self to referenced function - Stack Overflow](https://stackoverflow.com/questions/32319027/python-pass-self-to-referenced-function)


    > The problem is that you assigned myFoo to an unbound function and are calling it as though it were bound. If you want to be able to use `self.myFoo()` you will need to curry the object into the first arg yourself.
    > 
    > ```python
    > from functools import partial
    > 
    > def foo(self):
    >     print(self.toString())
    > 
    > class Node:
    >     def __init__(self, myFoo):
    >         self.myFoo = partial(myFoo, self)
    > 
    >     def run(self):
    >         self.myFoo()
    > 
    >     def toString(self):
    >         return "Hello World"
    > 
    > n = Node(foo)
    > n.run()
    > ```
    > 
    > Alternatively you could use
    > 
    > ```python
    > self.myFoo = types.MethodType(myFoo, self)
    > ```
    > 
    > in your `__init__(self, myFoo)` method, but using partial is more commonly done, and more versatile since you can use it to curry arguments for any sort of function, not just methods.
    > 

- [partial 函数 · Python 之旅](http://funhacks.net/explore-python/Functional/partial.html)

    > Python 提供了一个 functools 的模块，该模块为高阶函数提供支持，partial 就是其中的一个函数，该函数的形式如下：
    > 
    > ```python
    > functools.partial(func[,*args][, **kwargs])
    > 
    > ```
    > 
    > 这里先举个例子，看看它是怎么用的。
    > 
    > 假设有如下函数：
    > 
    > ```python
    > def multiply(x, y):
    >     return x * y
    > 
    > ```
    > 
    > 现在，我们想返回某个数的双倍，即：
    > 
    > ```python
    > >>> multiply(3, y=2)
    > 6
    > >>> multiply(4, y=2)
    > 8
    > >>> multiply(5, y=2)
    > 10
    > 
    > ```
    > 
    > 上面的调用有点繁琐，每次都要传入 `y=2`，我们想到可以定义一个新的函数，把 `y=2` 作为默认值，即：
    > 
    > ```python
    > def double(x, y=2):
    >     return multiply(x, y)
    > 
    > ```
    > 
    > 现在，我们可以这样调用了：
    > 
    > ```python
    > >>> double(3)
    > 6
    > >>> double(4)
    > 8
    > >>> double(5)
    > 10
    > 
    > ```
    > 
    > 事实上，我们可以不用自己定义 `double`，利用 `partial`，我们可以这样：
    > 
    > ```python
    > from functools import partial
    > 
    > double = partial(multiply, y=2)
    > 
    > ```
    > 
    > `partial` 接收函数 `multiply` 作为参数，固定 `multiply` 的参数 `y=2`，并返回一个新的函数给 `double`，这跟我们自己定义 `double` 函数的效果是一样的。
    > 
    > 所以，简单而言，`partial` 函数的功能就是：把一个函数的某些参数给固定住，返回一个新的函数。
    > 
    > 需要注意的是，我们上面是固定了 `multiply` 的关键字参数 `y=2`，如果直接使用：
    > 
    > ```python
    > double = partial(multiply, 2)
    > 
    > ```
    > 
    > 则 `2` 是赋给了 `multiply` 最左边的参数 `x`，不信？我们可以验证一下：
    > 
    > ```python
    > from functools import partial
    > 
    > def subtraction(x, y):
    >     return x - y
    > 
    > f = partial(subtraction, 4)  # 4 赋给了 x
    > >>> f(10)   # 4 - 10
    > -6
    > 
    > ```
    > 
    > 小结
    > ==
    > 
    > -   partial 的功能：固定函数参数，返回一个新的函数。
    > -   当函数参数太多，需要固定某些参数时，可以使用 `functools.partial` 创建一个新的函数。
    > 


# lambda/filter/reduce/map

- [4. Map, Filter and Reduce — Python Tips 0.1 documentation](http://book.pythontips.com/en/latest/map_filter.html)

## lambda

- [Is there a way to perform "if" in python's lambda - Stack Overflow](https://stackoverflow.com/questions/1585322/is-there-a-way-to-perform-if-in-pythons-lambda)

    > The syntax you're looking for:
    > 
    > ```python
    > lambda x: True if x % 2 == 0 else False
    > ```

## map()/reduce()

- [map/reduce - 廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/0014317852443934a86aa5bb5ea47fbbd5f35282b331335000)

    > Python内建了`map()`和`reduce()`函数。
    > 
    > 如果你读过Google的那篇大名鼎鼎的论文"[MapReduce: Simplified Data Processing on Large Clusters](http://research.google.com/archive/mapreduce.html)"，你就能大概明白map/reduce的概念。
    > 
    > 我们先看map。`map()`函数接收两个参数，一个是函数，一个是`Iterable`，`map`将传入的函数依次作用到序列的每个元素，并把结果作为新的`Iterator`返回。
    > 
    > 举例说明，比如我们有一个函数f(x)=x^2^，要把这个函数作用在一个list `[1, 2, 3, 4, 5, 6, 7, 8, 9]`上，就可以用`map()`实现如下：
    > 
    > ```
    >             f(x) = x * x
    > 
    >                   │
    >                   │
    >   ┌───┬───┬───┬───┼───┬───┬───┬───┐
    >   │   │   │   │   │   │   │   │   │
    >   ▼   ▼   ▼   ▼   ▼   ▼   ▼   ▼   ▼
    > 
    > [ 1   2   3   4   5   6   7   8   9 ]
    > 
    >   │   │   │   │   │   │   │   │   │
    >   │   │   │   │   │   │   │   │   │
    >   ▼   ▼   ▼   ▼   ▼   ▼   ▼   ▼   ▼
    > 
    > [ 1   4   9  16  25  36  49  64  81 ]
    > 
    > ```
    > 
    > 现在，我们用Python代码实现：
    > 
    > ```python
    > >>> def f(x):
    > ...     return x * x
    > ...
    > >>> r = map(f, [1, 2, 3, 4, 5, 6, 7, 8, 9])
    > >>> list(r)
    > [1, 4, 9, 16, 25, 36, 49, 64, 81]
    > 
    > ```
    > 
    > `map()`传入的第一个参数是`f`，即函数对象本身。由于结果`r`是一个`Iterator`，`Iterator`是惰性序列，因此通过`list()`函数让它把整个序列都计算出来并返回一个list。
    > 
    > 你可能会想，不需要`map()`函数，写一个循环，也可以计算出结果：
    > 
    > ```python
    > L = []
    > for n in [1, 2, 3, 4, 5, 6, 7, 8, 9]:
    >     L.append(f(n))
    > print(L)
    > 
    > ```
    > 
    > 的确可以，但是，从上面的循环代码，能一眼看明白"把f(x)作用在list的每一个元素并把结果生成一个新的list"吗？
    > 
    > 所以，`map()`作为高阶函数，事实上它把运算规则抽象了，因此，我们不但可以计算简单的f(x)=x^2^，还可以计算任意复杂的函数，比如，把这个list所有数字转为字符串：
    > 
    > ```python
    > >>> list(map(str, [1, 2, 3, 4, 5, 6, 7, 8, 9]))
    > ['1', '2', '3', '4', '5', '6', '7', '8', '9']
    > 
    > ```
    > 
    > 只需要一行代码。
    > 
    > 再看`reduce`的用法。`reduce`把一个函数作用在一个序列`[x1, x2, x3, ...]`上，这个函数必须接收两个参数，`reduce`把结果继续和序列的下一个元素做累积计算，其效果就是：
    > 
    > ```python
    > reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)
    > 
    > ```
    > 
    > 比方说对一个序列求和，就可以用`reduce`实现：
    > 
    > ```python
    > >>> from functools import reduce
    > >>> def add(x, y):
    > ...     return x + y
    > ...
    > >>> reduce(add, [1, 3, 5, 7, 9])
    > 25
    > 
    > ```
    > 
    > 当然求和运算可以直接用Python内建函数`sum()`，没必要动用`reduce`。
    > 
    > 但是如果要把序列`[1, 3, 5, 7, 9]`变换成整数`13579`，`reduce`就可以派上用场：
    > 
    > ```python
    > >>> from functools import reduce
    > >>> def fn(x, y):
    > ...     return x * 10 + y
    > ...
    > >>> reduce(fn, [1, 3, 5, 7, 9])
    > 13579
    > 
    > ```
    > 
    > 这个例子本身没多大用处，但是，如果考虑到字符串`str`也是一个序列，对上面的例子稍加改动，配合`map()`，我们就可以写出把`str`转换为`int`的函数：
    > 
    > ```python
    > >>> from functools import reduce
    > >>> def fn(x, y):
    > ...     return x * 10 + y
    > ...
    > >>> def char2num(s):
    > ...     digits = {'0': 0, '1': 1, '2': 2, '3': 3, '4': 4, '5': 5, '6': 6, '7': 7, '8': 8, '9': 9}
    > ...     return digits[s]
    > ...
    > >>> reduce(fn, map(char2num, '13579'))
    > 13579
    > 
    > ```
    > 
    > 整理成一个`str2int`的函数就是：
    > 
    > ```python
    > from functools import reduce
    > 
    > DIGITS = {'0': 0, '1': 1, '2': 2, '3': 3, '4': 4, '5': 5, '6': 6, '7': 7, '8': 8, '9': 9}
    > 
    > def str2int(s):
    >     def fn(x, y):
    >         return x * 10 + y
    >     def char2num(s):
    >         return DIGITS[s]
    >     return reduce(fn, map(char2num, s))
    > 
    > ```
    > 
    > 还可以用lambda函数进一步简化成：
    > 
    > ```python
    > from functools import reduce
    > 
    > DIGITS = {'0': 0, '1': 1, '2': 2, '3': 3, '4': 4, '5': 5, '6': 6, '7': 7, '8': 8, '9': 9}
    > 
    > def char2num(s):
    >     return DIGITS[s]
    > 
    > def str2int(s):
    >     return reduce(lambda x, y: x * 10 + y, map(char2num, s))
    > 
    > ```
    > 
    > 也就是说，假设Python没有提供`int()`函数，你完全可以自己写一个把字符串转化为整数的函数，而且只需要几行代码！
    > 
    > lambda函数的用法在后面介绍。




## reduce() 

- [Python reduce() 函数 | 菜鸟教程](http://www.runoob.com/python/python-func-reduce.html)

    > **reduce()** 函数会对参数序列中元素进行累积。
    > 
    > 函数将一个数据集合（链表，元组等）中的所有数据进行下列操作：用传给 reduce 中的函数 function（有两个参数）先对集合中的第 1、2 个元素进行操作，得到的结果再与第三个数据用 function 函数运算，最后得到一个结果。
    > 
    > ```python
    > >>>def add(x, y) :            # 两数相加
    > ...     return x + y
    > ... 
    > >>> reduce(add, [1,2,3,4,5])   # 计算列表和：1+2+3+4+5
    > 15
    > >>> reduce(lambda x, y: x+y, [1,2,3,4,5])  # 使用 lambda 匿名函数
    > 15
    > ```
    > ---
    > 
    > 在 Python3 中，reduce() 函数已经被从全局名字空间里移除了，它现在被放置在 functools 模块里，如果想要使用它，则需要通过引入 functools 模块来调用 reduce() 函数：
    > 
    > 
    > **实例：**
    > ```python
    > from functools import reduce
    > 
    > def add(x,y):
    >     return x + y
    > 
    > print (reduce(add, range(1, 101)))
    > ```

## filter()

- [4. Map, Filter and Reduce — Python Tips 0.1 documentation](http://book.pythontips.com/en/latest/map_filter.html)

    > As the name suggests, `filter` creates a list of elements for which a function returns true. Here is a short and concise example:
    > ```python
    > number_list = range(-5, 5)
    > less_than_zero = list(filter(lambda x: x < 0, number_list))
    > print(less_than_zero)
    > 
    > # Output: [-5, -4, -3, -2, -1]
    > ```
    > The filter resembles a for loop but it is a builtin function and faster.



# decorator

## assign function wrapper (@)

- [syntax - What does the "at" (@) symbol do in Python? - Stack Overflow](https://stackoverflow.com/questions/6392739/what-does-the-at-symbol-do-in-python)


    > > What does the "at" (@) symbol do in Python?
    > 
    > @ symbol is a syntactic sugar python provides to utilize `decorator`,\
    > to paraphrase the question, It's exactly about what does decorator do in Python?
    > 
    > Put it simple `decorator` allow you to modify a given function's definition without touch its innermost (it's closure).\
    > It's the most case when you import wonderful package from third party. You can visualize it, you can use it, but you cannot touch its innermost and its heart.
    > 
    > Here is a quick example,\
    > suppose I define a `read_a_book` function on Ipython
    > 
    > ```python
    > In [9]: def read_a_book():
    >    ...:     return "I am reading the book: "
    >    ...:
    > In [10]: read_a_book()
    > Out[10]: 'I am reading the book: '
    > ```
    > 
    > You see, I forgot to add a name to it.\
    > How to solve such a problem? Of course, I could re-define the function as:
    > 
    > ```python
    > def read_a_book():
    >     return "I am reading the book: 'Python Cookbook'"
    > ```
    > 
    > Nevertheless, what if I'm not allowed to manipulate the original function, or if there are thousands of such function to be handled.
    > 
    > Solve the problem by thinking different and define a new_function
    > 
    > ```python
    > def add_a_book(func):
    >     def wrapper():
    >         return func() + "Python Cookbook"
    >     return wrapper
    > ```
    > 
    > Then employ it.
    > 
    > ```python
    > In [14]: read_a_book = add_a_book(read_a_book)
    > In [15]: read_a_book()
    > Out[15]: 'I am reading the book: Python Cookbook'
    > ```
    > 
    > Tada, you see, I amended `read_a_book` without touching it inner closure. Nothing stops me equipped with `decorator`.
    > 
    > What's about `@`
    > 
    > ```python
    > @add_a_book
    > def read_a_book():
    >     return "I am reading the book: "
    > In [17]: read_a_book()
    > Out[17]: 'I am reading the book: Python Cookbook'
    > ```
    > 
    > `@add_a_book` is a fancy and handy way to say `read_a_book = add_a_book(read_a_book)`, it's a syntactic sugar, there's nothing more fancier about it.
    > 


# attribute

- [Python reserved attribute - LeetCode Playground](https://leetcode.com/playground/b76v2SoG)

    <iframe src="https://leetcode.com/playground/b76v2SoG/shared" frameBorder="0" width="400" height="300"></iframe>

## List attributes of an object

- [python - List attributes of an object - Stack Overflow](https://stackoverflow.com/questions/2675028/list-attributes-of-an-object)

    > All previous answers are correct, you have three options for what you are asking
    > 
    > 1.[dir()](https://docs.python.org/3/library/functions.html#dir "dir()")
    > 
    > 2.[vars()](https://docs.python.org/3/library/functions.html#vars)
    > 
    > 3.[__dict__](https://docs.python.org/3/library/stdtypes.html#object.__dict__ "__dict__")
    > 
    > ```python
    > >>> dir(a)
    > ['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'multi', 'str']
    > >>> vars(a)
    > {'multi': 4, 'str': '2'}
    > >>> a.__dict__
    > {'multi': 4, 'str': '2'}
    > ```
    > 
    > ---
    > 
    > ```python
    > >>> ', '.join(i for i in dir(a) if not i.startswith('__'))
    > 'multi, str'
    > ```
    > 
    > This of course will print any methods or attributes in the class definition. You can exclude "private" methods by changing `i.startwith('__')` to `i.startwith('_')`
    > 



## dir()

- [Python dir() 函数 | 菜鸟教程](http://www.runoob.com/python/python-func-dir.html)

    > **dir()** 函数不带参数时，返回当前范围内的变量、方法和定义的类型列表；带参数时，返回参数的属性、方法列表。如果参数包含方法__dir__()，该方法将被调用。如果参数不包含__dir__()，该方法将最大限度地收集参数信息。
    > 
    > ---
    > 
    > 以下实例展示了 dir 的使用方法：
    > ```python
    > >>> dir()  # 获得当前模块的属性列表  
    > ['__builtins__', '__doc__', '__name__', '__package__', 'arr', 'myslice'] 
    > >>> dir([ ])  # 查看列表的方法  
    > ['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__delslice__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getslice__', '__gt__', '__hash__', '__iadd__', '__imul__', '__init__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', '__rmul__', '__setattr__', '__setitem__', '__setslice__', '__sizeof__', '__str__', '__subclasshook__', 'append', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort'] 
    > >>>
    > ```
    > 


## \_\_dict__

- [特性名稱空間](https://openhome.cc/Gossip/Python/PropertyNameSpace.html)

    > 一個事實是：類別（Class）或實例（Instance）本身的作用是作為特性（Property）的名稱空間（Namespace）。類別或實例本身會擁有一個__dict__特性參考至一個字典物件，其中記錄著類別或實例所擁有的特性。例如：
    > ```python
    > >>> class Math:
    > ...     PI = 3.14159
    > ...
    > >>> Math.PI
    > 3.14159
    > >>> print(Math.__dict__)
    > {'__dict__': <attribute '__dict__' of 'Math' objects>, '__module__': '__main__',
    >  'PI': 3.14159, '__weakref__': <attribute '__weakref__' of 'Math' objects>, '__doc__': None}
    > >>> Math.__dict__['PI']
    > 3.14159
    > >>>
    > ```
    > 在上例中，Math類別上定義了PI特性，這記錄在Math.__dict__中，你嘗試使用Math.PI，則使用Math.__dict__['PI']來尋找出對應的值。如果你試著透過實例來取得PI：
    > ```python
    > >>> m = Math()
    > >>> m.PI
    > 3.14159
    > >>> print(m.__dict__)
    > {}
    > >>>
    > ```
    > 實際上m所參考的實例，其__dict__中並沒有PI，此時會到Math.__dict__中找看看有無PI。這是Python中尋找特性的順序：如果實例的__dict__中沒有，則到產生實例的類別__dict__中尋找。如果你試著在m實例上設定PI特性：
    > ```python
    > >>> m.PI
    > 3.14
    > >>> Math.PI
    > 3.14159
    > >>> print(m.__dict__)
    > {'PI': 3.14}
    > >>> print(Math.__dict__)
    > {'__dict__': <attribute '__dict__' of 'Math' objects>, '__module__': '__main__',
    >  'PI': 3.14159, '__weakref__': <attribute '__weakref__' of 'Math' objects>, '__doc__': None}
    > >>>
    > ```
    > 實際上你並沒有改變Math.__dict__中的PI，而是在實例m.__dict__中新增一個PI，而你嘗試使用實例存取PI時，由於m.__dict__中已經有了，就直接取得該值。
    > 
    > 這也說明了，為什麼實例方法的第一個參數會綁定至實例：
    > ```python
    > >>> class Some:
    > ...     def setx(self, x):
    > ...         self.x = x
    > ...
    > >>> s = Some()
    > >>> print(Some.__dict__)
    > {'__dict__': <attribute '__dict__' of 'Some' objects>, '__weakref__': <attribute  '__weakref__' of 'Some' objects>, '__module__': '__main__', 'setx': <function setx at 0x018FA078>, '__doc__': None}
    > >>> print(s.__dict__)
    > {}
    > >>> s.setx(10)
    > >>> print(s.__dict__)
    > {'x': 10}
    > >>>
    > ```
    > 類別中所定義的函式，其實就是類別的特性，也就是在類別的__dict__中可以找到該名稱。實例方法的第一個參數self綁定實例，透過self.x來設定特性值，也就是在self.__dict__中添增特性。
    > 
    > 由於Python可以動態地為類別添加屬性，即使是未添加屬性前就已建立的物件，在類別動態添加屬性之後， 也可依Python的名稱空間搜尋順序套用上新的屬性，用這種方式，您可以為類別動態地添加方法。例如：
    > 
    > ```python
    > class Some:
    >     def __init__(self, x):
    >         self.x = x
    >         
    > s = Some(1)
    > Some.service = lambda self, y: print('do service...', self.x + y)
    > s.service(2)    # do service... 3
    > ```
    > 如果你要刪除物件上的某個特性，則可以使用del。例如：
    > ```python
    > >>> class Some:
    > ...     pass
    > ...
    > >>> s = Some()
    > >>> s.x = 10
    > >>> print(s.__dict__)
    > {'x': 10}
    > >>> del s.x
    > >>> print(s.__dict__)
    > {}
    > >>>
    > ```
    > 如果你試著在實例上呼叫某個方法，而該實例上沒有該綁定方法時（被@staticmethod或@classmethod修飾的函式），則會試著去類別__dict__中尋找，並以類別呼叫方式來執行函式。例如：
    > ```python
    > >>> class Some:
    > ...     @staticmethod
    > ...     def service():
    > ...         print('XD')
    > ...
    > >>> s = Some()
    > >>> s.service()
    > XD
    > >>>
    > ```
    > 在上例中，嘗試執行s.service()，由於s並沒有service()的綁定方法（因為被@staticmethod修飾），所以嘗試尋找Some.service()執行。
    > 
    > 實際上，如果嘗試透過實例取得某個特性，如果實例的__dict__中沒有，則到產 生實例的類別__dict__中尋找，如果類別__dict__仍沒有，則會試著呼叫__getattr__()來傳回，如果沒有定義 __getattr__()方法，則會引發AttributeError，如果有__getattr__()，則看__getattr__()如何處理。例如：
    > ```python
    > >>> class Some:
    > ...     w = 10
    > ...     def __getattr__(self, name):
    > ...         if name == 'w':
    > ...             return 20
    > ...
    > >>> s = Some()
    > >>> s.w
    > 10
    > >>> s.x
    > >>> class Some:
    > ...     def __getattr__(self, name):
    > ...         if name == 'w':
    > ...             return 20
    > ...         else:
    > ...             raise AttributeError(name)
    > ...
    > >>> s = Some()
    > >>> s.w
    > 20
    > >>> s.x
    > Traceback (most recent call last):
    >   File "<stdin>", line 1, in <module>
    >   File "<stdin>", line 6, in __getattr__
    > AttributeError: x
    > >>>
    > ```
    > 在類別中的函式執行過程中若有定義實例特性時，具特性名稱是以__開頭，則該名稱會被加工處理。例如：
    > ```python
    > >>> class Some:
    > ...     def __init__(self):
    > ...         self.__x = 10
    > ...
    > >>> s = Some()
    > >>> s.__x
    > Traceback (most recent call last):
    >   File "<stdin>", line 1, in <module>
    > AttributeError: 'Some' object has no attribute '__x'
    > >>> print(s.__dict__)
    > {'_Some__x': 10}
    > >>> s._Some__x
    > 10
    > >>>
    > ```
    > 實例變數若以__name這樣的名稱，則會自動轉換為「_類別名__name」這樣的名稱儲存在實例的__dict__中，以__開頭的變數名稱，Python沒有真正阻止你存取它，但這提示不希望你直接存取。
    > 
    > 如果不想要直接使用實例的__dict__來取得特性字典物件，則可以使用vars()，vars()會代為呼叫實例的__dict__。例如：
    > ```python
    > >>> class Some:
    > ...     def __init__(self):
    > ...         self.x = 10
    > ...         self.y = 20
    > ...
    > >>> s = Some()
    > >>> vars(s)
    > {'y': 20, 'x': 10}
    > >>>
    > ```
    > 

## \_\_dict__ vs. dir()

- [19 Python __dict__与dir()区别 - CSDN博客](https://blog.csdn.net/lis_12/article/details/53521554)

    > `__dict__与dir()`的区别：
    > 
    > 1.  dir()是一个函数，返回的是list；
    > 2.  `__dict__`是一个字典，键为属性名，值为属性值；
    > 3.  dir()用来寻找一个对象的所有属性，包括`__dict__`中的属性，`__dict__`是dir()的子集；
    > 
    > ​ **并不是所有对象都拥有`__dict__`属性。** 许多内建类型就[没有`__dict__`属性](http://blog.csdn.net/lis_12/article/details/53511300)，如list，此时就需要用dir()来列出对象的所有属性。
    > 
    > `__dict__`属性
    > ------------
    > 
    > **`__dict__`是用来存储对象属性的一个字典，其键为属性名，值为属性的值。**
    > 
    > ```python
    > #!/usr/bin/python
    > # -*- coding: utf-8 -*-
    > class A(object):
    >     class_var = 1
    >     def __init__(self):
    >         self.name = 'xy'
    >         self.age = 2
    > 
    >     @property
    >     def num(self):
    >         return self.age + 10
    > 
    >     def fun(self):pass
    >     def static_f():pass
    >     def class_f(cls):pass
    > 
    > if __name__ == '__main__':#主程序
    >     a = A()
    >     print a.__dict__   #{'age': 2, 'name': 'xy'}   实例中的__dict__属性
    >     print A.__dict__
    >     '''
    >     类A的__dict__属性
    >     {
    >     '__dict__': <attribute '__dict__' of 'A' objects>, #这里如果想深究的话查看参考链接5
    >     '__module__': '__main__',               #所处模块
    >     'num': <property object>,               #特性对象
    >     'class_f': <function class_f>,          #类方法
    >     'static_f': <function static_f>,        #静态方法
    >     'class_var': 1, 'fun': <function fun >, #类变量
    >     '__weakref__': <attribute '__weakref__' of 'A' objects>,
    >     '__doc__': None,                        #class说明字符串
    >     '__init__': <function __init__ at 0x0000000003451AC8>}
    >     '''
    > 
    >     a.level1 = 3
    >     a.fun = lambda :x
    >     print a.__dict__  #{'level1': 3, 'age': 2, 'name': 'xy','fun': <function <lambda> at 0x>}
    >     print A.__dict__  #与上述结果相同
    > 
    >     A.level2 = 4
    >     print a.__dict__  #{'level1': 3, 'age': 2, 'name': 'xy'}
    >     print A.__dict__  #增加了level2属性
    > 
    >     print object.__dict__
    >     '''
    >     {'__setattr__': <slot wrapper '__setattr__' of 'object' objects>,
    >     '__reduce_ex__': <method '__reduce_ex__' of 'object' objects>,
    >     '__new__': <built-in method __new__ of type object at>,
    >     等.....
    >     '''
    > ```
    > 
    > 从上述代码可知，
    > 
    > 1.  实例的`__dict__`仅存储与该实例相关的实例属性，
    > 
    >     正是因为实例的`__dict__`属性，每个实例的实例属性才会互不影响。
    > 
    > 2.  类的`__dict__`存储所有实例共享的变量和函数(类属性，方法等)，类的`__dict__`并不包含其父类的属性。
    > 
    > ​
    > 
    > dir()函数
    > -------
    > 
    > ​ dir()是Python提供的一个API函数，**dir()函数会自动寻找一个对象的所有属性**(包括从父类中继承的属性)。
    > 
    > ​ 一个实例的`__dict__`属性仅仅是那个实例的实例属性的集合，并不包含该实例的所有有效属性。所以如果想获取一个对象所有有效属性，应使用dir()。
    > 
    > ```python
    > print dir(A)
    > '''
    > ['__class__', '__delattr__', '__dict__', '__doc__', '__format__', '__getattribute__', '__hash__', '__init__', '__module__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'age', 'class_f', 'class_var', 'fun', 'level1', 'level2', 'name', 'num', 'static_f']
    > '''
    > a_dict = a.__dict__.keys()
    > A_dict = A.__dict__.keys()
    > object_dict = object.__dict__.keys()
    > print a_dict
    > print A_dict
    > print object_dict
    > '''
    > ['fun', 'level1', 'age', 'name']
    > 
    > ['__module__', 'level2', 'num', 'static_f', '__dict__', '__weakref__', '__init__', 'class_f', 'class_var', 'fun', '__doc__']
    > 
    > ['__setattr__', '__reduce_ex__', '__new__', '__reduce__', '__str__', '__format__', '__getattribute__', '__class__', '__delattr__', '__subclasshook__', '__repr__', '__hash__', '__sizeof__', '__doc__', '__init__']
    > '''
    > 
    > #因为每个类都有一个__doc__属性，所以需要去重，去重后然后比较
    > print set(dir(a)) == set(a_dict + A_dict + object_dict)  #True
    > ```
    > 
    > 结论
    > --
    > 
    > dir()函数会自动寻找一个对象的所有属性，包括`__dict__`中的属性。
    > 
    > `__dict__`是dir()的子集，dir()包含`__dict__`中的属性。


## \_\_name__

- [Python 程式裡的 __name__ 可以用來分辨程式是直接執行還是被 import 的 | 技術海](https://technology-sea.blogspot.com/2012/03/python-name-import.html)

    > ```python
    > if __name__ == '__main__':
    > doSomething()
    > ```
    > 原來如果一個 python script 是被別的 python script 當成 module 來 import 的話，那麼這個被 import 的 python script 的 __name__ 就會是那個 python script 的名稱。而如果這個 python script 是直接被執行的話，\_\_name__ 就會是 \_\_main__。
    > 
    > 舉例來說，如果我有一個程式叫做 myModule.py，內容就是一行顯示自己的 \_\_name__:
    > ```python
    > print '__name__:' + __name__
    > ```
    > 那麼我直接執行它的話，結果會顯示 \_\_main__:
    > ```python
    > bash-3.2$ python myModule.py
    > __name__:__main__
    > ```
    > 但如果我準備了另一個程式叫做 testModule.py，裡面就這麼一行去 import myModule:
    > ```python
    > import myModule
    > ```
    > 然後我去執行 testModule.py 的話，則會顯示 myModule:
    > ```python
    > bash-3.2$ python testModule.py
    > __name__:myModule
    > ```
    > 所以用 \_\_name__ 就可以分辨我的程式是被 import 當成模組還是被直接執行的。這樣附帶的好處就是如果我寫的程式平常可以被 import 來使用，但有時它自己也可以直接執行。其它語言的話，可能就要區分 library 跟使用 library 的程式，而 python 的話這兩者的界線就很模糊。
    > 

- [python - Why is the value of \_\_name__ changing after assignment to sys.modules[\_\_name__]? - Stack Overflow](https://stackoverflow.com/questions/5365562/why-is-the-value-of-name-changing-after-assignment-to-sys-modules-name)

    > This happens because you have overwrite your module when you did `sys.modules[__name__] = _test()` so your module was deleted (because the module didn't have any references to it anymore and the reference counter went to zero so it's deleted) but in the mean time the interpreter still have the byte code so it will still work but by returning `None` to every variable in your module (this is because python sets all the variables to `None` in a module when it's deleted).
    > 
    > ---
    > 
    > A fix will be by doing like this:
    > 
    > ```python
    > class _test(object): pass
    > 
    > import sys
    > ref = sys.modules[__name__]  # Create another reference of this module.
    > sys.modules[__name__] = _test()   # Now when it's overwritten it will not be
    >                                   # deleted because a reference to it still
    >                                   # exists.
    > 
    > print __name__, _test
    > # __main__ <class '__main__._test'>
    > ```

## clear all varibles

- [How do I clear all variables in the middle of a Python script? - Stack Overflow](https://stackoverflow.com/questions/3543833/how-do-i-clear-all-variables-in-the-middle-of-a-python-script)

    > The following sequence of commands does remove **every** name from the current module:
    > 
    > ```python
    > >>> import sys
    > >>> sys.modules[__name__].__dict__.clear()
    > ```
    > 
    > ---
    > 
    > We can save the state of a module's namespace and restore it by using the following 2 methods...
    > 
    > ```python
    > __saved_context__ = {}
    > 
    > def saveContext():
    >     import sys
    >     __saved_context__.update(sys.modules[__name__].__dict__)
    > 
    > def restoreContext():
    >     import sys
    >     names = sys.modules[__name__].__dict__.keys()
    >     for n in names:
    >         if n not in __saved_context__:
    >             del sys.modules[__name__].__dict__[n]
    > 
    > saveContext()
    > 
    > hello = 'hi there'
    > print hello             # prints "hi there" on stdout
    > 
    > restoreContext()
    > 
    > print hello             # throws an exception
    > ```
    > 
    > You can also add a line "clear = restoreContext" before calling saveContext() and clear() will work like matlab's clear.
    > 

## underscore

- [详解Python中的下划线 - Python - 伯乐在线](http://python.jobbole.com/81129/)

    > 单下划线（_）
    > -------
    > 
    > 通常情况下，会在以下3种场景中使用：
    > 
    > 1、**在解释器中**：在这种情况下，"_"代表交互式解释器会话中上一条执行的语句的结果。这种用法首先被标准CPython解释器采用，然后其他类型的解释器也先后采用。
    > 
    > 
    > ```python
    > >>> _ Traceback (most recent call last): 
    > File "<stdin>", line 1, in <module> 
    > NameError: name '_' is not defined 
    > >>> 42 
    > >>> _ 
    > 42 
    > >>> 'alright!' if _ else ':(' 
    > 'alright!' 
    > >>> _ 
    > 'alright!'
    > ```
    > 
    > 2、**作为一个名称**：这与上面一点稍微有些联系，此时"_"作为临时性的名称使用。这样，当其他人阅读你的代码时将会知道，你分配了一个特定的名称，但是并不会在后面再次用到该名称。例如，下面的例子中，你可能对循环计数中的实际值并不感兴趣，此时就可以使用"_"。
    > 
    > ```python
    > n = 42 
    > for _ in range(n): 
    >     do_something()
    > ```
    > 
    > 3、**国际化**：也许你也曾看到"_"会被作为一个函数来使用。这种情况下，它通常用于实现国际化和本地化字符串之间翻译查找的函数名称，这似乎源自并遵循相应的C约定。例如，在[Django文档"转换"章节](https://docs.djangoproject.com/en/dev/topics/i18n/translation/)中，你将能看到如下代码：
    > 
    > ```python
    > from django.utils.translation import ugettext as _ 
    > from django.http import HttpResponse 
    > def my_view(request): 
    > 	output = _("Welcome to my site.") 
    > 	return HttpResponse(output)
    > ```
    > 
    > 可以发现，场景二和场景三中的使用方法可能会相互冲突，所以我们需要避免在使用"_"作为国际化查找转换功能的代码块中同时使用"_"作为临时名称。
    > 
    > 名称前的单下划线（如：_shahriar）
    > =====================
    > 
    > 程序员使用名称前的单下划线，用于指定该名称属性为"私有"。这有点类似于惯例，为了使其他人（或你自己）使用这些代码时将会知道以"_"开头的名称只供内部使用。正如Python文档中所述：
    > 
    > 以下划线"_"为前缀的名称（如_spam）应该被视为API中非公开的部分（不管是函数、方法还是数据成员）。此时，应该将它们看作是一种实现细节，在修改它们时无需对外部通知。
    > 
    > 正如上面所说，这确实类似一种惯例，因为它对解释器来说确实有一定的意义，如果你写了代码"from <模块/包名> import *"，那么以"_"开头的名称都不会被导入，除非模块或包中的"__all__"列表显式地包含了它们。了解更多请查看"[Importing * in Python](http://shahriar.svbtle.com/importing-star-in-python)"。
    > 
    > 名称前的双下划线（如：__shahriar）
    > ----------------------
    > 
    > 名称（具体为一个方法名）前双下划线（__）的用法并不是一种惯例，对解释器来说它有特定的意义。Python中的这种用法是为了避免与子类定义的名称冲突。Python文档指出，"__spam"这种形式（至少两个前导下划线，最多一个后续下划线）的任何标识符将会被"_classname__spam"这种形式原文取代，在这里"classname"是去掉前导下划线的当前类名。例如下面的例子：
    > 
    > ```python
    > >>> class A(object): 
    > ... def _internal_use(self): 
    > ... pass 
    > ... def __method_name(self): 
    > ... pass 
    > ... 
    > >>> dir(A()) 
    > ['_A__method_name', ..., '_internal_use']
    > ```
    > 
    > 正如所预料的，"_internal_use"并未改变，而"__method_name"却被变成了"_ClassName__method_name"。此时，如果你创建A的一个子类B，那么你将不能轻易地覆写A中的方法"__method_name"。
    > 
    > ```python
    > >>> class B(A): 
    > ... def __method_name(self): 
    > ... pass 
    > ... 
    > >>> dir(B()) 
    > ['_A__method_name', '_B__method_name', ..., '_internal_use']
    > ```
    > 
    > 这里的功能几乎和Java中的final方法和C++类中标准方法（非虚方法）一样。
    > 
    > 名称前后的双下划线（如：__init__）
    > ---------------------
    > 
    > 这种用法表示Python中特殊的方法名。其实，这只是一种惯例，对Python系统来说，这将确保不会与用户自定义的名称冲突。通常，你将会覆写这些方法，并在里面实现你所需要的功能，以便Python调用它们。例如，当定义一个类时，你经常会覆写"__init__"方法。
    > 
    > 虽然你也可以编写自己的特殊方法名，但不要这样做。
    > 
    > ```python
    > >>> class C(object): 
    > ... def __mine__(self): 
    > ... pass 
    > ... 
    > >>> dir(C) 
    > ... [..., '__mine__', ...]
    > ```
    > 
    > 其实，很容易摆脱这种类型的命名，而只让Python内部定义的特殊名称遵循这种约定。


# modules

## Python 的 Import 陷阱 

- [Python 的 Import 陷阱 – PyLadies Taiwan – Medium](https://medium.com/pyladies-taiwan/python-%E7%9A%84-import-%E9%99%B7%E9%98%B1-3538e74f57e3)


    > ### Module與Package
    > 
    > 基本上一個檔案就是一個 module，裡頭可以定義 function，class，和 variable。\
    > 把一個 module 想成一個檔案，那一個package就是一個目錄了。Package 可裝有 subpackage 和 module，讓你的專案更條理更組織化，最後一坨打包好還能分給別人使用。
    > 
    > 先看看 module。假設有一個 module `sample_module.py` 裡頭定義了一個 function `sample_func`：
    > ```python
    > def sample_func():
    >     print('Hello!')
    > ```
    > 現在你在同一個目錄裡下有另一個 module `sample_module_import.py` 想要重複使用這個 function，這時可以直接從 `sample_module` import 拿取：
    > ```python
    > from sample_module import sample_func
    > 
    > if __name__ == '__main__':
    >     sample_func()
    > ```
    > 跑 `python3 sample_module_import.py` 會得到：
    > ```
    > Hello!
    > ```
    > 再來是 package。我們把上面兩個檔案包在一個新的目錄 `sample_package` 底下：
    > ```
    > sample_package/
    > ├── __init__.py
    > ├── sample_module.py
    > └── sample_module_import.py
    > ```
    > 很重要的是新增那個 `__init__.py` 檔。它是空的沒關係，但一定要有，有點宣稱自己是一個 package 的味道。
    > 
    > 這時候如果是進到 `sample_package` 裡面跑一樣的指令，那沒差。但既然都打包成 package 了，通常是在整個專案的其他地方需要用到的時候 import 它，這時候裡面的 import 就要稍微做因應。
    > 
    > 讓我們修正一下 `sample_package/sample_module_import.py` 。假設這時我們在跟 `sample_package` 同一個 folder 底下執行下面兩種指令：
    > ```
    > 1. python3 sample_package/sample_module_import.py
    > 2. python3 -m sample_package.sample_module_import
    > ```
    > 以下幾種不同的 import 寫法，會各有什麼效果呢？
    > ```
    > # 不標準的 implicit relative import 寫法（Python 3 不支援）
    > from sample_module import sample_func
    > 1. 成功印出 Hello!
    > 2. ModuleNotFoundError。因為 Python 3 不支援 implicit relative import （前面不加點的寫法），故會將之當作 absolute import，但第三個例子才是正確寫法。
    > 
    > # 標準的 explicit relative import 寫法
    > from .sample_module import sample_func
    > 1. 包含相對路徑的檔案不能直接執行，只能作為 module 被引用，所以失敗
    > 2. 成功印出 Hello!
    > 
    > # 標準的 absolute import 寫法
    > from sample_package.sample_module import sample_func
    > 1. 如果此層目錄位置不在 python path 中，就會失敗
    > 2. 成功印出 Hello!
    > ```
    > 這邊 absolute import 和 relative import 的詳細說明請稍候。
    > 
    > 執行指令中的 `[-m](https://docs.python.org/2/using/cmdline.html#cmdoption-m)`是為了讓 Python 預先 import 你要的 package 或 module 給你，然後再執行 script。所以這時 `sample_module_import` 在跑的時候，是以 `sample_package` 為環境的，這樣那些 import 才會合理。
    > 
    > 另外，[**python path**](https://docs.python.org/3/library/sys.html#sys.path) 是 Python 查找 module 時候使用的路徑，例如 standard module 所在的目錄位置。因此在第三種寫法中，Python 會因為在 python path 中找不到 `sample_package.sample_module`而噴 error。你可以選擇把當前目錄加到 `sys.path`，也就是 Python path（初始化自環境變數`PYTHONPATH`），來讓 Python 搜尋得到這個 module ，但這個方法很髒很難維護，最多用來debug，其他時候強烈不建議使用。
    > 
    > * * * * *
    > 
    > ### 基本 import 語法
    > 
    > 前面有看過了，這邊統整介紹一下。如果你想使用在其他 module 裡定義的 function、class、variable 等等，就需要在使用它們之前先進行 import。通常都會把需要 import 的 module 們列在整個檔案的最一開始，但不是必須。
    > 
    > **語法1：** **`import [module]`**
    > ```python
    > # Import 整個 `random` module
    > import random
    > 
    > # 使用 `random` module 底下的 `randint` function
    > print(random.randint(0, 5))
    > ```
    > **語法2：** **`from [module] import [name1, name2, ...]`**
    > ```python
    > # 從 `random` module 裡 import 其中一個 function `randint`
    > from random import randint
    > 
    > # 不一樣的是，使用 `randint` 的時候就不需要先寫 `random` 了
    > print(randint(0, 5))
    > ```
    > **語法3：** **`import [module] as [new_name]`**
    > ```python
    > # Import 整個 `random` module，
    > # 但這個名字可能跟其他地方有衝突，因此改名成 `rd`
    > import random as rd
    > 
    > # 使用 `rd` 這個名稱取代原本的 `random`
    > print(rd.randint(0, 5))
    > ```
    > **語法4（不推薦）：** **`from [module] import *`**
    > ```python
    > # Import 所有 `random` module 底下的東西
    > from random import *
    > 
    > # 使用 `randint` 的時候也不需要先寫 `random`
    > print(randint(0, 5))
    > ```
    > 語法4不推薦原因是容易造成名稱衝突，降低可讀性和可維護性。
    > 
    > * * * * *
    > 
    > ### Absolute Import v.s. Relative Import
    > 
    > Python 有兩種 import 方法，**absolute import** 及 **relative import**。Absolute import 就是完整使用 module 路徑，relative import 則是使用以當前 package為參考的相對路徑。
    > 
    > Relative import 的需求在於，有時候在改變專案架構的時候，裡面的 package 和 module 會拉來拉去，這時候如果這些 package 裡面使用的是relative import 的話，他們的相對關係就不會改變，也就是不需要再一一進入 module 裡更改路徑。但因為 relative import 的路徑取決於當前 package，所以在哪裡執行就會造成不一樣的結果，一不小心又要噴一堆 error；這時absolute import 就會減少許多困擾。
    > 
    > 這邊參考[PEP328](https://www.python.org/dev/peps/pep-0328/#guido-s-decision)提供的範例。Package 架構如下：
    > ```
    > package
    > ├── __init__.py
    > ├── subpackage1
    > │   ├── __init__.py
    > │   ├── moduleX.py
    > │   └── moduleY.py
    > ├── subpackage2
    > │   ├── __init__.py
    > │   └── moduleZ.py
    > └── moduleA.py
    > ```
    > 現在假設 `package/subpackage1/moduleX.py`想要從其他 module 裡 import 一些東西，則使用下列語法（`[A]`表 absolute import 範例；`[R]`表 relative import 範例）：
    > ```
    > # Import 同一個 package 底下的 sibling module `moduleY`
    > [A] from package.subpackage1 import moduleY
    > [R] from . import moduleY
    > [Error] import .moduleY
    > 
    > # 從同一個 package 底下的 sibling module `moduleY` 中，
    > # import `spam` 這個 function
    > [A] from package.subpackage1.moduleY import spam
    > [R] from .moduleY import spam
    > 
    > # 從隔壁 package 底下的 module `moduleZ` 中，
    > # import `eggs` 這個 function
    > [A] from package.subpackage2.moduleZ import eggs
    > [R] from ..subpackage2.moduleZ import eggs
    > 
    > # Import parent package 底下的 module `moduleA`
    > [A] from package import moduleA
    > [R] from .. import moduleA 或 from ... package import moduleA
    > ```
    > 要點：
    > 
    > 1.  Relative import 裡，`..`代表上一層 ，多幾個`.`就代表多上幾層。
    > 2.  Relative import 一律採用 `from ... import ...`語法，即使是從 `.` import也要寫 `from . import some_module` 而非 `import .some_module`。原因是`.some_module`這個名稱在 expression 裡無法出現。Absolute import 則無限制。
    > 
    > * * * * *
    > 
    > ### 常見 import 陷阱
    > 
    > #### Trap 1: Circular Import
    > 
    > 想像一個 module `A`在一開始要 import 另一個 module `B` 裡的東西，但在匯入 module `B` 的途中也必須得執行它，而很不巧的 module `B`也需要從 module `A` import 一些東西。但 module `A`還正在執行途中，自己都還沒定義好自己的 function 啊！於是你不讓我我不讓你，這種類似 deadlock 的情形正是常見的 **circular import（循環匯入）**。
    > 
    > 讓我們看看範例。現在在 `sample_package` 裡有 `A` 和 `B` 兩個 module 想互打招呼，程式碼如下：
    > 
    > `A.py`
    > ```python
    > from .B import B_greet_back
    > def A_say_hello():
    >     print('A says hello!')
    >     B_greet_back()
    > 
    > def A_greet_back():
    >     print('A says hello back!')
    > if __name__ == '__main__':
    >     A_say_hello()
    > ```
    > `B.py`
    > ```python
    > from .A import A_greet_back
    > def B_say_hello():
    >     print('B says hello!')
    >     A_greet_back()
    > 
    > def B_greet_back():
    >     print('B says hello back!')
    > if __name__ == '__main__':
    >     B_say_hello()
    > ```
    > 內容都一樣，只是`A/B`互換。`B` 很有禮貌想先打招呼。在與 `sample_package` 同目錄底下執行：
    > ```
    > $ python3 -m sample_package.B
    > ```
    > 會得到：
    > ```
    > Traceback (most recent call last):
    >   File "/usr/local/Cellar/python3/3.6.2/Frameworks/Python.framework/Versions/3.6/lib/python3.6/runpy.py", line 193, in _run_module_as_main
    >  "__main__", mod_spec)
    >  File "/usr/local/Cellar/python3/3.6.2/Frameworks/Python.framework/Versions/3.6/lib/python3.6/runpy.py", line 85, in _run_code
    >  exec(code, run_globals)
    >  File "/path/to/sample_package/B.py", line 2, in < module>
    >  from .A import A_greet_back
    >  File "/path/to/sample_package/A.py", line 1, in < module>
    >  from .B import B_greet_back
    >  File "/path/to/sample_package/B.py", line 2, in < module>
    >  from .A import A_greet_back
    > ImportError: cannot import name 'A_greet_back'
    > ```
    > 觀察到了嗎？`B` 試圖 import `A_greet_back`，但途中先進到 `A` 執行，而因為 Python 是從頭開始一行一行執行下來的，於是在定義 `A_greet_back`之前會先碰到自己的 import statement，於是又進入 `B`，然後陷入死胡同。
    > 
    > 常見解決這種circular import的方法如下：
    > 
    > 1\.  **Import 整個 module 而非單一 attribute**
    > 
    > 把 `B.py` 更改成如下：
    > ```python
    > # from .A import A_greet_back
    > from . import A
    > def B_say_hello():
    >     print('B says hello!')
    >     # A_greet_back()
    >     A.A_greet_back()
    > 
    > ...
    > ```
    > 就不會發生錯誤：
    > ```
    > B says hello!
    > A says hello back!
    > ```
    > 理由是，原本執行 `from .A import A_greet_back` 時被迫要從 load 進來的 `A`module object 中找出 `A_greet_back` 的定義，但此時這個 module object 還是空的；而更新後的 `from . import A` 就只會檢查 `A` module object 存不存在，至於 `A_greet_back` 存不存在等到需要執行的時候再去找就行了。
    > 
    > 2\. **延遲 import**
    > 
    > 把 `B.py` 更改成如下：
    > ```python
    > # 前面全刪
    > 
    > def B_say_hello():
    >     from .A import A_greet_back
    > 
    >     print('B says hello!')
    >     A_greet_back()
    > ...
    > ```
    > 也會成功跑出結果。跟前面類似，Python 在跑到這行時才會 import `A` module，這時因為 `B` module 都已經 load 完了，所以不會有 circular import 的問題。但這個方法比較 hacky 一點，大概只能在 hackathon 中使用，否則正式專案裡看到這種難維護的 code 可能會有生命危險。
    > 
    > 另一方面，把所有 import statement 擺到整個 module 最後面也是類似效果，但也會被打。
    > 
    > 3\. **好好釐清架構，避免circular import**
    > 
    > 是的，治本方法還是好好思考自己寫的 code 為什麼會陷入這種危機，然後重新 refactor 吧。
    > 
    > #### Trap 2: Relative Import above Top-level Package
    > 
    > 還不熟悉 relative import 的人常常會見到這個 error：
    > ```
    > ValueError: attempted relative import beyond top-level package
    > ```
    > 讓我們重現一下這個 error。把 `B.py` 前頭更改成如下：
    > ```python
    > # from . import A
    > from ..sample_package import A
    > ...
    > ```
    > 現在我們的路徑位置在與 `sample_package` 同目錄底下。跑：
    > ```
    > $ python3 -m sample_package.B
    > ```
    > 會得到：
    > ```
    > Traceback (most recent call last):
    >   File "/usr/local/Cellar/python3/3.6.2/Frameworks/Python.framework/Versions/3.6/lib/python3.6/runpy.py", line 193, in _run_module_as_main
    >  "__main__", mod_spec)
    >  File "/usr/local/Cellar/python3/3.6.2/Frameworks/Python.framework/Versions/3.6/lib/python3.6/runpy.py", line 85, in _run_code
    >  exec(code, run_globals)
    >  File "/path/to/sample_package/B.py", line 5, in < module>
    >  from ..sample_package import A
    > ValueError: attempted relative import beyond top-level package
    > ```
    > 所謂的 `top-level package` 就是你所執行的 package 中最高的那一層，也就是 `sample_package`。超過這一層的 relative import 是不被允許的，指的就是`..sample_package` 這行嘗試跳一層上去而超過 `sample_package`了。
    > 
    > 可以試試更改當前目錄到上一層（`cd ..`），假設叫 `parent_folder` ，然後執行 `python3 -m parent_folder.sample_package.B`，就會發現 error 消失了，因為現在的 `top-level package` 已經變成 `parent_folder`了。
    > 

## import filename starts with a number (import_module)

- [In python, how to import filename starts with a number - Stack Overflow](https://stackoverflow.com/questions/9090079/in-python-how-to-import-filename-starts-with-a-number)

    > Error is:
    > 
    > ```
    > >>> import 8puzzle
    >   File "<input>", line 1
    >     import 8puzzle
    >            ^
    > SyntaxError: invalid syntax
    > >>>
    > ```
    > 
    > ---
    > 
    > You could do
    > 
    > ```
    > puzzle = __import__('8puzzle')
    > ```
    > 
    > ---
    > 
    > The above answers are correct, but as for now, the recommended way is to use [`import_module`](https://docs.python.org/3/library/importlib.html#importlib.import_module) function:
    > 
    > **`importlib.import_module(name, package=None)`**
    > 
    > 

## reload

- [Joe.Dev 的 freeloser 部落格: 筆記：Python: reload reload reload reload 大全](https://joe-dev.blogspot.com/2012/03/python-reload-reload-reload-reload.html)

    > Python 提供了一個方便又惹人厭的 reload function 好處在於透過重新 reload 一個 module，可以進行程式碼更新 (不過在記憶體內的東西還是更新不到...) 惹人厭的地方則是 module 與 module 之間往往具有相依性
    > 當 module A import module B ，且兩者同時有所更新的時候 reload(A); reload(B) 的結果不盡然與 reload(B); reload(A) 相同
    > 
    > 關於這一方面的問題可以參考：
    > [這篇中文介紹](http://powenyang.blogspot.com/2011/05/how-to-reload-python-modules.html) [英文原文](http://www.indelible.org/ink/python-reloading/) 以及 [一個解決此問題的專案](https://github.com/jparise/python-reloader)
    > 
    > 另外，使用此專案時要注意：
    > 
    > 1\. 由於 import 已經被暫時蓋掉，由 reload._import 執行 所以是否真的要對所有的 modules 建立一個 graph 取決於最後的目的 ＃我個人偏好，只對自己寫的 module 建立 graph 因為我不會吃飽太閒去改別人的 module
    > 
    > 2\. 如果使用 reload._import 某些外部的 module 的時候造成問題 那麼可以考慮"早點" import 這些 module
    > 
    > 3\. 對於 monitor.py ，記得補上應該要在 import reload 後面的 reload.enable() 該 module 的使用方式如下：
    >    import 該 module 後，製造出monitor.Reloader() 的 instance 並且使用 .poll() 來詢問是否檔案有所更新
    > 
    > 另外如果不考慮相依性，只是希望達到更新 module 便 reload module 的功能
    > 也可以參考 [對岸朋友的文章](http://www.blogjava.net/huanzhugege/archive/2007/03/12/103325.html) 原理就只是檢查檔案是否更新過
    > 
    > stackoverflow 上面也有類似上述的問題，不過解法是使用pyinotify觀察檔案的更新:
    > detect if a python module changes and then reload: [原文](http://stackoverflow.com/questions/6270395/detect-if-a-python-module-changes-and-then-reload)  [程式碼](https://gist.github.com/1013122)
    > 

- [How do I unload (reload) a Python module? - Stack Overflow](https://stackoverflow.com/questions/437589/how-do-i-unload-reload-a-python-module)

    > You can reload a module when it has already been imported by using the [`reload`](https://docs.python.org/2.7/library/functions.html#reload) builtin function:
    > 
    > ```python
    > from importlib import reload  # Python 3.4+ only.
    > import foo
    > 
    > while True:
    >     # Do some things.
    >     if is_changed(foo):
    >         foo = reload(foo)
    > ```
    > 


# process operation

- [subprocess — Subprocess management — Python 3.7.2rc1 documentation](https://docs.python.org/3/library/subprocess.html#subprocess.TimeoutExpired)

## Executing command line programs(subprocess)

- [Executing command line programs from within python - Stack Overflow](https://stackoverflow.com/questions/450285/executing-command-line-programs-from-within-python)

    > The [`subprocess`](http://docs.python.org/library/subprocess.html) module is the preferred way of running other programs from Python -- much more flexible and nicer to use than `os.system`.
    > 
    > ```python
    > import subprocess
    > #subprocess.check_output(['ls','-l']) #all that is technically needed...
    > print subprocess.check_output(['ls','-l'])
    > ```

### AttributeError: 'module' object has no attribute 'TimeoutExpired'

- [How do I set the TimeoutExpired? · Issue #24 · nst/JSONTestSuite](https://github.com/nst/JSONTestSuite/issues/24)

    > ```
    > AttributeError: 'module' object has no attribute 'TimeoutExpired'
    > ```
    > 
    > python2 subprocess don't have TimeoutExpired, use time.sleep() instead.[name=Ya-Lun Li]
    > 



## terminate a python subprocess launched with shell=True

- [linux - How to terminate a python subprocess launched with shell=True - Stack Overflow](https://stackoverflow.com/questions/4789837/how-to-terminate-a-python-subprocess-launched-with-shell-true)

    > If you can use [psutil](https://pypi.python.org/pypi/psutil/), then this works perfectly:
    > 
    > ```python
    > import subprocess
    > 
    > import psutil
    > 
    > def kill(proc_pid):
    >     process = psutil.Process(proc_pid)
    >     for proc in process.children(recursive=True):
    >         proc.kill()
    >     process.kill()
    > 
    > proc = subprocess.Popen(["infinite_app", "param"], shell=True)
    > try:
    >     proc.wait(timeout=3)
    > except subprocess.TimeoutExpired:
    >     kill(proc.pid)
    > ```


# argparse

## SystemExit: 2 error when calling parse_args()

- [python - SystemExit: 2 error when calling parse_args() - Stack Overflow](https://stackoverflow.com/questions/42249982/systemexit-2-error-when-calling-parse-args)

    > `parse_args` method, when it's called without arguments, attempts to parse content of `sys.argv`. Your interpreter process had filled `sys.argv` with values that does not match with arguments supported by your `parser` instance, that's why parsing fails.
    > 
    > Try printing `sys.argv` to check what arguments was passed to your interpreter process.
    > 
    > Try calling `parser.parse_args(['my', 'list', 'of', 'strings'])` to see how parser will work for interpreter launched with different cmdline arguments.

- [python - Argparse - SystemExit:2 - Stack Overflow](https://stackoverflow.com/questions/49419672/argparse-systemexit2?rq=1)

    > In an `ipython` session:
    > 
    > ```python
    > In [36]: import argparse
    > In [37]: # construct the argument parse and parse the arguments
    >     ...: ap = argparse.ArgumentParser()
    >     ...: ap.add_argument("-i", "--image", required=True,
    >     ...:     help="path to input image")
    >     ...: ap.add_argument("-p", "--prototxt", required=True,
    >     ...:     help="path to Caffe 'deploy' prototxt file")
    >     ...: ap.add_argument("-m", "--model", required=True,
    >     ...:     help="path to Caffe pre-trained model")
    >     ...: ap.add_argument("-c", "--confidence", type=float, default=0.5,
    >     ...:     help="minimum probability to filter weak detections")
    >     ...: args = vars(ap.parse_args())
    >     ...:
    > usage: ipython3 [-h] -i IMAGE -p PROTOTXT -m MODEL [-c CONFIDENCE]
    > ipython3: error: the following arguments are required: -i/--image, -p/--prototxt, -m/--model
    > An exception has occurred, use %tb to see the full traceback.
    > 
    > SystemExit: 2
    > 
    > /usr/local/lib/python3.6/dist-packages/IPython/core/interactiveshell.py:2918: UserWarning: To exit: use 'exit', 'quit', or Ctrl-D.
    >   warn("To exit: use 'exit', 'quit', or Ctrl-D.", stacklevel=1)
    > ```
    > 
    > I can run this parser by modifying `sys.argv`:
    > 
    > ```python
    > In [39]: import sys
    > In [40]: sys.argv[1:]
    > Out[40]:
    > ['--pylab',
    >  '--nosep',
    >  '--term-title',
    >  '--InteractiveShellApp.pylab_import_all=False']
    > In [41]: sys.argv[1:] = '-i image -p proto -m amodel'.split()
    > In [42]: args = ap.parse_args()
    > In [43]: args
    > Out[43]: Namespace(confidence=0.5, image='image', model='amodel', prototxt='proto')
    > ```
    > 
    > or with
    > 
    > ```python
    > In [45]: ap.parse_args('-i image -p proto -m amodel'.split())
    > Out[45]: Namespace(confidence=0.5, image='image', model='amodel', prototxt='proto')
    > ```
    > 
    > I often use this method to test a parser.
    > 
    > If this parser was in a script, and I ran it from command line without the arguments, it would print the `usage` and then exit. That exit is what `ipython` is catching and displaying as `SystemExit: 2`.
    > 
    > 

- [jupyter notebook：使用argparse包存在的问题及解决 - xixihaha的博客 - CSDN博客](https://blog.csdn.net/u012869752/article/details/72513141)

    > ### 问题分析
    > 
    > 由于在jupyter notebook中，args不为空，可以查看系统环境变量，大概是下面形式
    > 
    > ```python
    > import sys
    > sys.argv
    > ```
    > 
    > ```python
    > ['/home/liu/anaconda2/lib/python2.7/site-packages/ipykernel/__main__.py',
    >  '-f',
    >  '/run/user/1006/jupyter/kernel-ce6cfb61-acb9-40bf-a59b-ff6e1c1eacae.json']
    > 
    > ```
    > 
    > 可以看出，错误中的-f /...来自这里，可以查看parse_args()函数源码\
    > 以及和其调用的函数parse_known_args()源码\
    > 虽然args默认参数为None，但是实质为args = _sys.argv[1:]\
    > 所以在jupyter中，可以查看自己需要的系统环境变量，然后以list的数据形式传参给args则可以了
    > 
    > ---
    > 
    > ### 问题解决
    > 
    > ```python
    > parser = argparse.ArgumentParser()
    > parser.add_argument("--verbosity", help="increase output verbosity")
    > args = parser.parse_args(args=[])
    > print(args)
    > ```
    > 
    > ```
    > Namespace(verbosity=None)
    > ```


# easydict

## use easydict instead of argparse

- [python - How to fix ipykernel_launcher.py: error: unrecognized arguments in jupyter? - Stack Overflow](https://stackoverflow.com/questions/48796169/how-to-fix-ipykernel-launcher-py-error-unrecognized-arguments-in-jupyter)

    > or a dictionary using the library [`easydict`](https://pypi.python.org/pypi/easydict/) in this way:
    > 
    > ```
    > args = easydict.EasyDict({
    >     "batch_size": 100,
    >     "train_steps": 1000
    > })
    > ```
    > 
    > With `easydict` we can access dict values as attributes for the arguments.
    > 

## access dict keys as object attributes

- [(1 封私信 / 83 条消息)python中EasyDict是干嘛用的？ - 知乎](https://www.zhihu.com/question/64834166)

    > EasyDict可以让你像访问属性一样访问dict里的变量。如：
    > 
    > ```python
    > >>> from easydict import EasyDict as edict
    > >>> d = edict({'foo':3, 'bar':{'x':1, 'y':2}})
    > >>> d.foo
    > 3
    > >>> d.bar.x
    > 1
    > 
    > >>> d = edict(foo=3)
    > >>> d.foo
    > 3
    > ```



# unittest

## example

- [unittest — Unit testing framework — Python 3.7.2rc1 documentation](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertRaises)

    > Basic example
    > -------------
    > 
    > The [`unittest`](https://docs.python.org/3/library/unittest.html#module-unittest "unittest: Unit testing framework for Python.") module provides a rich set of tools for constructing and running tests. This section demonstrates that a small subset of the tools suffice to meet the needs of most users.
    > 
    > Here is a short script to test three string methods:
    > 
    > ```python
    > import unittest
    > 
    > class TestStringMethods(unittest.TestCase):
    > 
    >     def test_upper(self):
    >         self.assertEqual('foo'.upper(), 'FOO')
    > 
    >     def test_isupper(self):
    >         self.assertTrue('FOO'.isupper())
    >         self.assertFalse('Foo'.isupper())
    > 
    >     def test_split(self):
    >         s = 'hello world'
    >         self.assertEqual(s.split(), ['hello', 'world'])
    >         # check that s.split fails when the separator is not a string
    >         with self.assertRaises(TypeError):
    >             s.split(2)
    > 
    > if __name__ == '__main__':
    >     unittest.main()
    > ```
    > 


# Anaconda

## Virtual environments

- [Create virtual environments for python with conda](https://uoa-eresearch.github.io/eresearch-cookbook/recipe/2014/11/20/conda/)

    1\. Check conda is installed and in your PATH
    ---------------------------------------------

    1.  Open a terminal client.
    2.  Enter `conda -V` into the terminal command line and press enter.
    3.  If conda is installed you should see somehting like the following.

    ```bash
    $ conda -V
    conda 3.7.0
    ```

    2\. Check conda is up to date
    -----------------------------

    1.  In the terminal client enter

    ```bash
    conda update conda
    ```

    2.  Upadate any packages if necessary by typing `y` to proceed.

    3\. Create a virtual environment for your project
    -------------------------------------------------

    1.  In the terminal client enter the following where _yourenvname_ is the name you want to call your environment, and replace _x.x_ with the Python version you wish to use. (To see a list of available python versions first, type `conda search "^python$"` and press enter.)

    ```bash
    conda create -n yourenvname python=x.x anaconda
    ```

    2.  Press `y` to proceed. This will install the Python version and all the associated anaconda packaged libraries at “path\_to\_your\_anaconda\_location/anaconda/envs/yourenvname”

    4\. Activate your virtual environment.
    --------------------------------------

    1.  To activate or switch into your virtual environment, simply type the following where _yourenvname_ is the name you gave to your environement at creation.

    ```bash
    source activate yourenvname
    ```

    2.  Activating a conda environment modifies the PATH and shell variables to point to the specific isolated Python set-up you created. The command prompt will change to indicate which conda environemnt you are currently in by prepending `(yourenvname)`. To see a list of all your environments, use the command `conda info -e`.

    5\. Install additional Python packages to a virtual environment.
    ----------------------------------------------------------------

    1.  To install additional packages only to your virtual environment, enter the following command where _yourenvname_ is the name of your environemnt, and _\[package\]_ is the name of the package you wish to install. _Failure to specify “-n yourenvname” will install the package to the root Python installation._

    ```bash
    conda install -n yourenvname [package]
    ```

    6\. Deactivate your virtual environment.
    ----------------------------------------

    1.  To end a session in the current environment, enter the following. There is no need to specify the envname - which ever is currently active will be deactivated, and the PATH and shell variables will be returned to normal.

    ```bash
    source deactivate
    ```

    7\. Delete a no longer needed virtual environment
    -------------------------------------------------

    1.  To delete a conda environment, enter the following, where _yourenvname_ is the name of the environment you wish to delete.

    ```bash
    conda remove -n yourenvname -all
    ```

- [virtualenv - CondaValueError: Value error: prefix already exists: - Stack Overflow](https://stackoverflow.com/questions/40180652/condavalueerror-value-error-prefix-already-exists)

    > simply deleted folder `C:\Program Files\Miniconda2\envs\ENV1\`

### clean packages

- [conda clean — Conda documentation](https://conda.io/docs/commands/conda-clean.html)

    ```shell
    conda clean
    ```


# Troubleshooting

- [[問題] python讀檔時不認得中文字？ - 看板 Python - 批踢踢實業坊](https://www.ptt.cc/bbs/Python/M.1412756706.A.390.html)

    Symptom:
    `UnicodeDecodeError: 'cp950' codec can't decode byte 0xe6 in position 6: illegal multibyte sequence`
    
    Solution:
    指定open的 encoding 為 utf8
    `f = open('test.txt', encoding = 'utf8')`


- [python - img = Image.open(fp) AttributeError: class Image has no attribute 'open' - Stack Overflow](https://stackoverflow.com/questions/10748822/img-image-openfp-attributeerror-class-image-has-no-attribute-open)

    > You have a namespace conflict. One of your import statements is masking `PIL.Image` (which is a module, not a class) with some class named `Image`.
    > 
    > Instead of ...
    > 
    > ```
    > from PIL import Image
    > ```
    > 
    > try ...
    > 
    > ```
    > import PIL.Image
    > ```
    > 
    > then later in your code...
    > 
    > ```
    > fp = open("/pdf-ex/downloadwin7.png","rb")
    > img = PIL.Image.open(fp)
    > img.show()
    > ```
    > 
    > When working with a LOT of imports, beware of namespace conflicts. I'm generally very wary of `from some_module import *` statements.
    > 
    > Good luck with your project and happy coding.
    > 


## Python ValueError: too many values to unpack

- [Python ValueError: too many values to unpack - Stack Overflow](https://stackoverflow.com/questions/7053551/python-valueerror-too-many-values-to-unpack)

    > ```
    > for k, m in self.materials.items():
    > ```
    > 
    > example:
    > 
    > ```
    > miles_dict = {'Monday':1, 'Tuesday':2.3, 'Wednesday':3.5, 'Thursday':0.9}
    > for k, v in miles_dict.items():
    >     print("%s: %s" % (k, v))
    > ```
    > 

- [ValueError: too many values to unpack - 乐居 - ITeye博客](http://leonzhan.iteye.com/blog/1720315)

    > too many values to unpack  
    >   
    > 这种错误是指一个tuple值赋给一个tuple变量时，变量个数不够造成的。如：  
    > a, b = (1, 2, 3)
    > 
    > for example: if ditc_a is dict, following code will get this error
    > 
    > for key, value in ditc_a:
    > 
    >     ...
    > 
    > Correct:
    > 
    > for key, value in ditc_a.items():
    > 
    >     ...
    > 


