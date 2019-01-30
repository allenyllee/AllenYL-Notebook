# Python__筆記1-1

[toc]
<!-- toc --> 



# Tutorial
- [Python Tutorial](https://www.tutorialspoint.com/python/index.htm)

- [Python Example](https://www.programcreek.com/python/)

## 必學項目


### Functions
- [Python Tutorial: Functions](https://www.python-course.eu/python3_functions.php)

### Recursive Functions
- [Python Tutorial: Recursive Functions](https://www.python-course.eu/python3_recursive_functions.php)

### Passing Arguments
- [Python Tutorial: Passing Arguments](https://www.python-course.eu/python3_passing_arguments.php)

### File Management
- [Python Tutorial: File Management](https://www.python-course.eu/python3_file_management.php)

### Exception Handling
- [Python Tutorial: Exception Handling](https://www.python-course.eu/python3_exception_handling.php)

### Regular Expression
- [Python Tutorial: Regular Expression](https://www.python-course.eu/python3_re.php)

### Object Oriented Programming
- [Python Tutorial: Object Oriented Programming](https://www.python-course.eu/python3_object_oriented_programming.php)

### Class vs. Instance Attributes
- [Python Tutorial: Class vs. Instance Attributes](https://www.python-course.eu/python3_class_and_instance_attributes.php)

## 變數與資料結構

### Data Types and Variables

- [Python Tutorial: Data Types and Variables](https://www.python-course.eu/python3_variables.php)

### Sequential Data Types

- [Python Tutorial: Sequential Data Types](https://www.python-course.eu/python3_sequential_data_types.php)

### Lists

- [Python Tutorial: Lists](https://www.python-course.eu/python3_list_manipulation.php)

### Dictionaries

- [Python Tutorial: Dictionaries](https://www.python-course.eu/python3_dictionaries.php)

### Sets and Frozen Sets

- [Python Tutorial: Sets and Frozen Sets](https://www.python-course.eu/python3_sets_frozensets.php)




## 進階項目

### Shallow and Deep Copy
- [Python Tutorial: Shallow and Deep Copy](https://www.python-course.eu/python3_deep_copy.php)


### List Comprehension

- [Python Tutorial: List Comprehension](https://www.python-course.eu/python3_list_comprehension.php)

### Lambda Operator, filter, reduce and map

- [Python Tutorial: Lambda Operator, filter, reduce and map](https://www.python-course.eu/python3_lambda.php)


### Iterators and Iterables
- [Python Tutorial: Iterators and Iterables](https://www.python-course.eu/python3_iterable_iterator.php)

### Generators
- [Python Tutorial: Generators](https://www.python-course.eu/python3_generators.php)


### Advanced Regular Expressions

- [Python Tutorial: Regular Expression for Advanced Users](https://www.python-course.eu/python3_re_advanced.php)



### Modular Programming and Modules
- [Python Tutorial: Modular Programming and Modules](https://www.python-course.eu/python3_modules_and_modular_programming.php)


### Properties vs. getters and setters
- [Python Tutorial: Properties vs. getters and setters](https://www.python-course.eu/python3_properties.php)


### Slots

- [Python Tutorial: Slots, Avoiding Dynamically Created Attributes](https://www.python-course.eu/python3_slots.php)


### Multiple Inheritance
- [Python Tutorial: Multiple Inheritance](https://www.python-course.eu/python3_multiple_inheritance.php)

    > The case in which m will be overridden only in one of the classes B or C, e.g. in C:
    > ```python
    > class A:
    >     def m(self):
    >         print("m of A called")
    > 
    > class B(A):
    >     pass
    > 
    > class C(A):
    >     def m(self):
    >         print("m of C called")
    > 
    > class D(B,C):
    >     pass
    > 
    > x = D()
    > x.m()
    > ```
    > Principially, two possibilities are imaginable: "m of C" or "m of A" could be used
    > 
    > We call this script with Python2.7 (python) and with Python3 (python3) to see what's happening:
    > ```shell
    > $ python diamond1.py
    > m of A called
    > $ python3 diamond1.py
    > m of C called
    > ```
    > Only for those who are interested in Python version2:
    > To have the same inheritance behaviour in Python2 as in Python3, every class has to inherit from the class "object". Our class A doesn't inherit from object, so we get a so-called old-style class, if we call the script with python2. Multiple inheritance with old-style classes is governed by two rules: depth-first and then left-to-right. If you change the header line of A into "class A(object):", we will have the same behaviour in both Python versions.
    > 
    > ---
    > 
    > The super function is often used when instances are initialized with the __init__ method:
    > ```python
    > class A:
    >     def __init__(self):
    >         print("A.__init__")
    > 
    > class B(A):
    >     def __init__(self):
    >         print("B.__init__")
    >         super().__init__()
    > 
    > class C(A):
    >     def __init__(self):
    >         print("C.__init__")
    >         super().__init__()
    > 
    > class D(B,C):
    >     def __init__(self):
    >         print("D.__init__")
    >         super().__init__()
    > ```
    > 
    > We demonstrate the way of working in the following interactive session:
    > ```python
    > >>> from super_init import A,B,C,D
    > >>> d = D()
    > D.__init__
    > B.__init__
    > C.__init__
    > A.__init__
    > >>> c = C()
    > C.__init__
    > A.__init__
    > >>> b = B()
    > B.__init__
    > A.__init__
    > >>> a = A()
    > A.__init__
    > ```
    > 
    > The question arises how the super functions makes its decision. How does it decide which class has to be used? As we have already mentioned, it uses the so-called method resolution order(MRO). It is based on the "C3 superclass linearisation" algorithm. This is called a linearisation, because the tree structure is broken down into a linear order. The mro method can be used to create this list:
    > ```python
    > >>> from super_init import A,B,C,D
    > >>> D.mro()
    > [<class 'super_init.D'>, <class 'super_init.B'>, <class 'super_init.C'>, <class 'super_init.A'>, <class 'object'>]
    > >>> B.mro()
    > [<class 'super_init.B'>, <class 'super_init.A'>, <class 'object'>]
    > >>> A.mro()
    > [<class 'super_init.A'>, <class 'object'>]
    > ```
    > 


### Abstract Classes

- [Python Tutorial: 'The ABC' of Abstract Base Classes](https://www.python-course.eu/python3_abstract_classes.php)



# General Usage

## API

- [The Python Standard Library — Python 3.3.7 documentation](https://docs.python.org/3.3/library/index.html)

## Style Guide for Python Code

- [PEP 8 -- Style Guide for Python Code | Python.org](https://www.python.org/dev/peps/pep-0008/#function-names)

## Pretty Print

- [8.11. pprint — Data pretty printer — Python 3.3.7 documentation](https://docs.python.org/3.3/library/pprint.html?highlight=pprint#module-pprint)
    
    - __pprint.pprint(_object_, _stream=None_, _indent=1_, _width=80_, _depth=None_)__
        Prints the formatted representation of _object_ on _stream_, followed by a newline.



## run Python scripts as excutable

- [shell - Should I put #! (shebang) in Python scripts, and what form should it take? - Stack Overflow](https://stackoverflow.com/questions/6908143/should-i-put-shebang-in-python-scripts-and-what-form-should-it-take)

    > **Correct** usage for Python 3 scripts is:
    > 
    > ```
    > #!/usr/bin/env python3
    > ```
    > 
    > This defaults to version 3.latest. For Python 2.7.latest use `python2` in place of `python3`.
    > 
    > The following **should NOT be used** (except for the rare case that you are writing code which is compatible with both Python 2.x and 3.x):
    > 
    > ```
    > #!/usr/bin/env python
    > ```
    > 
    > The reason for these recommendations, given in [PEP 394](https://www.python.org/dev/peps/pep-0394/#recommendation "PEP 394"), is that `python` can refer either to `python2` or `python3` on different systems. It currently refers to `python2` on most distributions, but that is likely to change at some point.
    > 
    > **Also, DO NOT Use:**
    > 
    > ```
    > #!/usr/local/bin/python
    > ```
    > 
    > > "python may be installed at /usr/bin/python or /bin/python in those cases, the above #! will fail."
    > 


## Python 2 to 3 translation

- [2to3 - Automated Python 2 to 3 code translation — Python v3.0.1 documentation](https://docs.python.org/3.0/library/2to3.html)
    > ```sh
    > $ 2to3 -w example.py
    > ```

## Writing Python 2-3 compatible code

- [Cheat Sheet: Writing Python 2-3 compatible code — Python-Future documentation](http://python-future.org/compatible_idioms.html)

    > ### print
    > 
    > #### Python 2 only:
    > ```python
    > print 'Hello'
    > ```
    > 
    > #### Python 2 and 3:
    > ```python
    > print('Hello')
    > ```
    > 
    > To print multiple strings, import `print_function` to prevent Py2 from interpreting it as a tuple:
    > 
    > #### Python 2 only:
    > ```python
    > print 'Hello', 'Guido'
    > ```
    > 
    > #### Python 2 and 3:
    > ```python
    > from __future__ import print_function    # (at top of module)
    > 
    > print('Hello', 'Guido')
    > ```
    > 
    > #### Python 2 only:
    > ```python
    > print >> sys.stderr, 'Hello'
    > ```
    > 
    > #### Python 2 and 3:
    > ```python
    > from __future__ import print_function
    > 
    > print('Hello', file=sys.stderr)
    > ```
    > 
    > #### Python 2 only:
    > ```python
    > print 'Hello',
    > ```
    > 
    > #### Python 2 and 3:
    > ```python
    > from __future__ import print_function
    > 
    > print('Hello', end='')
    > ```
    > 

## inline comments(no inline comment in python)

- [How to write an an inline-comment in python - Stack Overflow](https://stackoverflow.com/questions/24872745/how-to-write-an-an-inline-comment-in-python)

    > No, there are no inline comments in Python.
    > 
    > From the [documentation](https://docs.python.org/3/reference/lexical_analysis.html#comments):
    > 
    > > A comment starts with a hash character (`#`) that is not part of a string literal, **and ends at the end of the physical line**. A comment signifies the end of the logical line unless the implicit line joining rules are invoked. Comments are ignored by the syntax; they are not tokens.
    > > 

## precedence of "=" (assign statement)

- [What is the operator precedence of "=" in Python? - Stack Overflow](https://stackoverflow.com/questions/38389391/what-is-the-operator-precedence-of-in-python)

    > `=` is not an operator. `=` is an [assignment **statement**](https://docs.python.org/3/reference/simple_stmts.html#assignment-statements).
    > 
    > Because it is a statement, it can't be part of an expression (expressions are instead part of certain statements, and never the other way around), so ordering is irrelevant. The expression is always executed to serve a statement.
    > 
    > For assignments, the grammar specifies that specific types of expressions are permitted after the `=` symbol:
    > 
    > ```
    > assignment_stmt ::=  (target_list "=")+ (starred_expression | yield_expression)
    > ```
    > 
    > and the documentation for that statement details what order things are executed in:
    > 
    > > An assignment statement evaluates the expression list (remember that this can be a single expression or a comma-separated list, the latter yielding a tuple) and assigns the single resulting object to each of the target lists, from left to right.

# math function

## Round UP a number(ceil)

- [floating point - How do you round UP a number in Python? - Stack Overflow](https://stackoverflow.com/questions/2356501/how-do-you-round-up-a-number-in-python)

    > The [ceil](https://docs.python.org/2/library/math.html#math.ceil) (ceiling) function:
    > 
    > ```python
    > import math
    > print(math.ceil(4.2))
    > ```


## exponential

- [math - How do I do exponentiation in python? - Stack Overflow](https://stackoverflow.com/questions/30148740/how-do-i-do-exponentiation-in-python)

    > `^` is the [xor](http://en.wikipedia.org/wiki/Exclusive_or) operator.
    > 
    > `**` is exponentiation.
    > 
    > `2**3 = 8`

## sqrt
- [Python sqrt() 函数 | 菜鸟教程](http://www.runoob.com/python/func-number-sqrt.html)

## random/choice/sample

- [random — 你所不知道的 Python 標準函式庫用法 02 | louie_lu's blog](https://blog.louie.lu/2017/07/27/random-python-standard-library-02/)

    > ### 01\. random.seed(a=None, version=2)
    > 
    > [*random.seed()*](https://docs.python.org/3/library/random.html#random.seed) 初始化亂數種子。`a` 如果是 None 則使用目前的亂數種子。`a` 可以是 `str`, `bytes`, `bytearray`, 都會被轉型成 `int`。
    > 
    > ---
    > 
    > ### 02\. random.choices(population, weights=None, *, cum_weights=None, k=1)
    > 
    > > *所有動物一律平等，但一些動物比其他動物更加平等。*
    > 
    > 回傳從 `population` 中選取 k 個元素。可以設定 `weights` 或是 `cum_weights` 來改變元素的權重。weights `[10, 5, 13, 27]` 跟 cum_weights `[10, 15, 28, 55]` 是相同的。此為重置抽樣 (sampling with replacement)。
    > 
    > ---
    > 
    > ### 04\. random.sample(population, k)
    > 
    > 回傳長度為 `k` 且元素唯一的 list。此為非重置抽樣 (sampling without replacement)。
    > 
    > 
    > ### 重置抽樣、非重置抽樣
    > 
    > -   Sampling with replacement: 從總體抽出一個元素後，**會**將該元素放回總體。接著重新抽取，因此有機會抽取到相同的元素。
    > -   Sampling without replacement: 從總體抽出一個元素後，**不會**將該元素放回總體。因此不會在次抽到已抽到的元素。
    > 


### random.sample() doesn't keeping same secquence between different sample length

- [random - python seed() not keeping same sequence - Stack Overflow](https://stackoverflow.com/questions/23066235/python-seed-not-keeping-same-sequence)

    > It is the fact that `random.sample()` is drawing samples *without replacement* that's getting in the way. To understand how these algorithms work, see [Reservoir Sampling](http://en.wikipedia.org/wiki/Reservoir_sampling). In essence what happens is that *later* samples can push *earlier* samples out of the result set.
    > 
    > One alternative might be to shuffle a list of indices and then take either 10 or 40 first elements:
    > 
    > ```python
    > In [1]: import random
    > 
    > In [2]: a = range(0,100)
    > 
    > In [3]: random.shuffle(a)
    > 
    > In [4]: a[:10]
    > Out[4]: [48, 27, 28, 4, 67, 76, 98, 68, 35, 80]
    > 
    > In [5]: a[:40]
    > Out[5]: [48, 27, 28, 4, 67, 76, 98, 68, 35, 80, ...]
    > ```
    > 
    > ---
    > 
    > It seems that `random.sample` is deterministic only if the seed *and* sample size are kept constant. In other words, even if you reset the seed, generating a sample with a different length is not "the same" random operation, and may give a different initial subsequence than generating a smaller sample with the same seed. In other words, the same random numbers are being generated internally, but the way `sample` uses them to derive the random sequence is different depending on how large a sample you ask for.
    > 

### random.shuffle() return None, it changes list *in place*

- [python - Why does random.shuffle return None? - Stack Overflow](https://stackoverflow.com/questions/17649875/why-does-random-shuffle-return-none)

    > `random.shuffle()` changes the `x` list **in place**.
    > 
    > Python API methods that alter a structure in-place generally return `None`, not the modified data structure.
    > 
    > If you wanted to create a **new** randomly-shuffled list based of an existing one, where the existing list is kept in order, you could use [`random.sample()`](https://docs.python.org/2/library/random.html#random.sample) with the full length of the input:
    > 
    > ```
    > x = ['foo', 'bar', 'black', 'sheep']
    > random.sample(x, len(x))
    > ```
    > 
    > You could also use [`sorted()`](http://docs.python.org/2/library/functions.html#sorted) with [`random.random()`](http://docs.python.org/2/library/random.html#random.random) for a sorting key:
    > 
    > ```
    > shuffled = sorted(x, key=lambda k: random.random())
    > ```
    > 
    > but this invokes sorting (an O(NlogN) operation), while sampling to the input length only takes O(N) operations (the same process as `random.shuffle()` is used, swapping out random values from a shrinking pool).
    > 
    > Demo:
    > 
    > ```
    > >>> import random
    > >>> x = ['foo', 'bar', 'black', 'sheep']
    > >>> random.sample(x, len(x))
    > ['bar', 'sheep', 'black', 'foo']
    > >>> sorted(x, key=lambda k: random.random())
    > ['sheep', 'foo', 'black', 'bar']
    > >>> x
    > ['foo', 'bar', 'black', 'sheep']
    > ```
    > 
    > ---
    > 
    > `shuffle` modifies the list in place. This is nice, because copying a large list would be pure overhead if you do not need the original list anymore.
    > 
    > According to the *"explicit is better than implicit"* principle of [pythonic style](http://www.python.org/dev/peps/pep-0020/), returning the list would be a bad idea, because then one might think it *is* a new one although in fact it is not.
    > 
    > If you *do* need a fresh list, you will have to write something like
    > 
    > ```
    > new_x = list(x)  # make a copy
    > random.shuffle(new_x)
    > ```
    > 
    > which is nicely explicit. If you need this idiom frequently, wrap it in a function `shuffled` (see `sorted`) that returns `new_x`.
    > 
    > 

## Permutation/Combination/Cartesian product

- [algorithm - How to generate all permutations of a list in Python - Stack Overflow](https://stackoverflow.com/questions/104420/how-to-generate-all-permutations-of-a-list-in-python)

    > *The following code with Python 2.6 and above ONLY*
    > 
    > First, import `itertools`:
    > 
    > ```
    > import itertools
    > ```
    > 
    > ### Permutation (order matters):
    > 
    > ```
    > print list(itertools.permutations([1,2,3,4], 2))
    > [(1, 2), (1, 3), (1, 4),
    > (2, 1), (2, 3), (2, 4),
    > (3, 1), (3, 2), (3, 4),
    > (4, 1), (4, 2), (4, 3)]
    > ```
    > 
    > ### Combination (order does NOT matter):
    > 
    > ```
    > print list(itertools.combinations('123', 2))
    > [('1', '2'), ('1', '3'), ('2', '3')]
    > ```
    > 
    > ### Cartesian product (with several iterables):
    > 
    > ```
    > print list(itertools.product([1,2,3], [4,5,6]))
    > [(1, 4), (1, 5), (1, 6),
    > (2, 4), (2, 5), (2, 6),
    > (3, 4), (3, 5), (3, 6)]
    > ```
    > 
    > ### Cartesian product (with one iterable and itself):
    > 
    > ```
    > print list(itertools.product([1,2], repeat=3))
    > [(1, 1, 1), (1, 1, 2), (1, 2, 1), (1, 2, 2),
    > (2, 1, 1), (2, 1, 2), (2, 2, 1), (2, 2, 2)]
    > ```
    > 
### Permutations with repetitions

- [generating permutations with repetitions in python - Stack Overflow](https://stackoverflow.com/questions/3099987/generating-permutations-with-repetitions-in-python)

    > You are looking for the [Cartesian Product](http://en.wikipedia.org/wiki/Cartesian_product).
    > 
    > > In mathematics, a Cartesian product (or product set) is the direct product of two sets.
    > 
    > In your case, this would be `{1, 2, 3, 4, 5, 6}` x `{1, 2, 3, 4, 5, 6}`. [`itertools`](http://docs.python.org/library/itertools.html) can help you there:
    > 
    > ```python
    > import itertools
    > x = [1, 2, 3, 4, 5, 6]
    > [p for p in itertools.product(x, repeat=2)]
    > [(1, 1), (1, 2), (1, 3), (1, 4), (1, 5), (1, 6), (2, 1), (2, 2), (2, 3),
    >  (2, 4), (2, 5), (2, 6), (3, 1), (3, 2), (3, 3), (3, 4), (3, 5), (3, 6),
    >  (4, 1), (4, 2), (4, 3), (4, 4), (4, 5), (4, 6), (5, 1), (5, 2), (5, 3),
    >  (5, 4), (5, 5), (5, 6), (6, 1), (6, 2), (6, 3), (6, 4), (6, 5), (6, 6)]
    > ```
    > 
    > To get a random dice roll (in a totally inefficient way):
    > 
    > ```python
    > import random
    > random.choice([p for p in itertools.product(x, repeat=2)])
    > (6, 3)
    > ```




# if/or/not/switch case/for/any

## if/or/not

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

### `if x is not None` or `if not x is None`

- [coding style - Python `if x is not None` or `if not x is None`? - Stack Overflow](https://stackoverflow.com/questions/2710940/python-if-x-is-not-none-or-if-not-x-is-none)

    > Both Google and [Python](http://www.python.org/dev/peps/pep-0008/#programming-recommendations)'s style guide is the best practice:
    > 
    > ```
    > if x is not None:
    >     # Do something about x
    > ```
    > 
    > Using `not x` can cause unwanted results. See below:
    > 
    > ```
    > >>> x = 1
    > >>> not x
    > False
    > >>> x = [1]
    > >>> not x
    > False
    > >>> x = 0
    > >>> not x
    > True
    > >>> x = [0]         # You don't want to fall in this one.
    > >>> not x
    > False
    > ```
    > 
    > You may be interested to see what literals are evaluated to `True` or `False` in Python:
    > 
    > -   [Truth Value Testing](http://docs.python.org/library/stdtypes.html)
    > 
    > **Edit for comment below:**
    > 
    > I just did some more testing. `not x` is None doesn't negate `x` first and then compared to `None`. In fact, it seems the `is` operator has a higher precedence when used that way:
    > 
    > ```
    > >>> x
    > [0]
    > >>> not x is None
    > True
    > >>> not (x is None)
    > True
    > >>> (not x) is None
    > False
    > ```
    > 
    > Therefore, `not x is None` is just, in my honest opinion, best avoided.
    > 
    > **More edit:**
    > 
    > I just did *more* testing and can confirm that bukzor's comment is correct. (At least, I wasn't able to prove it otherwise.)
    > 
    > This means `if x is not None` has the exact result as `if not x is None`. I stand corrected. Thanks bukzor.
    > 
    > However, my answer still stands: **Use the conventional `if x is not None`**. `:]`
    > 

## One-line if-then-else

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


## check if any condition holds (any())

- [python - Pythonic way of checking if a condition holds for any element of a list - Stack Overflow](https://stackoverflow.com/questions/1342601/pythonic-way-of-checking-if-a-condition-holds-for-any-element-of-a-list)

    > [any()](http://docs.python.org/library/functions.html#any):
    > 
    > ```python
    > if any(t < 0 for t in x):
    >     # do something
    > ```
    > 
    > Also, if you're going to use "True in ...", make it a generator expression so it doesn't take O(n) memory:
    > 
    > ```python
    > if True in (t < 0 for t in x):
    > ```





## One-line for loop

- [Python Single Line For Loops - Treehouse Blog](http://blog.teamtreehouse.com/python-single-line-loops)
    ```python
    doubled = [thing for thing in list_of_things]
    ```

## enumerate in for loop

- [Python 慣用語 - 6 善用 enumerate « Python Life](http://seanlin.logdown.com/posts/210856-python-idioms-6-enumerate)

    > ```python
    > names = ['Alice', 'Bob', 'Cindy']
    > for index, element in enumerate(names):
    >     print '%d %s' % (index, element)
    > ```


## use dict as switch

- [Replacements for switch statement in Python? - Stack Overflow](https://stackoverflow.com/questions/60208/replacements-for-switch-statement-in-python?page=2&tab=active#tab-top)

    > A combination of 2 of the solutions posted here, which is relatively easy to read and supports defaults.
    > 
    > ```python
    > result = {
    >   'a': lambda x: x * 5,
    >   'b': lambda x: x + 7,
    >   'c': lambda x: x - 2
    > }.get(whatToUse, lambda x: x - 22)(value)
    > ```
    > 
    > where
    > 
    > ```python
    > .get('c', lambda x: x - 22)(23)
    > ```
    > 
    > looks up `"lambda x: x - 2"` in the dict and uses it with `x=23`
    > 
    > ```python
    > .get('xxx', lambda x: x - 22)(44)
    > ```
    > 
    > doesn't find it in the dict and uses the default `"lambda x: x - 22"` with `x=44`.
    > 
    > ---
    > 
    > expanding on the "dict as switch" idea. if you want to use a default value for your switch:
    > 
    > ```python
    > def f(x):
    >     try:
    >         return {
    >             'a': 1,
    >             'b': 2,
    >         }[x]
    >     except KeyError:
    >         return 'default'
    > ```
    > 
    > ---
    > 
    > A solution I tend to use which also makes use of dictionaries is :
    > 
    > ```py
    > def decision_time( key, *args, **kwargs):
    >     def action1()
    >         """This function is a closure - and has access to all the arguments"""
    >         pass
    >     def action2()
    >         """This function is a closure - and has access to all the arguments"""
    >         pass
    >     def action3()
    >         """This function is a closure - and has access to all the arguments"""
    >         pass
    > 
    >    return {1:action1, 2:action2, 3:action3}.get(key,default)()
    > ```
    > 
    > This has the advantage that it doesn't try to evaluate the functions every time, and you just have to ensure that the outer function gets all the information that the inner functions need.
    > 
    >
    > 


- [Python switch case - LeetCode Playground](https://leetcode.com/playground/Vx2sL4cZ)

    <iframe src="https://leetcode.com/playground/Vx2sL4cZ/shared" frameBorder="0" width="400" height="300"></iframe>


# string operation

## replace()

- [Python String replace() Method](https://www.tutorialspoint.com/python/string_replace.htm)
    > The method **replace()** returns a copy of the string in which the occurrences of _old_ have been replaced with _new_, optionally restricting the number of replacements to _max_.

- [Python replace()方法 | 菜鸟教程](http://www.runoob.com/python/att-string-replace.html)

    > 以下实例展示了replace()函数的使用方法：
    > ```shell
    > #!/usr/bin/python str =  "this is string example....wow!!! this is really string";
    > print str.replace("is",  "was");
    > print str.replace("is",  "was",  3);
    > ```
    > 以上实例输出结果如下：
    > ```shell
    > thwas was string example....wow!!! thwas was really string 
    > thwas was string example....wow!!! thwas is really string
    > ```

### delete a character from a string

- [How to delete a character from a string using Python - Stack Overflow](https://stackoverflow.com/questions/3559559/how-to-delete-a-character-from-a-string-using-python)

    > In Python, strings are immutable, so you have to create a new string. You have a few options of how to create the new string. If you want to remove the 'M' wherever it appears:
    > 
    > ```
    > newstr = oldstr.replace("M", "")
    > ```
    > 
    > If you want to remove the central character:
    > 
    > ```
    > midlen = len(oldstr)/2
    > newstr = oldstr[:midlen] + oldstr[midlen+1:]
    > ```
    > 
    > You asked if strings end with a special character. No, you are thinking like a C programmer. In Python, strings are stored with their length, so any byte value, including `\0`, can appear in a string.

## strip()(移除頭尾字元)

- [Python strip()方法 | 菜鸟教程](http://www.runoob.com/python/att-string-strip.html)

    > 描述
    > --
    > 
    > Python strip() 方法用于移除字符串头尾指定的字符（默认为空格或换行符）或字符序列。
    > 
    > **注意：** 该方法只能删除开头或是结尾的字符，不能删除中间部分的字符。
    > 
    > ---
    > 
    > 实例
    > --
    > 
    > 以下实例展示了strip()函数的使用方法：
    > 
    > 实例(Python 2.0+)
    > ---------------
    > ```sh
    > #!/usr/bin/python  
    > # -*- coding: UTF-8 -*-  
    > 
    > str = "00000003210Runoob01230000000"; 
    > print  str.strip(  '0'  ); # 去除首尾字符 0  
    > 
    > str2 = " Runoob "; # 去除首尾空格  
    > print  str2.strip();
    > ```
    > 
    > 以上实例输出结果如下：
    > ```
    > 3210Runoob0123  Runoob
    > ```
    > 
    > 从结果上看，可以注意到中间部分的字符并未删除。
    > 
    > 以上下例演示了只要头尾包含有指定字符序列中的字符就删除：
    > 
    > 实例
    > --
    > ```
    > #!/usr/bin/python  
    > # -*- coding: UTF-8 -*-  
    > 
    > str = "123abcrunoob321"  
    > print  (str.strip(  '12'  ))  # 字符序列为 12
    > ```
    > 
    > 以上实例输出结果如下：
    > ```
    > 3abcrunoob3
    > ```



## concate strings (with + or +=)

- [Which is the preferred way to concatenate a string in Python? - Stack Overflow](https://stackoverflow.com/questions/12169839/which-is-the-preferred-way-to-concatenate-a-string-in-python)

    > The _best_ way of appending a string to a string variable is to use `+` or `+=`. This is because it's readable and fast.


## join() strings with specific characters

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



## Add leading zeroes to a string

- [Add leading zeroes to a string Python - Stack Overflow](https://stackoverflow.com/questions/39777690/add-leading-zeroes-to-a-string-python)

    > There is a built-in, the [`str.ljust()` method](https://docs.python.org/3/library/stdtypes.html#str.ljust). It takes the target width and an optional fill character (defaulting to a space). You can use it to pad out a string with `'0'` characters:
    > 
    > ```
    > val = val.ljust(8, '0')
    > ```
    > 
    > There is also an equivalent [`str.rjust()` method](https://docs.python.org/3/library/stdtypes.html#str.rjust) to add padding on the left.
    > 
    > However, if you want *leading* zeros (as opposed to trailing), I'd use the [`str.zfill()` method](https://docs.python.org/3/library/stdtypes.html#str.zfill) as that takes any `-` or `+` prefix into account.

## Split()

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
    > #!/usr/bin/python 
    > str =   "Line1-abcdef \nLine2-abc \nLine4-abcd";   
    > print str.split(   );   
    > print str.split(' ',   1   );
    > ```
    > 以上实例输出结果如下：
    > ```python
    > ['Line1-abcdef',   'Line2-abc',   'Line4-abcd']   
    > ['Line1-abcdef',   '\nLine2-abc \nLine4-abcd']
    > ```
    > 

## Convert bytes to a string

- [python - Convert bytes to a string? - Stack Overflow](https://stackoverflow.com/questions/606191/convert-bytes-to-a-string)

    > You need to decode the bytes object to produce a string:
    > 
    > ```python
    > >>> b"abcde"
    > b'abcde'
    > 
    > # utf-8 is used here because it is a very common encoding, but you
    > # need to use the encoding your data is actually in.
    > >>> b"abcde".decode("utf-8")
    > 'abcde'
    > ```


## find()

- [Python find()方法 | 菜鸟教程](http://www.runoob.com/python/att-string-find.html)

```python
>>>info = 'abca'
>>> print info.find('a')    # 从下标0开始，查找在字符串里第一个出现的子串，返回结果：0
0
>>> print info.find('a',1)  # 从下标1开始，查找在字符串里第一个出现的子串：返回结果3
3
>>> print info.find('3')    # 查找不到返回-1
-1
>>>
```

## character to a integer/integer to a character (ord()/chr())

- [How can I convert a character to a integer in Python, and viceversa? - Stack Overflow](https://stackoverflow.com/questions/704152/how-can-i-convert-a-character-to-a-integer-in-python-and-viceversa)

    > Use [`chr()`](http://docs.python.org/library/functions.html#chr) and [`ord()`](http://docs.python.org/library/functions.html#ord):
    > 
    > ```python
    > >>> chr(97)
    > 'a'
    > >>> ord('a')
    > 97
    > ```
    > 

# time

## string format time(time.strftime(), time.localtime())

- [Python 日期和时间 | 菜鸟教程](http://www.runoob.com/python/python-date-time.html)

    > ```python
    > #!/usr/bin/python
    > # -*- coding: UTF-8 -*-
    >  
    > import time
    >  
    > # 格式化成2016-03-20 11:45:39形式
    > print time.strftime("%Y-%m-%d %H:%M:%S", time.localtime()) 
    >  
    > # 格式化成Sat Mar 28 22:24:24 2016形式
    > print time.strftime("%a %b %d %H:%M:%S %Y", time.localtime()) 
    >   
    > # 将格式字符串转换为时间戳
    > a = "Sat Mar 28 22:24:24 2016"
    > print time.mktime(time.strptime(a,"%a %b %d %H:%M:%S %Y"))
    > ```
    > 

    > python中时间日期格式化符号：
    > 
    > -   %y 两位数的年份表示（00-99）
    > -   %Y 四位数的年份表示（000-9999）
    > -   %m 月份（01-12）
    > -   %d 月内中的一天（0-31）
    > -   %H 24小时制小时数（0-23）
    > -   %I 12小时制小时数（01-12）
    > -   %M 分钟数（00=59）
    > -   %S 秒（00-59）
    > -   %a 本地简化星期名称
    > -   %A 本地完整星期名称
    > -   %b 本地简化的月份名称
    > -   %B 本地完整的月份名称
    > -   %c 本地相应的日期表示和时间表示
    > -   %j 年内的一天（001-366）
    > -   %p 本地A.M.或P.M.的等价符
    > -   %U 一年中的星期数（00-53）星期天为星期的开始
    > -   %w 星期（0-6），星期天为星期的开始
    > -   %W 一年中的星期数（00-53）星期一为星期的开始
    > -   %x 本地相应的日期表示
    > -   %X 本地相应的时间表示
    > -   %Z 当前时区的名称
    > -   %% %号本身

## speed test wrapper function

- [How can I do a comparison of two lists in Python with each value? - Quora](https://www.quora.com/How-can-I-do-a-comparison-of-two-lists-in-Python-with-each-value)

    > ```python
    > import time
    > 
    > def speed_test(func):
    >     def wrapper(*args, **kwargs):
    >         t1 = time.time()
    >         for x in xrange(5000):
    >             results = func(*args, **kwargs)
    >         t2 = time.time()
    >         print '%s took %0.3f ms' % (func.func_name, (t2-t1)*1000.0)
    >         return results
    >     return wrapper
    > 
    > @speed_test
    > def compare_bitwise(x, y):
    >     set_x = frozenset(x)
    >     set_y = frozenset(y)
    >     return set_x & set_y
    > 
    > @speed_test
    > def compare_listcomp(x, y):
    >     return [i for i, j in zip(x, y) if i == j]
    > 
    > @speed_test
    > def compare_intersect(x, y):
    >     return frozenset(x).intersection(y)
    > 
    > # Comparing short lists
    > a = [1, 2, 3, 4, 5]
    > b = [9, 8, 7, 6, 5]
    > compare_bitwise(a, b)
    > compare_listcomp(a, b)
    > compare_intersect(a, b)
    > 
    > # Comparing longer lists
    > import random
    > a = random.sample(xrange(100000), 10000)
    > b = random.sample(xrange(100000), 10000)
    > compare_bitwise(a, b)
    > compare_listcomp(a, b)
    > compare_intersect(a, b)
    > ```

## make a time delay 

- [How can I make a time delay in Python? - Stack Overflow](https://stackoverflow.com/questions/510348/how-can-i-make-a-time-delay-in-python)


    > There are 5 methods which I know: `time.sleep()`, `pygame.time.wait()`, matplotlib's `pyplot.pause()`, `.after()`, and `driver.implicitly_wait()`.
    > 
    > * * * * *
    > 
    > `time.sleep()` example (do not use if using Tkinter):
    > 
    > ```python
    > import time
    > print('Hello')
    > time.sleep(5) #number of seconds
    > print('Bye')
    > ```
    > 
    > * * * * *
    > 
    > `pygame.time.wait()` example (not recommended if you are not using the pygame window, but you could exit the window instantly):
    > 
    > ```python
    > import pygame
    > #If you are going to use the time module
    > #don't do "from pygame import *"
    > pygame.init()
    > print('Hello')
    > pygame.time.wait(5000)#milliseconds
    > print('Bye')
    > ```
    > 
    > * * * * *
    > 
    > matplotlib's function `pyplot.pause()` example (not recommended if you are not using the graph, but you could exit the graph instantly):
    > 
    > ```python
    > import matplotlib
    > print('Hello')
    > matplotlib.pyplot.pause(5)#seconds
    > print('Bye')
    > ```
    > 
    > * * * * *
    > 
    > The `.after()` method (best with Tkinter):
    > 
    > ```python
    > import tkinter as tk #Tkinter for python 2
    > root = tk.Tk()
    > print('Hello')
    > def ohhi():
    >  print('Oh, hi!')
    > root.after(5000, ohhi)#milliseconds and then a function
    > print('Bye')
    > ```
    > 
    > * * * * *
    > 
    > Finally, the `driver.implicitly_wait()` method (selenium):
    > 
    > ```python
    > driver.implicitly_wait(5)#waits 5 seconds
    > enter code here
    > ```
    > 


# list, dict, range, sort, zip, tuple, unpack

## create a list and initialize with same values

- [Python : How to create a list and initialize with same values – thispointer.com](https://thispointer.com/python-how-to-create-a-list-and-initialize-with-same-values/)

    > Creating a list of same values by [] and multiply
    > -------------------------------------------------
    > 
    > Suppose we want to create a list of strings, which contains 20 same strings i.e. 'Hi'
    > ```
    > ['Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi']
    > ```
    > 
    > Let's see how to do that i.e.
    > ```
    > ''' create a list by [] and multiply by repeat count ''' 
    > 
    > listOfStrings1 = ['Hi'] * 20
    > ```
    > 
    > ['Hi'] will create a list with single value, then we can multiply this list by 20. It will repeat the contents of list 20 times.
    > 
    > So, lists content will be now i.e.
    > ```
    > ['Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi']
    > ```
    > 
    > Creating a list of same values by List Comprehension with range()
    > -----------------------------------------------------------------
    > 
    > This is an another way to create a list of same value using range() i.e.
    > 
    > ```
    > '''
    >     Use List Comprehension with range() to initialize a list by 20 elements 0
    >     It will iterate over the tange from 0 to 20 and for
    >     each entry, it will add 'Hi' to the list and in the end
    >     returns the list to listOfNums
    > '''
    > 
    > listOfStrings2  =  ['Hi'  for  i  in  range(20)]
    > ```
    > 
    > In this list comprehension, for loop will iterate over the range object 20 times and in each iteration it will add 'Hi' in the list.\
    > So, list will coatain 20 'Hi' elements i.e.
    > ```
    > ['Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi', 'Hi']
    > ```


## list initialization using multiple range statements

- [Python list initialization using multiple range statements - Stack Overflow](https://stackoverflow.com/questions/13959510/python-list-initialization-using-multiple-range-statements)

    > Try this for Python 2.x:
    > 
    > ```
    >  range(1,6) + range(15,20)
    > ```
    > 
    > Or if you're using Python3.x, try this:
    > 
    > ```
    > list(range(1,6)) + list(range(15,20))
    > ```
    > 
    > For dealing with elements in-between, for Python 2.x:
    > 
    > ```
    > range(101,6284) + [8001,8003,8010] + range(10000,12322)
    > ```
    > 
    > And finally for dealing with elements in-between, for Python 3.x:
    > 
    > ```
    > list(range(101,6284)) + [8001,8003,8010] + list(range(10000,12322))
    > ```


## indexing & slicing

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

    > and a\[::-1\] to reverse a string. – [Christopher Mahan](https://stackoverflow.com/users/479/christopher-mahan "5,181 reputation") [Feb 3 '09 at 23:54](https://stackoverflow.com/questions/509211/understanding-pythons-slice-notation#comment323779_509295)

    > Also can be important that `[:]` returns a [`shallow copy`](http://docs.python.org/2/library/copy.html) of a list. it means that every slice notation returns a list which have new address in memory, but its elements would have same addresses that elements of source list have. – [Gill Bates](https://stackoverflow.com/users/1818608/gill-bates "1,959 reputation") [Dec 30 '12 at 17:07](https://stackoverflow.com/questions/509211/understanding-pythons-slice-notation#comment19491969_509295)


### what `a[:-1]`, `a[::-1]` and `a[:-1:-1]` does

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

### reverse list

- [How can I reverse a list in Python? - Stack Overflow](https://stackoverflow.com/questions/3940128/how-can-i-reverse-a-list-in-python)

    > ```python
    > >>> L = [0,10,20,40]
    > >>> L[::-1]
    > [40, 20, 10, 0]
    > ```

## turn range() to list

- [Python 3 turn range to a list - Stack Overflow](https://stackoverflow.com/questions/11480042/python-3-turn-range-to-a-list)

    > In Pythons <= 3.4 you can, as others suggested, use list(range(10)) in order to make a list out of a range (In general, any iterable).
    > 
    > Another alternative, introduced in Python 3.5 with its unpacking generalizations, is by using * in a list literal []:
    > 
    > ```python
    > >>> r = range(10)
    > >>> l = [*r]
    > >>> print(l)
    > [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    > ```
    > 
    > ---
    > 
    > You really shouldn't need to use the numbers 1-1000 in a list. But if for some reason you really do need these numbers, then you could do:
    > 
    > ```python
    > [i for i in range(1, 1001)]
    > ```
    > 

### range(start, stop[, step])

- [Python range() 函数 | 菜鸟教程](http://www.runoob.com/python/python-func-range.html)

    > range(start, stop[, step])
    > 
    > 参数说明：
    > 
    > -   start: 计数从 start 开始。默认是从 0 开始。例如range（5）等价于range（0， 5）;
    > -   stop: 计数到 stop 结束，但不包括 stop。例如：range（0， 5） 是[0, 1, 2, 3, 4]没有5
    > -   step：步长，默认为1。例如：range（0， 5） 等价于 range(0, 5, 1)
    > 


## list append/merge

- [What is the syntax to insert one list into another list in python? - Stack Overflow](https://stackoverflow.com/questions/3748063/what-is-the-syntax-to-insert-one-list-into-another-list-in-python)

    > Do you mean `append`?
    > 
    > ```py
    > >>> x = [1,2,3]
    > >>> y = [4,5,6]
    > >>> x.append(y)
    > >>> x
    > [1, 2, 3, [4, 5, 6]]
    > ```
    > 
    > Or merge?
    > 
    > ```py
    > >>> x = [1,2,3]
    > >>> y = [4,5,6]
    > >>> x + y
    > [1, 2, 3, 4, 5, 6]
    > >>> x.extend(y)
    > >>> x
    > [1, 2, 3, 4, 5, 6]
    > ```
    > 

## Finding the index of an item 

- [Finding the index of an item given a list containing it in Python - Stack Overflow](https://stackoverflow.com/questions/176918/finding-the-index-of-an-item-given-a-list-containing-it-in-python)

    > ```python
    > >>> ["foo", "bar", "baz"].index("bar")
    > 1
    > ```
    > ---
    > 
    > The majority of answers explain how to find **a single index**, but their methods do not return multiple indexes if the item is in the list multiple times. Use [`enumerate()`](https://docs.python.org/3.6/library/functions.html#enumerate):
    > 
    > ```python
    > for i, j in enumerate(['foo', 'bar', 'baz']):
    >     if j == 'bar':
    >         print(i)
    > ```
    > 
    > The `index()` function only returns the first occurrence, while `enumerate()` returns all occurrences.
    > 
    > As a list comprehension:
    > 
    > ```python
    > [i for i, j in enumerate(['foo', 'bar', 'baz']) if j == 'bar']
    > ```
    > 
    > * * * * *
    > 
    > Here's also another small solution with [`itertools.count()`](http://docs.python.org/2/library/itertools.html#itertools.count) (which is pretty much the same approach as enumerate):
    > 
    > ```python
    > from itertools import izip as zip, count # izip for maximum efficiency
    > [i for i, j in zip(count(), ['foo', 'bar', 'baz']) if j == 'bar']
    > ```
    > 
    > This is more efficient for larger lists than using `enumerate()`:
    > 
    > ```shell
    > $ python -m timeit -s "from itertools import izip as zip, count" "[i for i, j in zip(count(), ['foo', 'bar', 'baz']*500) if j == 'bar']"
    > 10000 loops, best of 3: 174 usec per loop
    > $ python -m timeit "[i for i, j in enumerate(['foo', 'bar', 'baz']*500) if j == 'bar']"
    > 10000 loops, best of 3: 196 usec per loop
    > ```

## compare each item in a list with the rest

- [python - How to compare each item in a list with the rest, only once? - Stack Overflow](https://stackoverflow.com/questions/16603282/how-to-compare-each-item-in-a-list-with-the-rest-only-once)


    > Of course this will generate each pair twice as each `for` loop will go through every item of the list.
    > 
    > You could use some [itertools](http://docs.python.org/3/library/itertools.html) magic here to generate all possible combinations:
    > 
    > ```
    > import itertools
    > for a, b in itertools.combinations(mylist, 2):
    >     compare(a, b)
    > ```
    > 
    > [`itertools.combinations`](http://docs.python.org/3/library/itertools.html#itertools.combinations) will pair each element with each other element in the iterable, but only once.
    > 
    > * * * * *
    > 
    > You could still write this using index-based item access, equivalent to what you are used to, using nested `for` loops:
    > 
    > ```
    > for i in range(len(mylist)):
    >     for j in range(i + 1, len(mylist)):
    >         compare(mylist[i], mylist[j])
    > ```
    > 
    > Of course this may not look as nice and pythonic but sometimes this is still the easiest and most comprehensible solution, so you should not shy away from solving problems like that.
    > 
    > ---
    > 
    > If you want index, just add `index=range(len(mylist))` and `for a, b in itertools.combinations(index, 2):` then `compare(mylist[a], mylist[b])`. Now you can use the index to get the element from `mylist`. -- [allenyllee](https://stackoverflow.com/users/1851492/allenyllee "121 reputation") [just now](https://stackoverflow.com/questions/16603282/how-to-compare-each-item-in-a-list-with-the-rest-only-once#comment94547146_16603357)
    > 


## remove items from a list while iterating (loop backward: range(N-1,-1,-1))

- [python - How to remove items from a list while iterating? - Stack Overflow](https://stackoverflow.com/questions/1207406/how-to-remove-items-from-a-list-while-iterating)

    > ```python
    > for i in range(len(somelist) - 1, -1, -1):
    >     if some_condition(somelist, i):
    >         del somelist[i]
    > ```
    > 
    > You need to go backwards otherwise it's a bit like sawing off the tree-branch that you are sitting on :-)
    > 

## remove an element from a list by index (pop())

- [How do I remove an element from a list by index in Python? - Stack Overflow](https://stackoverflow.com/questions/627435/how-do-i-remove-an-element-from-a-list-by-index-in-python)

    > You probably want `pop`:
    > 
    > ```
    > a = ['a', 'b', 'c', 'd']
    > a.pop(1)
    > 
    > # now a is ['a', 'c', 'd']
    > ```
    > 
    > By default, `pop` without any arguments removes the last item:
    > 
    > ```
    > a = ['a', 'b', 'c', 'd']
    > a.pop()
    > 
    > # now a is ['a', 'b', 'c']
    > ```

## unpack list (*my_list)

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
    list = [1, 2, 3, 4]
    a, b, *rest = list
    ```
    
    __Catch-all unpacking in Python 2.x__

    ```python
    list = [1, 2, 3, 4]
    (a, b), rest = list[:2], list[2:] # The first and second elements are in
    ```
## unpack list to zip to make transpose

- [程式扎記: [ Python 文章收集 ] Python 中 zip() 函數用法實例教程](https://puremonkey2010.blogspot.com/2015/10/python-python-zip.html)

    > ```py
    > >>> zip(*a)
    > [(1, 4, 7), (2, 5, 8), (3, 6, 9)]
    > >>> map(list,zip(*a))
    > [[1, 4, 7], [2, 5, 8], [3, 6, 9]]
    > ```
    > 
    > 這種方法速度更快但也更難以理解，將 list 看成tuple解壓，恰好得到我們「行列互換」的效果，再通過對每個元素應用 [list()](https://docs.python.org/2/library/functions.html#list) 函數，將 tuple 轉換為 list
    > 


## get list from iterator object 

- [Zip lists in Python - Stack Overflow](https://stackoverflow.com/questions/13704860/zip-lists-in-python)

    > In **Python 3** `zip` returns an iterator instead and needs to be passed to a list function to get the zipped tuples:
    > 
    > ```py
    > x = [1, 2, 3]; y = ['a','b','c']
    > z = zip(x, y)
    > z = list(z)
    > print(z)
    > >>> [(1, 'a'), (2, 'b'), (3, 'c')]
    > ```
    > 
    > Then to `unzip` them back just conjugate the zipped iterator:
    > 
    > ```py
    > x_back, y_back = zip(*z)
    > print(x_back); print(y_back)
    > >>> (1, 2, 3)
    > >>> ('a', 'b', 'c')
    > ```
    > 
    > If the original form of list is needed instead of tuples:
    > 
    > ```py
    > x_back, y_back = zip(*z)
    > print(list(x_back)); print(list(y_back))
    > >>> [1,2,3]
    > >>> ['a','b','c']
    > ```
    > 

## sort vs. sorted

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

### sort (list/tuple) of lists/tuples

- [python - How to sort (list/tuple) of lists/tuples? - Stack Overflow](https://stackoverflow.com/questions/3121979/how-to-sort-list-tuple-of-lists-tuples)

    > ```python
    > sorted_by_second = sorted(data, key=lambda tup: tup[1])
    > ```
    > 
    > or:
    > 
    > ```python
    > data.sort(key=lambda tup: tup[1])  # sorts in place
    > ```

## Add new keys to a dictionary

- [python - Add new keys to a dictionary? - Stack Overflow](https://stackoverflow.com/questions/1024847/add-new-keys-to-a-dictionary)

    > ```python
    > >>> d = {'key':'value'}
    > >>> print(d)
    > {'key': 'value'}
    > >>> d['mynewkey'] = 'mynewvalue'
    > >>> print(d)
    > {'mynewkey': 'mynewvalue', 'key': 'value'}
    > ```


## convert list to string (join())

- [python - How to convert list to string - Stack Overflow](https://stackoverflow.com/questions/5618878/how-to-convert-list-to-string)

    > By using `''.join`
    > 
    > ```python
    > list1 = ['1', '2', '3']
    > str1 = ''.join(list1)
    > ```
    > 
    > Or if the list is of integers, convert the elements before joining them.
    > 
    > ```pyton
    > list1 = [1, 2, 3]
    > str1 = ''.join(str(e) for e in list1)
    > ```

# set

## compare two lists( set().intersection() )

- [How can I compare two lists in python and return matches - Stack Overflow](https://stackoverflow.com/questions/1388818/how-can-i-compare-two-lists-in-python-and-return-matches)

    > Not the most efficient one, but by far the most obvious way to do it is:
    > 
    > ```python
    > >>> a = [1, 2, 3, 4, 5]
    > >>> b = [9, 8, 7, 6, 5]
    > >>> set(a) & set(b)
    > {5}
    > ```
    > 
    > if order is significant you can do it with list comprehensions like this:
    > 
    > ```python
    > >>> [i for i, j in zip(a, b) if i == j]
    > [5]
    > ```
    > 
    > (only works for equal-sized lists, which order-significance implies).
    > 
    > ---
    > 
    > 
    > Use [set.intersection()](http://docs.python.org/library/stdtypes.html#set.intersection), it's fast and readable.
    > 
    > ```python
    > >>> set(a).intersection(b)
    > set([5])
    > ```
    > 
    > ---
    > 
    > This answer has good algorithmic performance, as only one of the lists (shorter should be preferred) is turned into a set for quick lookup, and the other list is traversed looking up its items in the set. -- [u0b34a0f6ae](https://stackoverflow.com/users/137317/u0b34a0f6ae "31,600 reputation") [Sep 7 '09 at 12:08](https://stackoverflow.com/questions/1388818/how-can-i-compare-two-lists-in-python-and-return-matches#comment1229439_1388842)
    > 
    > ---
    > 
    > `bool(set(a).intersection(b))` for `True` or `False` -- [Akshay](https://stackoverflow.com/users/3782963/akshay "745 reputation") [Oct 20 '17 at 3:20](https://stackoverflow.com/questions/1388818/how-can-i-compare-two-lists-in-python-and-return-matches#comment80631587_1388842)
    > 



# enumerations

- [enum — Support for enumerations — Python 3.7.1 documentation](https://docs.python.org/3/library/enum.html)

    > The [`Enum`](https://docs.python.org/3/library/enum.html#enum.Enum "enum.Enum") class is callable, providing the following functional API:
    > ```python
    > >>> Animal = Enum('Animal', 'ANT BEE CAT DOG')
    > >>> Animal
    > <enum 'Animal'>
    > >>> Animal.ANT
    > <Animal.ANT: 1>
    > >>> Animal.ANT.value
    > 1
    > >>> list(Animal)
    > [<Animal.ANT: 1>, <Animal.BEE: 2>, <Animal.CAT: 3>, <Animal.DOG: 4>]
    > ```
    > 
    > ---
    > 
    > The complete signature is:
    > 
    > ```
    > Enum(value='NewEnumName', names=<...>, *, module='...', qualname='...', type=<mixed-in class>, start=1)
    > ```
    > 
    > | value:    | What the new Enum class will record as its name.                                                                                                                                                                                                                                                                                                                                                  |
    > |-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    > | names:    | The Enum members.  This can be a whitespace or comma separated string (values will start at 1 unless otherwise specified):  
    > ||'RED GREEN BLUE' \| 'RED,GREEN,BLUE' \| 'RED, GREEN, BLUE'  
    > ||or an iterator of names:  
    > ||['RED', 'GREEN', 'BLUE']  
    > ||or an iterator of (name, value) pairs:  
    > ||[('CYAN', 4), ('MAGENTA', 5), ('YELLOW', 6)]  
    > ||or a mapping:  
    > ||{'CHARTREUSE': 7, 'SEA_GREEN': 11, 'ROSEMARY': 42} |
    > | module:   | name of module where new Enum class can be found.                                                                                                                                                                                                                                                                                                                                                 |
    > | qualname: | where in module new Enum class can be found.                                                                                                                                                                                                                                                                                                                                                      |
    > | type:     | type to mix in to new Enum class.                                                                                                                                                                                                                                                                                                                                                                 |
    > | start:    | number to start counting at if only names are passed in.                                                                                                                                                                                                                                                                                                                                          |
    > 


## enumerate()

- [Python enumerate() 函数 | 菜鸟教程](http://www.runoob.com/python/python-func-enumerate.html)

    > enumerate() 函数用于将一个可遍历的数据对象(如列表、元组或字符串)组合为一个索引序列，同时列出数据和数据下标，一般用在 for 循环当中。
    > 
    > Python 2.3. 以上版本可用，2.6 添加 start 参数。
    > 
    > ---
    > 
    > 以下展示了使用 enumerate() 方法的实例：
    > ```python
    > >>> seasons = ['Spring', 'Summer', 'Fall', 'Winter'] 
    > >>> list(enumerate(seasons))  
    > [(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')] 
    > >>> list(enumerate(seasons, start=1))  # 下标从 1 开始  
    > [(1, 'Spring'), (2, 'Summer'), (3, 'Fall'), (4, 'Winter')]
    > ```
    > 
    > ---
    > 
    > for 循环使用 enumerate
    > ------------------
    > ```python
    > >>> seq = ['one', 'two', 'three'] 
    > >>> for  i, element  in  enumerate(seq): 
    > ... print  i, element 
    > ... 
    > >>> 0  one  
    > >>> 1  two  
    > >>> 2  three
    > ```

### How to enumerate a range of numbers starting at 1

- [python - How to enumerate a range of numbers starting at 1 - Stack Overflow](https://stackoverflow.com/questions/3303608/how-to-enumerate-a-range-of-numbers-starting-at-1)

    > As you already mentioned, this is straightforward to do in Python 2.6 or newer:
    > 
    > ```
    > enumerate(range(2000, 2005), 1)
    > ```
    > 
    > Python 2.5 and older do not support the `start` parameter so instead you could create two range objects and zip them:
    > 
    > ```
    > r = xrange(2000, 2005)
    > r2 = xrange(1, len(r) + 1)
    > h = zip(r2, r)
    > print h
    > ```
    > 
    > Result:
    > 
    > [(1, 2000), (2, 2001), (3, 2002), (4, 2003), (5, 2004)]
    > 
    > If you want to create a generator instead of a list then you can use [izip](http://docs.python.org/library/itertools.html#itertools.izip) instead.


# os operation

## get Kernel path

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

## get command output

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


# with...as...

## open file with...as...

- [icodding愛程式: python 研究-with as 用法](https://icodding.blogspot.tw/2016/05/python-with-as.html)

    > 有一些任務，可能事先需要設置，事後做清理工作。對於這種場景，Python的with語句提供了一種非常方便的處理方式。一個很好的例子是文件處理，你需要獲取一個文件句柄，從文件中讀取資料，然後關閉文件句柄。  
    > 
    > 如果不用with語句，程式碼如下：  
    > 
    > ```python=
    > file = open("/tmp/foo.txt")  
    > data = file.read()  
    > file.close()  
    > ```
    > 
    > 這裡有兩個問題:  
    > 
    > 一是可能忘記關閉文件句柄；  
    > 二是文件讀取資料發生異常，沒有進行任何處理。  
    > 
    > 下面是處理異常的加強版本：  
    > 
    > ```python=
    > try:  
    >     f = open('xxx')  
    > except:  
    >     print 'fail to open'  
    >     exit(-1)  
    > try:  
    >     do something  
    > except:  
    >     do something  
    > finally:  
    >     f.close()  
    > ```
    > 
    > 雖然這段程式碼執行良好，但是太冗長了。  
    > 
    > 這時候就是with一展身手的時候了。除了有更優雅的語法，with還可以很好的處理上下文環境產生的異常。  
    > 
    > 下面是with版本的程式碼：  
    > 
    > ```python=
    > with open("/tmp/foo.txt") as file:  
    >     data = file.read()  
    > ```
    > 
    > with如何工作?  
    > 
    > 緊跟with後面的語句被求值後，返回物件的 \_\_enter\_\_() 方法被呼叫，這個方法的返回值將被賦值給as後面的變數。  
    > 當with後面的程式碼塊全部被執行完之後，將呼叫前面返回物件的 \_\_exit\_\_()方法。  
    > 
    > 下面例子可以具體說明with如何工作：  
    > 
    > ```python=
    > #!/usr/bin/env python  
    > # with_example01.py  
    > class Sample:  
    >     def __enter__(self):  
    >         print "In __enter__()"  
    >         return "Foo"  
    >     def __exit__(self, type, value, trace):  
    >         print "In __exit__()"  
    >         
    > def get_sample():  
    >     return Sample()  
    > with get_sample() as sample:  
    >     print "sample:", sample  
    > ```
    > 
    > 執行程式碼，輸出如下  
    > 
    > ```shell=
    > bash-3.2$ ./with_example01.py  
    > In __enter__()  
    > sample: Foo  
    > In __exit__()  
    > ```
    > 
    > 正如你看到的: 1\. \_\_enter\_\_()方法被執行 2. \_\_enter\_\_()方法返回的值 - 這個例子中是」Foo」，賦值給變數』sample' 3. 執行程式碼塊，列印變數」sample」的值為 「Foo」 4. \_\_exit\_\_()方法被呼叫 with真正強大之處是它可以處理異常。
    > 
    > ---
    > 
    > 可能你已經注意到Sample類的 \_\_exit\_\_ 方法有三個參數 val, type 和 trace。 這些參數在異常處理中相當有用。我們來改一下程式碼，看看具體如何工作的。
    > ```python=
    > #!/usr/bin/env python
    > # with_example02.py
    > class Sample:
    >     def __enter__(self):
    >         return self
    >     def __exit__(self, type, value, trace):
    >         print "type:", type
    >         print "value:", value
    >         print "trace:", trace
    >     def do_something(self):
    >         bar = 1/0
    >         return bar + 10
    > with Sample() as sample:
    >     sample.do_something()
    > ```
    > 
    > 這個例子中，with後面的get_sample()變成了Sample()。這沒有任何關係，只要緊跟with後面的語句所返回的物件有 \_\_enter\_\_() 和 \_\_exit\_\_() 方法即可。此例中，Sample()的 \_\_enter\_\_() 方法返回新新增的Sample物件，並賦值給變數sample。
    > 
    > 程式碼執行後：
    > ```shell=
    > bash-3.2$ ./with_example02.py
    > type: <type 'exceptions.ZeroDivisionError'>
    > value: integer division or modulo by zero
    > trace: <traceback object at 0x1004a8128>
    > Traceback (most recent call last):
    >   File "./with_example02.py", line 19, in <module>
    >     sample.do_something()
    >   File "./with_example02.py", line 15, in do_something
    >     bar = 1/0
    > ZeroDivisionError: integer division or modulo by zero
    > ```
    > 實際上，在with後面的程式碼塊拋出任何異常時，\_\_exit\_\_() 方法被執行。正如例子所示，異常拋出時，與之關聯的type，value和stack trace傳給 \_\_exit\_\_() 方法，因此拋出的ZeroDivisionError異常被列印出來了。開發庫時，清理資源，關閉文件等等操作，都可以放在 \_\_exit\_\_ 方法當中。
    > 
    > 另外，\_\_exit\_\_ 除了用於tear things down，還可以進行異常的監控和處理，注意後幾個參數。要跳過一個異常，只需要返回該函數True即可。
    > 
    > 下面的樣例程式碼跳過了所有的TypeError，而讓其他異常正常拋出。
    > ```python
    > def __exit__(self, type, value, traceback):
    >     return isinstance(value, TypeError)
    > ```
    > 
    > ---
    > 
    > 上文說了 \_\_exit\_\_ 函數可以進行部分異常的處理，如果我們不在這個函數中處理異常，他會正常拋出，這時候我們可以這樣寫（python 2.7及以上版本，之前的版本參考使用contextlib.nested這個庫函數）：  
    > 
    > ```python=
    > try:  
    >     with open( "a.txt" ) as f :  
    >         do something  
    > except xxxError:  
    >     do something about exception  
    > ```
    > 
    > 總之，with-as表達式極大的簡化了每次寫finally的工作，這對保持程式碼的優雅性是有極大幫助的。  
    > 
    > 如果有多個項，我們可以這麼寫：  
    > 
    > ```python=
    > with open("x.txt") as f1, open('xxx.txt') as f2:  
    >     do something with f1,f2
    > ```

- [What is the python keyword "with" used for? - Stack Overflow](https://stackoverflow.com/questions/1369526/what-is-the-python-keyword-with-used-for)

    > The `with` statement is a control-flow structure whose basic structure is:
    > 
    > ```python=
    > with expression [as variable]:
    >     with-block
    > ```
    > 
    > The expression is evaluated, and it should result in an object that supports the context management protocol (that is, has `__enter__()` and `__exit__()` methods).


## AttributeError: \_\_exit\_\_

- [How to troubleshoot an "AttributeError: \_\_exit\_\_" in multiproccesing in Python? - Stack Overflow](https://stackoverflow.com/questions/7447284/how-to-troubleshoot-an-attributeerror-exit-in-multiproccesing-in-python)

    > The problem is in this line:
    > 
    > ```python
    > with pattern.findall(row) as f:
    > ```
    > 
    > You are using the `with` statement. It requires an object with `__enter__` and `__exit__` methods. But `pattern.findall` returns a `list`, `with` tries to store the `__exit__` method, but it can't find it, and raises an error. Just use
    > 
    > ```python
    > f = pattern.findall(row)
    > ```
    > 
    > instead.


# file operation

## open()

### open(): TypeError: an integer is required (got type str)

- [Python对文件的读取问题_百度知道](https://zhidao.baidu.com/question/304077298629576884.html)

    > ```
    > open(...)
    >     open(name[, mode[, buffering]]) -> file object
    >      
    >     Open a file using the file() type, returns a file object.  This is the
    >     preferred way to open a file.  See file.__doc__ for further information.
    > ```
    > open这个函数的第三个参数不是用来接收编码方式的，而是传入一个buffering的值，你传入了'utf-8'字符串所以系统让你传一个整型
    > TypeError: an integer is required (got type str)
    > 
    > ---
    > 
    > 改用 `encoding='utf8'` 即可[name=Ya-Lun Li]


### reading from a file and saving to utf-8

- [Python reading from a file and saving to utf-8 - Stack Overflow](https://stackoverflow.com/questions/19591458/python-reading-from-a-file-and-saving-to-utf-8)

    > Process text to and from Unicode at the I/O boundaries of your program using the `codecs` module:
    > 
    > ```python
    > import codecs
    > with codecs.open(filename,'r',encoding='utf8') as f:
    >     text = f.read()
    > # process Unicode text
    > with codecs.open(filename,'w',encoding='utf8') as f:
    >     f.write(text)
    > ```
    > 
    > **Edit:** The `io` module is now recommended instead of codecs and is compatible with Python 3's `open` syntax:
    > 
    > ```python
    > import io
    > with io.open(filename,'r',encoding='utf8') as f:
    >     text = f.read()
    > # process Unicode text
    > with io.open(filename,'w',encoding='utf8') as f:
    >     f.write(text)
    > ```


## read file(read()/readline()/readlines())

- [python中的三个读read(),readline()和readlines() - CSDN博客](https://blog.csdn.net/werm520/article/details/6898473)
    > .read() 每次读取整个文件，它通常用于将文件内容放到一个字符串变量中。然而 .read() 生成文件内容最直接的字符串表示，但对于连续的面向行的处理，它却是不必要的，并且如果文件大于可用内存，则不可能实现这种处理。

    >.readline() 和 .readlines()之间的差异是后者一次读取整个文件，象 .read()一样。.readlines()自动将文件内容分析成一个行的列表，该列表可以由 Python 的 for... in ... 结构进行处理。另一方面，.readline()每次只读取一行，通常比 .readlines()慢得多。仅当没有足够内存可以一次读取整个文件时，才应该使用.readline()。

- [string - In Python, how do I read a file line-by-line into a list? - Stack Overflow](https://stackoverflow.com/questions/3277503/in-python-how-do-i-read-a-file-line-by-line-into-a-list)

    > ```python
    > with open(fname) as f:
    >     content = f.readlines()
    > # you may also want to remove whitespace characters like `\n` at the end of each line
    > content = [x.strip() for x in content]
    > ```

### Read entire file

- [Reading entire file in Python - Stack Overflow](https://stackoverflow.com/questions/7409780/reading-entire-file-in-python)

    > A better solution, to make sure that the file is closed, is this pattern:
    > 
    > ```py
    > with open('Path/to/file', 'r') as content_file:
    >     content = content_file.read()
    > ```
    > 
    > which will always close the file immediately after the block ends; even if an exception occurs.

## write file

- [Python Print String To Text File - Stack Overflow](https://stackoverflow.com/questions/5214578/python-print-string-to-text-file)
    
    > ```py
    > text_file = open("Output.txt", "w")
    > text_file.write("Purchase Amount: %s" % TotalAmount)
    > text_file.close()
    > ```
    > 
    > If you use a context manager, the file is closed automatically for you
    > 
    > ```py
    > with open("Output.txt", "w") as text_file:
    >     text_file.write("Purchase Amount: %s" % TotalAmount)
    > ```
    > 
    > If you're using Python2.6 or higher, it's preferred to use `str.format()`
    > 
    > ```py
    > with open("Output.txt", "w") as text_file:
    >     text_file.write("Purchase Amount: {0}".format(TotalAmount))
    > ```
    > 
    > For python2.7 and higher you can use `{}` instead of `{0}`
    > 
    > In Python3, there is an optional `file` parameter to the `print` function
    > 
    > ```py
    > with open("Output.txt", "w") as text_file:
    >     print("Purchase Amount: {}".format(TotalAmount), file=text_file)
    > ```
    > 
    > Python3.6 introduced [f-strings](https://docs.python.org/3/whatsnew/3.6.html#pep-498-formatted-string-literals) for another alternative
    > 
    > ```py
    > with open("Output.txt", "w") as text_file:
    >     print(f"Purchase Amount: {TotalAmount}", file=text_file)
    > ```
    > 
    > ---
    > 
    > In case you want to pass multiple arguments you can use a tuple
    > 
    > ```py
    > price = 33.3
    > with open("Output.txt", "w") as text_file:
    >     text_file.write("Purchase Amount: %s price %f" % (TotalAmount, price))
    > ```
    > 
    > More: [Print multiple arguments in python](https://stackoverflow.com/questions/15286401/print-multiple-arguments-in-python)

### Writing a list to a file with newline ("\n".join(...))

- [Writing a list to a file with Python - Stack Overflow](https://stackoverflow.com/questions/899103/writing-a-list-to-a-file-with-python)

    > The best way is:
    > 
    > ```
    > outfile.write("\n".join(itemlist))
    > ```

## copy file

- [How do I copy a file in python? - Stack Overflow](https://stackoverflow.com/questions/123198/how-do-i-copy-a-file-in-python)


    > [`copy2(src,dst)`](https://docs.python.org/2/library/shutil.html#shutil.copy2) is often more useful than [`copyfile(src,dst)`](https://docs.python.org/2/library/shutil.html#shutil.copyfile) because:
    > 
    > -   it allows `dst` to be a *directory* (instead of the complete target filename), in which case the [basename](https://docs.python.org/2/library/os.path.html#os.path.basename) of `src` is used for creating the new file;
    > -   it preserves the original modification and access info (mtime and atime) in the file metadata (however, this comes with a slight overhead).
    > 
    > Here is a short example:
    > 
    > ```py
    > import shutil
    > shutil.copy2('/src/dir/file.ext', '/dst/dir/newname.ext') # complete target filename given
    > shutil.copy2('/src/file.ext', '/dst/dir') # target filename is /dst/dir/file.ext
    > ```

## parsing json file

- [python - Parsing values from a JSON file? - Stack Overflow](https://stackoverflow.com/questions/2835559/parsing-values-from-a-json-file)

    > ```py
    > import json
    > from pprint import pprint
    > 
    > with open('data.json') as f:
    >     data = json.load(f)
    > 
    > pprint(data)
    > ```
    > 
    > With data, you can now also find values like so:
    > 
    > ```py
    > data["maps"][0]["id"]
    > data["masks"]["id"]
    > data["om_points"]
    > ```
    > 

## write to excel file

- [Python - Write to Excel Spreadsheet - Stack Overflow](https://stackoverflow.com/questions/13437727/python-write-to-excel-spreadsheet)

    > Use [DataFrame.to_excel](http://pandas.pydata.org/pandas-docs/dev/generated/pandas.DataFrame.to_excel.html) from [pandas](https://github.com/pydata/pandas). Pandas allows you to represent your data in functionally rich datastructures and will let you [read in](http://pandas.pydata.org/pandas-docs/stable/io.html#excel-files) excel files as well.
    > 
    > You will first have to convert your data into a DataFrame and then save it into an excel file like so:
    > 
    > ```
    > In [1]: from pandas import DataFrame
    > In [2]: l1 = [1,2,3,4]
    > In [3]: l2 = [1,2,3,4]
    > In [3]: df = DataFrame({'Stimulus Time': l1, 'Reaction Time': l2})
    > In [4]: df
    > Out[4]:
    >    Reaction Time  Stimulus Time
    > 0              1              1
    > 1              2              2
    > 2              3              3
    > 3              4              4
    > 
    > In [5]: df.to_excel('test.xlsx', sheet_name='sheet1', index=False)
    > ```
    > 
    > and the excel file that comes out looks like this:
    > 
    > ![enter image description here](https://i.stack.imgur.com/RXFGb.png)
    > 
    > Note that both lists need to be of equal length else pandas will complain. To solve this, replace all missing values with `None`.



## create new dir

- [python - How to create new folder? - Stack Overflow](https://stackoverflow.com/questions/1274405/how-to-create-new-folder)

    > You can create a folder with [os.makedirs()](http://docs.python.org/3/library/os.html?highlight=os.makedirs#os.makedirs)\
    > and use [os.path.exists()](http://docs.python.org/3/library/os.path.html?highlight=os.path.exists#os.path.exists) to see if it already exists:
    > 
    > ```py
    > newpath = r'C:\Program Files\arbitrary'
    > if not os.path.exists(newpath):
    >     os.makedirs(newpath)
    > ```
    > 
    > ---
    > 
    > do `os.path.join('dir','other-dir')` instead of `dir\other-dir` if you want to be compatible with stuff besides windows.
    > 

## change working directory

- [python - How to change working directory in Jupyter Notebook? - Stack Overflow](https://stackoverflow.com/questions/35664972/how-to-change-working-directory-in-jupyter-notebook/35665295)

    > Running `os.chdir(NEW_PATH)` will change the working directory.
    > 
    > ```py
    > import os
    > os.getcwd()
    > Out[2]:
    > '/tmp'
    > In [3]:
    > 
    > os.chdir('/')
    > In [4]:
    > 
    > os.getcwd()
    > Out[4]:
    > '/'
    > In [ ]:
    > ```
    > 
    > ---
    > 
    > You may use jupyter magic command as below
    > ```
    > %cd "C:\abc\xyz\"
    > ```

## get dicectory path

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



## list directory(glob, os.walk)

- [filesystems - Directory listing in Python - Stack Overflow](https://stackoverflow.com/questions/120656/directory-listing-in-python)

    > This is a way to traverse every file and directory in a directory tree:
    > 
    > ```py
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
    > ```py
    > import glob
    > print(glob.glob("/home/adam/*.txt"))
    > ```
    > 
    > Will return a list with the queried files:
    > 
    > ```py
    > ['/home/adam/file1.txt', '/home/adam/file2.txt', .... ]
    > ```
    > 


    > [`os.listdir()`](https://docs.python.org/2/library/os.html#os.listdir "os.listdir") will get you everything that's in a directory - files and directories.
    > 
    > If you want _just_ files, you could either filter this down using [`os.path`](https://docs.python.org/2/library/os.path.html#module-os.path):
    > 
    > ```py
    > from os import listdir
    > from os.path import isfile, join
    > onlyfiles = [f for f in listdir(mypath) if isfile(join(mypath, f))]
    > ```
    > 
    > or you could use [`os.walk()`](https://docs.python.org/2/library/os.html#os.walk "os.walk") which will yield two lists for each directory it visits - splitting into files and dirs for you. If you only want the top directory you can just break the first time it yields
    > 
    > ```py
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
    > ```py
    > >>> q = [1, 2, 3]
    > >>> w = [4, 5, 6]
    > >>> q = q + w
    > >>> q
    > [1, 2, 3, 4, 5, 6]
    > ```
    > 
    > Personally, I prefer `.extend()`
    > 

### using windows path in glob

- [windows - Getting Every File in a Directory, Python - Stack Overflow](https://stackoverflow.com/questions/5629242/getting-every-file-in-a-directory-python)

    > All of the answers here don't address the fact that if you pass `glob.glob()` a Windows path (for example, `C:\what\okay\i_guess\`), it does not run as expected. Instead, you need to use `pathlib`:
    > 
    > ```python
    > from pathlib import Path
    > 
    > glob_path = Path(r"C:\what\okay\i_guess")
    > file_list = [str(pp) for pp in glob_path.glob("**/*.txt")]
    > ```

### "u" and "r" string flags

- [python - What exactly do "u" and "r" string flags do, and what are raw string literals? - Stack Overflow](https://stackoverflow.com/questions/2081640/what-exactly-do-u-and-r-string-flags-do-and-what-are-raw-string-literals)

    > A "u" prefix denotes the value has type `unicode` rather than `str`.
    > 
    > Raw string literals, with an "r" prefix, escape any escape sequences within them, so `len(r"\n")` is 2. Because they escape escape sequences, you cannot end a string literal with a single backslash: that's not a valid escape sequence (e.g. `r"\"`).
    > 
    > "Raw" is not part of the type, it's merely one way to represent the value. For example, `"\\n"` and `r"\n"` are identical values, just like `32`, `0x20`, and `0b100000` are identical.
    > 


### using pathlib, getting error: TypeError: invalid file: PosixPath('example.txt')

- [python - When using pathlib, getting error: TypeError: invalid file: PosixPath('example.txt') - Stack Overflow](https://stackoverflow.com/questions/42694112/when-using-pathlib-getting-error-typeerror-invalid-file-posixpathexample-t)

    > [`pathlib`](https://docs.python.org/3/library/pathlib.html) integrates seemlessly with `open` only in Python 3.6 and later. From [Python 3.6's release notes](https://docs.python.org/3/whatsnew/3.6.html):
    > 
    > > The built-in `open()` function has been updated to accept `os.PathLike` objects, as have all relevant functions in the `os` and `os.path` modules, and most other functions and classes in the standard library.
    > 
    > To get it to work in Python 3.5 and Python 3.6, just convert the object to a string:
    > 
    > ```python
    > contents = open(str(filename), "r").read()
    > ```

## path tilde expansion

- [Python's os.makedirs doesn't understand "~" in my path - Stack Overflow](https://stackoverflow.com/questions/2057045/pythons-os-makedirs-doesnt-understand-in-my-path)

    > You need to expand the tilde manually:
    > 
    > ```py
    > my_dir = os.path.expanduser('~/some_dir')
    > ```

## md5/checksum

- [How do I calculate the md5 checksum of a file in Python? - Stack Overflow](https://stackoverflow.com/questions/16874598/how-do-i-calculate-the-md5-checksum-of-a-file-in-python)


    > In regards to your error and what's missing in your code. m is name which was not defined for getmd5() function. No offence, I know you are a beginner, but your code is all over the place. Let's look at your issues one by one :) First off, you are not using hashlib.md5.hexdigest() method correctly. Please find explanation on haslib functions [Python Doc Library](http://docs.python.org/3.3/library/hashlib.html). The correct way to return md5 for provided **string** is to do something like this:
    > 
    > ```py
    > >>> import hashlib
    > >>> hashlib.md5("filename.exe").hexdigest()
    > '2a53375ff139d9837e93a38a279d63e5'
    > ```
    > 
    > However, you have bigger problem here. You are calculating MD5 on a **file name string**, where in reality MD5 is calculated based on file **contents**. You will need to basically read file contents and pipe it though md5. My next example is not very efficient, but something like that:
    > 
    > ```py
    > >>> import hashlib
    > >>> hashlib.md5(open('filename.exe','rb').read()).hexdigest()
    > 'd41d8cd98f00b204e9800998ecf8427e'
    > ```
    > 
    > As you can clearly see second MD5 hash is totally different from the first one. The reason for that is that we are pushing contents of the file through, not just file name. A simple solution could be something like that:
    > 
    > ```py
    > # Import hashlib library (md5 method is part of it)
    > import hashlib
    > 
    > # File to check
    > file_name = 'filename.exe'
    > 
    > # Correct original md5 goes here
    > original_md5 = '5d41402abc4b2a76b9719d911017c592'
    > 
    > # Open,close, read file and calculate MD5 on its contents
    > with open(file_name) as file_to_check:
    >     # read contents of the file
    >     data = file_to_check.read()
    >     # pipe contents of the file through
    >     md5_returned = hashlib.md5(data).hexdigest()
    > 
    > # Finally compare original MD5 with freshly calculated
    > if orginal_md5 == md5_returned:
    >     print "MD5 verified."
    > else:
    >     print "MD5 verification failed!."
    > ```
    > 
    > Please look at the post **[Python: Generating a MD5 checksum of a file](https://stackoverflow.com/questions/3431825/python-generating-a-md5-checksum-of-a-file)** it explains in detail couple of ways how it can be achieved efficiently.


- [python - Generating an MD5 checksum of a file - Stack Overflow](https://stackoverflow.com/questions/3431825/generating-an-md5-checksum-of-a-file)

    > You can use [hashlib.md5()](http://docs.python.org/library/hashlib.html)
    > 
    > Note that sometimes you won't be able to fit the whole file in memory. In that case, you'll have to read chunks of 4096 bytes sequentially and feed them to the Md5 function:
    > 
    > ```py
    > def md5(fname):
    >     hash_md5 = hashlib.md5()
    >     with open(fname, "rb") as f:
    >         for chunk in iter(lambda: f.read(4096), b""):
    >             hash_md5.update(chunk)
    >     return hash_md5.hexdigest()
    > ```

## Search for a file using a wildcard(glob)

- [python - Search for a file using a wildcard - Stack Overflow](https://stackoverflow.com/questions/3348753/search-for-a-file-using-a-wildcard)

    > Like this:
    > 
    > ```python
    > >>> import glob
    > >>> glob.glob('./[0-9].*')
    > ['./1.gif', './2.txt']
    > >>> glob.glob('*.gif')
    > ['1.gif', 'card.gif']
    > >>> glob.glob('?.gif')
    > ['1.gif']
    > ```
    > 
    > This comes straight from here: <http://docs.python.org/library/glob.html>

## exclude pattern in glob

- [python - glob exclude pattern - Stack Overflow](https://stackoverflow.com/questions/20638040/glob-exclude-pattern)

    > The pattern rules for glob are not regular expressions. Instead, they follow standard Unix path expansion rules. There are only a few special characters: two different wild-cards, and character ranges are supported [from [glob](https://pymotw.com/2/glob/)].
    > 
    > So you can exclude some files with patterns.\
    > For example to exclude manifests files (files starting with `_`) with glob, you can use:
    > 
    > ```python
    > files = glob.glob('files_path/[!_]*')
    > ```
    > 
    > ---
    > 
    > You can deduct sets:
    > 
    > ```python
    > set(glob("*")) - set(glob("eph"))
    > ```
    > 
    > ---
    > Just as a side note, glob returns lists and not sets, but this kind of operation only works on sets, hence why [neutrinus](https://stackoverflow.com/users/1216074/neutrinus) cast it. If you need it to remain a list, simply wrap the entire operation in a cast: `list(set(glob("*")) - set(glob("eph")))` -- [Nathan Smith](https://stackoverflow.com/users/6332918/nathan-smith "533 reputation") [Aug 10 '17 at 21:48](https://stackoverflow.com/questions/20638040/glob-exclude-pattern#comment78207512_21502564)
    > 
    > ---
    > 
    > Late to the game but you could alternatively just apply a python `filter` to the result of a `glob`:
    > 
    > ```python
    > files = glob.iglob('your_path_here')
    > files_i_care_about = filter(lambda x: not x.startswith("eph"), files)
    > ```
    > 
    > or replacing the lambda with an appropriate regex search, etc...
    > 
    > EDIT: I just realized that if you're using full paths the `startswith` won't work, so you'd need a regex
    > 
    > ```python
    > In [10]: a
    > Out[10]: ['/some/path/foo', 'some/path/bar', 'some/path/eph_thing']
    > 
    > In [11]: filter(lambda x: not re.search('/eph', x), a)
    > Out[11]: ['/some/path/foo', 'some/path/bar']
    > ```
    > 




## Find files with content matching regex

- [python - Find files with content matching regex - Code Review Stack Exchange](https://codereview.stackexchange.com/questions/139423/find-files-with-content-matching-regex)

    > ```python
    > def get_files(path, regex):
    >     search = regex.search
    >     for root, dirs, files in walk(path):
    >         for name in files:
    >             with codecs.open(join(root, name), 'r', 'utf-8') as f:
    >                 try:
    >                     data = f.read()
    >                 except (UnicodeError, ValueError):
    >                     continue
    >             match = search(data)
    >             if match is not None:
    >                 yield join(root, name), match
    > ```
    > 

## find files whose whole name (path + name) matches a regular expression

- ["find . -regex ..." in Python or How to find files whose whole name (path + name) matches a regular expression? - Stack Overflow](https://stackoverflow.com/questions/6798097/find-regex-in-python-or-how-to-find-files-whose-whole-name-path-name)

    > From `help(os.walk)`:
    > 
    > > When topdown is true, the caller can modify the dirnames list in-place (e.g., via del or slice assignment), and walk will only recurse into the subdirectories whose names remain in dirnames; this can be used to prune the search...
    > 
    > So once a subdirectory (listed in `dirnames`) is determined to be inadmissable, it should be deleted from `dirnames`. This will produce the subtree-pruning you are looking for. (Just be sure to `del` items from `dirnames` from the tail-end first, so you don't change the index of remaining items to be deleted.)
    > 
    > ```python
    > import os
    > import re
    > 
    > def prune(regex,top='.'):
    >     sep=os.path.sep
    >     matcher = re.compile(regex)
    >     pieces=regex.split(sep)
    >     partial_matchers = map(
    >         re.compile,
    >         (sep.join(pieces[:i+1]) for i in range(len(pieces))))
    >     for root, dirs, files in os.walk(top,topdown=True):
    >         for i in reversed(range(len(dirs))):
    >             dirname=os.path.relpath(os.path.join(root,dirs[i]), top)
    >             dirlevel=dirname.count(sep)
    >             # print(dirname,dirlevel,sep.join(pieces[:dirlevel+1]))
    >             if not partial_matchers[dirlevel].match(dirname):
    >                 print('pruning {0}'.format(
    >                     os.path.relpath(os.path.join(root,dirs[i]), top)))
    >                 del dirs[i]
    > 
    >         for filename in files:
    >             filename=os.path.relpath(os.path.join(root,filename))
    >             # print('checking {0}'.format(filename))
    >             if matcher.match(filename):
    >                 print(filename)
    > 
    > if __name__=='__main__':
    >     prune(r'foo/\w+/bar/\d+-\w+.dat')
    > ```
    > 
    > Running the script with a directory structure like this:
    > 
    > ```
    > ~/test% tree .
    > .
    > |-- foo
    > |   `-- baz
    > |       |-- bad
    > |       |   |-- bad1.txt
    > |       |   `-- badbad
    > |       |       `-- bad2.txt
    > |       `-- bar
    > |           |-- 1-good.dat
    > |           `-- 2-good.dat
    > `-- tmp
    >     |-- 000.png
    >     |-- 001.png
    >     `-- output.gif
    > ```
    > 
    > yields
    > 
    > ```
    > pruning tmp
    > pruning foo/baz/bad
    > foo/baz/bar/2-good.dat
    > foo/baz/bar/1-good.dat
    > ```
    > 
    > If you uncomment the "checking" print statement, it is clear the pruned directories are not walked.
    > 


## grep to display folders which contain files which contain a string

- [grep to display folders which contain files which contain a string - Server Fault](https://serverfault.com/questions/290915/grep-to-display-folders-which-contain-files-which-contain-a-string)

    > You might be able to do this with `grep`, but I think the required logic justifies using a script... This is a quick python script that will search based on the parameters you provided above...
    > 
    > First it recursively searches from `ROOT_DIRECTORY` for any files matching `FILE_FILTER`... then it searches each of those files for a string matching `SEARCH_STRING`. If it finds *any* file matching the `SEARCH_STRING` it will log the match, and immediately skip remaining files in that directory, moving on to the next file in `all_files` that hasn't already had a match (saving you some CPU and disk wear).
    > 
    > If I have made incorrect assumptions, you can edit the variables named `FILE_FILTER`, `SEARCH_STRING`, and `ROOT_PATH`.
    > 
    > Save the script below as `searchme.py` and execute it with `python searchme.py`
    > 
    > ===
    > 
    > ```python
    > import os
    > import re
    > import sys
    > 
    > def get_directory(path):
    >     return '/'.join(path.split('/')[0:-1])
    > 
    > FILE_FILTER = '(\.htm|\.php)'
    > SEARCH_STRING = 'MY_Output'
    > ROOT_PATH = '~/'
    > 
    > all_files = []
    > retval = {}
    > rootdir = os.path.expanduser(ROOT_PATH)
    > 
    > ## Find all files matching FILE_FILTER
    > for root, subFolders, files in os.walk(rootdir):
    >     for file in files:
    >         pname = os.path.join(root,file)
    >         if re.search(FILE_FILTER, pname) is not None: all_files.append(pname)
    >         retval[get_directory(pname)] = False
    > 
    > ## Search files for SEARCH_STRING; take shortcut if string is found
    > for pname in all_files:
    >     path = get_directory(pname)
    >     if not retval[path]:
    >         try:
    >             for line in open(pname):
    >                 if SEARCH_STRING in line:
    >                     retval[path] = True; break
    >         except IOError:
    >             ## Occasionally firefox makes lock files that can't be opened...
    >             ##     Ignore any permission errors...
    >             pass
    > 
    > ## Print resultant directories...
    > for path in sorted(retval.keys()):
    >     if retval[path]: print path
    > 
    > ```







