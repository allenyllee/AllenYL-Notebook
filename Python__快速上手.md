# Python__快速上手

<!-- toc --> 
[toc]

## Basic Tutorial
* [Python Tutorial](https://www.tutorialspoint.com/python/index.htm)

## Packages

- [Python Extension Packages for Windows - Christoph Gohlke](https://www.lfd.uci.edu/~gohlke/pythonlibs/)

## Usage

### if or not

- [Python simple if or logic statement - Stack Overflow](https://stackoverflow.com/questions/7141208/python-simple-if-or-logic-statement)

    > If `key` isn't an `int` or `float` but a `str`ing, you need to convert it to an `int` first by doing
    > 
    > ```
    > key = int(key)
    > ```
    > 
    > or to a `float` by doing
    > 
    > ```
    > key = float(key)
    > ```
    > 
    > Otherwise, what you have in your question should work, but
    > 
    > ```
    > if (key < 1) or (key > 34):
    > ```
    > 
    > or
    > 
    > ```
    > if not (1 <= key <= 34):
    > ```
    > 
    > would be a bit clearer.


### Sort

- [Sw@y's Notes: [Python]如何在Python排序(Python Sorting)](https://swaywang.blogspot.tw/2012/05/pythonpythonpython-sorting.html)

    > Python提供兩種內建排序的function分別是sort()和sorted()  
    > 這兩個function都可以用來排序一個list  
    > 差別在於sorted()會回傳一個排序好新的list  
    > sort()會直接修改原始的list並排序完成  
    > 以下是一個範例:  
    > ```python
    > >>> a = [2, 4, 3, 5, 1]
    > >>> sorted(a)
    > [1, 2, 3, 4, 5]
    > >>> a
    > [2, 4, 3, 5, 1]
    > >>> a.sort()
    > >>> print a
    > [1, 2, 3, 4, 5]
    > ```
    > 從以上範例可以知道，如果你確定原始的list不需要保留下來的話，可以使用sort()來排序  
    > 如果要保留原本的list，就用sorted()來產生一個排序好的新list


### Pretty Print

- [8.11. pprint — Data pretty printer — Python 3.3.7 documentation](https://docs.python.org/3.3/library/pprint.html?highlight=pprint#module-pprint)
    
    - __pprint.pprint(_object_, _stream=None_, _indent=1_, _width=80_, _depth=None_)__
        Prints the formatted representation of _object_ on _stream_, followed by a newline.

### Regular Expresion

- [6.2. re — Regular expression operations — Python 3.3.7 documentation](https://docs.python.org/3.3/library/re.html?highlight=re#re.compile)
    - __re.compile(_pattern_, _flags=0_)[](https://docs.python.org/3.3/library/re.html?highlight=re#re.compile "Permalink to this definition")__
        Compile a regular expression pattern into a regular expression object, which can be used for matching using its [match()](https://docs.python.org/3.3/library/re.html?highlight=re#re.match "re.match") and [search()](https://docs.python.org/3.3/library/re.html?highlight=re#re.search "re.search") methods, described below.





### String Operation

- [Python String replace() Method](https://www.tutorialspoint.com/python/string_replace.htm)
    > The method **replace()** returns a copy of the string in which the occurrences of _old_ have been replaced with _new_, optionally restricting the number of replacements to _max_.

- [Which is the preferred way to concatenate a string in Python? - Stack Overflow](https://stackoverflow.com/questions/12169839/which-is-the-preferred-way-to-concatenate-a-string-in-python)

    > The _best_ way of appending a string to a string variable is to use `+` or `+=`. This is because it's readable and fast.

- [Python join()方法 | 菜鸟教程](http://www.runoob.com/python/att-string-join.html)

    > Python join() 方法用于将序列中的元素以指定的字符连接生成一个新的字符串。
    > 
    > 以下实例展示了join()的使用方法：
    > 
    > ```python
    > #!/usr/bin/python 
    > str =   "-"; 
    > seq =   ("a",   "b",   "c");   \# 字符串序列
    > print str.join( seq );
    > ```
    > 
    > 以上实例输出结果如下：
    > ```shell
    > a-b-c
    > ```


### Math 

- [math - How do I do exponentiation in python? - Stack Overflow](https://stackoverflow.com/questions/30148740/how-do-i-do-exponentiation-in-python)

    > `^` is the [xor](http://en.wikipedia.org/wiki/Exclusive_or) operator.
    > 
    > `**` is exponentiation.
    > 
    > `2**3 = 8`



### yield & Generator

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

    當使用者第一次呼叫 generator 的  next 方法時，他會從 a = 3 開始執行，直到遇到 yield。python 會回傳 yield 後面接的東西(就像 return )，之後再把現在的 call stack( python 中是 frame)，儲存在 generator 的 gi_frame 屬性中。  

    當使用者第二次呼叫 generator 的  next 方法時，他不會建立一個新的 call stack，而是從  generator 的 gi_frame 屬性中取出之前的 call stack。因此，程式會從 c = 4 開始執行(不是從 a = 3喔，如果是 function 的話，是從 a = 3 開始執行)。直到遇到 yield 或是 return 為止。遇到 yield 表示下次還可以再呼叫一次 next 方法。遇到 return 則表示 這個 generator 已經沒東西了。無法再呼叫 next 了。執行流程像這樣。  


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




### Column/Row operation

* [numpy - Python Pandas - Changing some column types to categories - Stack Overflow](https://stackoverflow.com/questions/28910851/python-pandas-changing-some-column-types-to-categories)

    __Solution1:__
    
    Sometimes, you just have to use a for-loop:

    ```python=
    for col in ['parks', 'playgrounds', 'sports', 'roading']:
        public[col] = public[col].astype('category')
    ```
    
    __Solution2:__
    You can use the `pandas.DataFrame.apply` method along with a `lambda` expression to solve this. In your example you could use

    ```python=
    df[['parks', 'playgrounds', 'sports']].apply(lambda x: x.astype('category'))
    ```

    I don't know of a way to execute this inplace, so typically I'll end up with something like this:

    ```python=
    df[df.select_dtypes(['object']).columns] = df.select_dtypes(['object']).apply(lambda x: x.astype('category'))
    ```

    Obviously you can replace `.select_dtypes` with explicit column names if you don't want to select all of a certain datatype (although in your example it seems like you wanted all `object` types).


- [Combine two columns of text in dataframe in pandas/python - Stack Overflow](https://stackoverflow.com/questions/19377969/combine-two-columns-of-text-in-dataframe-in-pandas-python/19378497)

    > ```python
    > df = pd.DataFrame({'Year': ['2014', '2015'], 'quarter': ['q1', 'q2']})
    > df['period'] = df[['Year', 'quarter']].apply(lambda x: ''.join(x), axis=1)
    > ```
    > 
    > Yields this dataframe
    > 
    > ```shell
    >    Year quarter  period
    > 0  2014      q1  2014q1
    > 1  2015      q2  2015q2
    > ```
    > 
    > This method generalizes to an arbitrary number of string columns by replacing `df[['Year', 'quarter']]` with any column slice of your dataframe, e.g. `df.iloc[:,0:2].apply(lambda x: ''.join(x), axis=1)`.
    > 
    > You can check more information about apply() method [here](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.apply.html)


### Oneline if-then-else

- [python - Putting a simple if-then-else statement on one line - Stack Overflow](https://stackoverflow.com/questions/2802726/putting-a-simple-if-then-else-statement-on-one-line)

    __Solution1:__
    
    That's more specifically a [ternary operator](https://en.wikipedia.org/wiki/%3F:#Python) expression than an if-then, here's the python syntax

    ```python=
    value_when_true if condition else value_when_false
    ```

    **Better Example:** (thanks [Mr. Burns](https://stackoverflow.com/users/253254/joshua-burns))

    `'Yes' if fruit == 'Apple' else 'No'`

    **Now with assignment and contrast with if syntax**

    ```python=
    fruit = 'Apple'
    isApple = True if fruit == 'Apple' else False
    ```

    **vs**

    ```python=
    fruit = 'Apple'
    isApple = False
    if fruit == 'Apple' : isApple = True
    ```

    __Solution2:__
    
    General ternary syntax:

    ```python=
    value_true if <test> else value_false
    ```

    Another way can be:

    ```python=
    [value_false, value_true][<test>]
    ```

    e.g:

    ```python=
    count = [0,N+1][count==N]
    ```

    This evaluates both branches before choosing one. To only evaluate the chosen branch:

    ```python=
    [lambda: value_false, lambda: value_true][<test>]()
    ```

    e.g.:

    ```python=
    count = [lambda:0, lambda:N+1][count==N]()
    ```

- [python - One line if-condition-assignment - Stack Overflow](https://stackoverflow.com/questions/7872838/one-line-if-condition-assignment)

    ```python=
    num1 = 10 + 10*(someBoolValue == True)
    ```

- [python - How to implement the ReLU function in Numpy - Stack Overflow](https://stackoverflow.com/questions/32109319/how-to-implement-the-relu-function-in-numpy)

    You can do it in much easier way and without numpy:

    ```python=
    def ReLU(x):
        return x * (x > 0)

    def dReLU(x):
        return 1. * (x > 0)
    ```

### with...as...

- [icodding愛程式: python 研究-with as 用法](https://icodding.blogspot.tw/2016/05/python-with-as.html)

    有一些任務，可能事先需要設置，事後做清理工作。對於這種場景，Python的with語句提供了一種非常方便的處理方式。一個很好的例子是文件處理，你需要獲取一個文件句柄，從文件中讀取資料，然後關閉文件句柄。  

    如果不用with語句，程式碼如下：  

    ```python=
        file = open("/tmp/foo.txt")  
        data = file.read()  
        file.close()  
    ```
    
    這裡有兩個問題:  

        一是可能忘記關閉文件句柄；  
        二是文件讀取資料發生異常，沒有進行任何處理。  

    下面是處理異常的加強版本：  

    ```python=
        try:  
            f = open('xxx')  
        except:  
            print 'fail to open'  
            exit(-1)  
        try:  
            do something  
        except:  
            do something  
        finally:  
             f.close()  
    ```
                    
    雖然這段程式碼執行良好，但是太冗長了。  

    這時候就是with一展身手的時候了。除了有更優雅的語法，with還可以很好的處理上下文環境產生的異常。  

    下面是with版本的程式碼：  

    ```python=
        with open("/tmp/foo.txt") as file:  
            data = file.read()  
    ```
    
    with如何工作?  

        緊跟with後面的語句被求值後，返回物件的 \_\_enter\_\_() 方法被呼叫，這個方法的返回值將被賦值給as後面的變數。  
        當with後面的程式碼塊全部被執行完之後，將呼叫前面返回物件的 \_\_exit\_\_()方法。  

    下面例子可以具體說明with如何工作：  

    ```python=
        #!/usr/bin/env python  
        # with_example01.py  
        class Sample:  
            def \_\_enter\_\_(self):  
                print "In \_\_enter\_\_()"  
                return "Foo"  
            def \_\_exit\_\_(self, type, value, trace):  
                print "In \_\_exit\_\_()"  
        def get_sample():  
            return Sample()  
        with get_sample() as sample:  
            print "sample:", sample  
    ```
            
    執行程式碼，輸出如下  

    ```shell=
        bash-3.2$ ./with_example01.py  
        In \_\_enter\_\_()  
        sample: Foo  
        In \_\_exit\_\_()  
    ```
    
    正如你看到的: 1\. \_\_enter\_\_()方法被執行 2. \_\_enter\_\_()方法返回的值 - 這個例子中是」Foo」，賦值給變數』sample' 3. 執行程式碼塊，列印變數」sample」的值為 「Foo」 4. \_\_exit\_\_()方法被呼叫 with真正強大之處是它可以處理異常。

    上文說了 \_\_exit\_\_ 函數可以進行部分異常的處理，如果我們不在這個函數中處理異常，他會正常拋出，這時候我們可以這樣寫（python 2.7及以上版本，之前的版本參考使用contextlib.nested這個庫函數）：  

    ```python=
        try:  
            with open( "a.txt" ) as f :  
                do something  
        except xxxError:  
            do something about exception  
    ```
    
    總之，with-as表達式極大的簡化了每次寫finally的工作，這對保持程式碼的優雅性是有極大幫助的。  

    如果有多個項，我們可以這麼寫：  
    
    ```python=
        with open("x.txt") as f1, open('xxx.txt') as f2:  
            do something with f1,f2
    ```

- [What is the python keyword "with" used for? - Stack Overflow](https://stackoverflow.com/questions/1369526/what-is-the-python-keyword-with-used-for)

    The `with` statement is a control-flow structure whose basic structure is:

    ```python=
    with expression [as variable]:
        with-block
    ```

    The expression is evaluated, and it should result in an object that supports the context management protocol (that is, has `__enter__()` and `__exit__()` methods).

### get dicectory path

- [python - Find current directory and file's directory - Stack Overflow](https://stackoverflow.com/questions/5137497/find-current-directory-and-files-directory)

    > To get the full path to the directory a Python file is contained in, write this in that file:
    > 
    > ```python
    > import os 
    > dir_path = os.path.dirname(os.path.realpath(__file__))
    > ```
    > 
    > (Note that the incantation above won't work if you've already used `os.chdir()` to change your current working directory, since the value of the `__file__` constant is relative to the current working directory and is not changed by an `os.chdir()` call.)
    > 
    > ---
    > 
    > To get the current working directory use
    > 
    > ```python
    > import os
    > cwd = os.getcwd()
    > ```
    > 
    > ---
    > 
    > Documentation references for the modules, constants and functions used above:
    > 
    > -   The [`os`](https://docs.python.org/library/os.html) and [`os.path`](https://docs.python.org/library/os.path.html#module-os.path) modules.
    > -   The [`__file__`](https://docs.python.org/reference/datamodel.html) constant
    > -   [`os.path.realpath(path)`](https://docs.python.org/library/os.path.html#os.path.realpath) (returns _"the canonical path of the specified filename, eliminating any symbolic links encountered in the path"_)
    > -   [`os.path.dirname(path)`](https://docs.python.org/library/os.path.html#os.path.dirname) (returns _"the directory name of pathname `path`"_)
    > -   [`os.getcwd()`](https://docs.python.org/library/os.html#os.getcwd) (returns _"a string representing the current working directory"_)
    > -   [`os.chdir(path)`](https://docs.python.org/library/os.html#os.chdir) (_"change the current working directory to `path`"_)


### get command output

- [Running shell command from Python and capturing the output - Stack Overflow](https://stackoverflow.com/questions/4760215/running-shell-command-from-python-and-capturing-the-output)

    > This is a **tricky** but **super simple** solution which works in many situations:
    > 
    > ```python
    > import os
    > os.system('sample_cmd > tmp')
    > print open('tmp', 'r').read()
    > ```
    > 
    > A temporary file(here is tmp) is created with the output of the command and you can read from it your desired output.
    > 
    > Extra note from the comments: You can remove the tmp file in the case of one-time job. If you need to do this several times, there is no need to delete the tmp.
    > 
    > ```python
    > os.remove('tmp')
    > ```

### get running Kernel path

- [python - Jupyter notebook xgboost import - Stack Overflow](https://stackoverflow.com/questions/44856105/jupyter-notebook-xgboost-import)

    > Running a shell escape `!pip3` doesn't guarantee that it will install in the kernel you are running. Try:
    > 
    > ```
    > import sys
    > print(sys.base_prefix)
    > ```
    > 
    > and see if this matches either of your terminal pythons. You should be able to run `<base_prefix>/bin/pip install <package>` to ensure it is in the right `site-packages`.
    > 
    > You can also look at which `python` your kernel is running by looking in `kernel.json` most likely in `~/Library/Jupyter/kernels/<kernel>/kernel.json`.
    > 
    > Note: you can also programmatically install packages with:
    > 
    > ```
    > import pip
    > pip.main(['install', '<package>'])
    > ```
    > 
    > which will force it to be in the right `site-packages` for your kernel.
    > 


### indexing & slicing

- [list - Understanding Python's slice notation - Stack Overflow](https://stackoverflow.com/questions/509211/understanding-pythons-slice-notation)

    > It's pretty simple really:
    > 
    > ```
    > a[start:end] # items start through end-1
    > a[start:]    # items start through the rest of the array
    > a[:end]      # items from the beginning through end-1
    > a[:]         # a copy of the whole array
    > ```
    > 
    > There is also the `step` value, which can be used with any of the above:
    > 
    > ```
    > a[start:end:step] # start through not past end, by step
    > ```
    > 
    > The key point to remember is that the `:end` value represents the first value that is _not_ in the selected slice. So, the difference beween `end` and `start` is the number of elements selected (if `step` is 1, the default).
    > 
    > The other feature is that `start` or `end` may be a _negative_ number, which means it counts from the end of the array instead of the beginning. So:
    > 
    > ```
    > a[-1]    # last item in the array
    > a[-2:]   # last two items in the array
    > a[:-2]   # everything except the last two items
    > ```
    > 
    > Python is kind to the programmer if there are fewer items than you ask for. For example, if you ask for `a[:-2]` and `a` only contains one element, you get an empty list instead of an error. Sometimes you would prefer the error, so you have to be aware that this may happen.

    > and a\[::-1\] to reverse a string. – [Christopher Mahan](https://stackoverflow.com/users/479/christopher-mahan "5,181 reputation") [Feb 3 '09 at 23:54](https://stackoverflow.com/questions/509211/understanding-pythons-slice-notation#comment323779_509295)

    > Also can be important that `[:]` returns a [`shallow copy`](http://docs.python.org/2/library/copy.html) of a list. it means that every slice notation returns a list which have new address in memory, but its elements would have same addresses that elements of source list have. – [Gill Bates](https://stackoverflow.com/users/1818608/gill-bates "1,959 reputation") [Dec 30 '12 at 17:07](https://stackoverflow.com/questions/509211/understanding-pythons-slice-notation#comment19491969_509295)

 - [Python list error: [::-1] step on [:-1] slice - Stack Overflow](https://stackoverflow.com/questions/41430791/python-list-error-1-step-on-1-slice)

    > **The first `-1` in `a[:-1:-1]` doesn't mean what you think it does.**
    > 
    > In slicing, negative start/end indices are not interpreted literally. Instead, they are used to conveniently refer to the end of the list (i.e. they are relative to `len(a)`). This happens irrespectively of the direction of the slicing.
    > 
    > This means that
    > 
    > ```
    > a[:-1:-1]
    > ```
    > 
    > is equivalent to
    > 
    > ```
    > a[:len(a)-1:-1]
    > ```
    > 
    > When omitted during reverse slicing, the start index defaults to `len(a)-1`, making the above equivalent to
    > 
    > ```
    > a[len(a)-1:len(a)-1:-1]
    > ```
    > 
    > This always gives an empty list, since the start and end indices are the same and the end index is exclusive.
    > 
    > To slice in reverse up to, and including, the zeroth element you can use any of the following notations:
    > 
    > ```
    > >>> a[::-1]
    > [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
    > >>> a[:None:-1]
    > [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
    > >>> a[:-len(a)-1:-1]
    > [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
    > ```
    > 


### Split

- [Python split()方法 | 菜鸟教程](http://www.runoob.com/python/att-string-split.html)

    > 描述
    > --
    > 
    > Python split()通过指定分隔符对字符串进行切片，如果参数num 有指定值，则仅分隔 num 个子字符串
    > 
    > 语法
    > --
    > 
    > split()方法语法：
    > 
    > str.split(str="", num=string.count(str)).
    > 
    > 参数
    > --
    > 
    > -   str -- 分隔符，默认为所有的空字符，包括空格、换行(\\n)、制表符(\\t)等。
    > -   num -- 分割次数。
    > 
    > 返回值
    > ---
    > 
    > 返回分割后的字符串列表。
    > 
    > 实例
    > --
    > 
    > 以下实例展示了split()函数的使用方法：
    > ```shell
    > #!/usr/bin/python str =   "Line1-abcdef \nLine2-abc \nLine4-abcd";   print str.split(   );   print str.split(' ',   1   );
    > ```
    > 以上实例输出结果如下：
    > ```python
    > ['Line1-abcdef',   'Line2-abc',   'Line4-abcd']   ['Line1-abcdef',   '\nLine2-abc \nLine4-abcd']
    > ```
    > 


### One-line for loop

- [Python Single Line For Loops - Treehouse Blog](http://blog.teamtreehouse.com/python-single-line-loops)
    ```python
    doubled = [thing for thing in list_of_things]
    ```

### unpack list

- [Unpack a list in Python? - Stack Overflow](https://stackoverflow.com/questions/3480184/unpack-a-list-in-python)
    
    > ```python
    > my_list = ['red', 'blue', 'orange']
    > function_that_needs_strings('red', 'blue', 'orange') # works!
    > function_that_needs_strings(my_list) # breaks!
    > ```

    > ```python
    > function_that_needs_strings(*my_list) # works!
    > ```
    > 
    > [You can read all about it here.](https://docs.python.org/2/tutorial/controlflow.html#unpacking-argument-lists)

- [Homunculus: Unpacking "some" list elements in Python](https://anothercomputingblog.blogspot.tw/2010/05/functional-unpacking-style.html)

    __Catch-all unpacking in Python 3.x__
    
    ```python
    list = \[1, 2, 3, 4\]
    a, b, *rest = list
    ```
    
    __Catch-all unpacking in Python 2.x__

    ```python
    list = [1, 2, 3, 4]
    (a, b), rest = list[:2], list[2:] # The first and second elements are in
    ```


### list directory

- [filesystems - Directory listing in Python - Stack Overflow](https://stackoverflow.com/questions/120656/directory-listing-in-python)

    > This is a way to traverse every file and directory in a directory tree:
    > 
    > ```
    > import os
    > 
    > for dirname, dirnames, filenames in os.walk('.'):
    >     # print path to all subdirectories first.
    >     for subdirname in dirnames:
    >         print(os.path.join(dirname, subdirname))
    > 
    >     # print path to all filenames.
    >     for filename in filenames:
    >         print(os.path.join(dirname, filename))
    > 
    >     # Advanced usage:
    >     # editing the 'dirnames' list will stop os.walk() from recursing into there.
    >     if '.git' in dirnames:
    >         # don't go into any .git directories.
    >         dirnames.remove('.git')
    > ```
    > 

- [python - How do I list all files of a directory? - Stack Overflow](https://stackoverflow.com/questions/3207219/how-do-i-list-all-files-of-a-directory)

    > I prefer using the [`glob`](https://docs.python.org/library/glob.html) module, as it does pattern matching and expansion.
    > 
    > ```
    > import glob
    > print(glob.glob("/home/adam/*.txt"))
    > ```
    > 
    > Will return a list with the queried files:
    > 
    > ```
    > ['/home/adam/file1.txt', '/home/adam/file2.txt', .... ]
    > ```
    > 


    > [`os.listdir()`](https://docs.python.org/2/library/os.html#os.listdir "os.listdir") will get you everything that's in a directory - files and directories.
    > 
    > If you want _just_ files, you could either filter this down using [`os.path`](https://docs.python.org/2/library/os.path.html#module-os.path):
    > 
    > ```
    > from os import listdir
    > from os.path import isfile, join
    > onlyfiles = [f for f in listdir(mypath) if isfile(join(mypath, f))]
    > ```
    > 
    > or you could use [`os.walk()`](https://docs.python.org/2/library/os.html#os.walk "os.walk") which will yield two lists for each directory it visits - splitting into files and dirs for you. If you only want the top directory you can just break the first time it yields
    > 
    > ```
    > from os import walk
    > 
    > f = []
    > for (dirpath, dirnames, filenames) in walk(mypath):
    >     f.extend(filenames)
    >     break
    > ```
    > 
    > And lastly, as that example shows, adding one list to another you can either use [`.extend()`](https://docs.python.org/3/tutorial/datastructures.html#more-on-lists) or
    > 
    > ```
    > >>> q = [1, 2, 3]
    > >>> w = [4, 5, 6]
    > >>> q = q + w
    > >>> q
    > [1, 2, 3, 4, 5, 6]
    > ```
    > 
    > Personally, I prefer `.extend()`
    > 


## Anaconda

### Virtual environments

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


## Troubleshooting

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


### Python ValueError: too many values to unpack

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
    >     ...
    > 
    > Correct:
    > 
    > for key, value in ditc_a.items():
    > 
    >     ...
    > 