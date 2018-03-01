# Python__快速上手

<!-- toc --> 
[toc]

## Basic Tutorial
* [Python Tutorial](https://www.tutorialspoint.com/python/index.htm)


## API reference

- [API Reference — pandas 0.22.0 documentation](https://pandas.pydata.org/pandas-docs/stable/api.html?highlight=dataframe#dataframe)
- [API Reference — scikit-learn 0.19.1 documentation](http://scikit-learn.org/stable/modules/classes.html#module-sklearn.datasets)
    - [Choosing the right estimator — scikit-learn 0.19.1 documentation](http://scikit-learn.org/stable/tutorial/machine_learning_map/index.html)
    - [Classifier comparison — scikit-learn 0.19.1 documentation](http://scikit-learn.org/stable/auto_examples/classification/plot_classifier_comparison.html)
    - [Comparing Python Clustering Algorithms — hdbscan 0.8.1 documentation](https://hdbscan.readthedocs.io/en/latest/comparing_clustering_algorithms.html)

- [The Matplotlib API — Matplotlib 2.1.1 documentation](https://matplotlib.org/api/index.html)
    - [The Pyplot API — Matplotlib 2.1.1 documentation](https://matplotlib.org/api/pyplot_summary.html)
        - [Pyplot tutorial — Matplotlib 2.0.2 documentation](https://matplotlib.org/users/pyplot_tutorial.html)
        - [Tight Layout guide — Matplotlib 2.0.2 documentation](https://matplotlib.org/users/tight_layout_guide.html)
        - [A simple plot with a custom dashed line — Matplotlib 2.1.0 documentation](https://matplotlib.org/2.1.0/gallery/lines_bars_and_markers/line_demo_dash_control.html)
        - [Line-style reference — Matplotlib 2.1.2 documentation](https://matplotlib.org/gallery/lines_bars_and_markers/line_styles_reference.html?highlight=line%20style%20reference)
- [Routines — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/routines.html)
    - [Index — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/genindex.html)

- [SciPy — SciPy v1.0.0 Reference Guide](https://docs.scipy.org/doc/scipy-1.0.0/reference/)
    - [Index — SciPy v1.0.0 Reference Guide](https://docs.scipy.org/doc/scipy-1.0.0/reference/genindex.html)
- [The Python Standard Library — Python 3.3.7 documentation](https://docs.python.org/3.3/library/index.html)
    - [Python Tutorial](https://www.tutorialspoint.com/python/index.htm)

- [API Reference — graphviz 0.8.2 documentation](https://graphviz.readthedocs.io/en/stable/api.html)
    - [User Guide — graphviz 0.8.2 documentation](https://graphviz.readthedocs.io/en/stable/manual.html)

## Default Method


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


## Library 

### Python Module

- [8.11. pprint — Data pretty printer — Python 3.3.7 documentation](https://docs.python.org/3.3/library/pprint.html?highlight=pprint#module-pprint)
    
    - __pprint.pprint(_object_, _stream=None_, _indent=1_, _width=80_, _depth=None_)__
        Prints the formatted representation of _object_ on _stream_, followed by a newline.

- [6.2. re — Regular expression operations — Python 3.3.7 documentation](https://docs.python.org/3.3/library/re.html?highlight=re#re.compile)
    - __re.compile(_pattern_, _flags=0_)[](https://docs.python.org/3.3/library/re.html?highlight=re#re.compile "Permalink to this definition")__
        Compile a regular expression pattern into a regular expression object, which can be used for matching using its [match()](https://docs.python.org/3.3/library/re.html?highlight=re#re.match "re.match") and [search()](https://docs.python.org/3.3/library/re.html?highlight=re#re.search "re.search") methods, described below.



### pyplot

- [matplotlib.pyplot.imshow — Matplotlib 2.1.2 documentation](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.imshow.html#matplotlib.pyplot.imshow)

    - 加上 interpolation='bicubic' 可以平滑化

        before:

        ```python=
        plt.imshow(example_grad, cmap = 'rainbow') 
        ```
        ![](https://screenshotscdn.firefoxusercontent.com/images/5c21da21-13d8-4c4e-950e-20372715c4f1.png)

        after:

        ```python=
        plt.imshow(example_grad, cmap = 'rainbow',  interpolation='bicubic') 
        ```
        ![](https://screenshotscdn.firefoxusercontent.com/images/b771dbf5-c3b0-4a37-b142-cd74a145f2c1.png)


### numpy

- [numpy.array — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/generated/numpy.array.html#numpy.array)
    Create an array.

- [numpy.eye — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/generated/numpy.eye.html#numpy.eye)
    Return a 2-D array with ones on the diagonal and zeros elsewhere.

- [numpy.ma.max — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/generated/numpy.ma.max.html#numpy.ma.max)
    Return the maximum along a given axis.

- [numpy.nonzero — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/generated/numpy.nonzero.html#numpy.nonzero)
    Return the indices of the elements that are non-zero.

- [numpy.ma.shape — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/generated/numpy.ma.shape.html#numpy.ma.shape)
    Return the shape of an array.

- [numpy.arange — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/generated/numpy.arange.html#numpy.arange)
    Return evenly spaced values within a given interval.

- [numpy.nditer — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/generated/numpy.nditer.html#numpy.nditer)
    Efficient multi-dimensional iterator object to iterate over arrays. To get started using this object, see the [_introductory guide to array iteration_](https://docs.scipy.org/doc/numpy-1.12.0/reference/arrays.nditer.html#arrays-nditer).
- [numpy.ma.argmax — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/generated/numpy.ma.argmax.html#numpy.ma.argmax)
    Returns array of indices of the maximum values along the given axis. Masked values are treated as if they had the value fill_value.
- [numpy.append — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/generated/numpy.append.html#numpy.append)
    Append values to the end of an array.


### Pandas
- [pandas.DataFrame.from_records — pandas 0.22.0 documentation](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.from_records.html#pandas.DataFrame.from_records)
    Convert structured or record ndarray to DataFrame

- [pandas.DataFrame.apply — pandas 0.22.0 documentation](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.apply.html)
    Applies function along input axis of DataFrame.




## Usage

### Math 

- [math - How do I do exponentiation in python? - Stack Overflow](https://stackoverflow.com/questions/30148740/how-do-i-do-exponentiation-in-python)

    > `^` is the [xor](http://en.wikipedia.org/wiki/Exclusive_or) operator.
    > 
    > `**` is exponentiation.
    > 
    > `2**3 = 8`


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




---
↩️ back to [SUMMARY](SUMMARY.md)