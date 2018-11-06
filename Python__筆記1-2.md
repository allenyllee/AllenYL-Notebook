# Python__筆記1-2

[toc]
<!-- toc --> 

# functions/passing varibles/return/yield/Generator

- [Python switch case - LeetCode Playground](https://leetcode.com/playground/Vx2sL4cZ)

    <iframe src="https://leetcode.com/playground/Vx2sL4cZ/shared" frameBorder="0" width="400" height="300"></iframe>

### how to passed by reference

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





# Python reserved attribute

- [Python reserved attribute - LeetCode Playground](https://leetcode.com/playground/b76v2SoG)

    <iframe src="https://leetcode.com/playground/b76v2SoG/shared" frameBorder="0" width="400" height="300"></iframe>

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


