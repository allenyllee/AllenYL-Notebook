# Python__機器學習

[toc]
<!-- toc --> 

# python2 to python 3

- [How to update your scikit-learn code for 2018](https://www.dataschool.io/how-to-update-your-scikit-learn-code-for-2018/)

# scikit learn videos

- [justmarkham/scikit-learn-videos: Jupyter notebooks from the scikit-learn video series](https://github.com/justmarkham/scikit-learn-videos)



# API reference

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




# pyplot

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

- [matplotlib.pyplot.subplot — Matplotlib 2.1.1 documentation](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.subplot.html#matplotlib.pyplot.subplot)

    `plot_dict` 內容結構為 noise:axis 的字典, 其中 noise 為字典的 key 值, 而 axis 值作為 subplot 分割的 row, col, index。

    倘若 row, col 和 index 皆可用單位數字表示，則可以用單個 3 位數字來指定。

    ```python
    # 指定圖表的大小 (寬, 高) 單位為英吋
    rcParams['figure.figsize'] = 8, 4
    # 1 row, 4 cols, 從左到右
    plot_dict = { 1: 141, 9: 142, 18: 143, 1000: 144 }
    linear_prediction(plot_dict)

    # 指定圖表的大小 (寬, 高) 單位為英吋
    rcParams['figure.figsize'] = 8, 10
    # 2 rows, 2 cols, 從左至右，由上到下
    plot_dict = { 1: 221, 9: 222, 18: 223, 1000: 224}
    linear_prediction(plot_dict)
    ```
    
## 在for loop中畫圖

- [python - Display numpy array in a for loop using matplotlib imshow - Stack Overflow](https://stackoverflow.com/questions/25812905/display-numpy-array-in-a-for-loop-using-matplotlib-imshow)

    > `imshow(a)` will plot the values of the array a as pixel values, but it won't display the plot. To view the image after each iteration of the for loop, you need to add `show()`.

    > ```
    > a = np.array([[1,2,3],[4,5,6],[7,8,9]])
    > 
    > for t in range(0,10):
    >     imshow(a)
    >     show()
    > ```



# numpy

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



- [numpy.nditer — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/generated/numpy.nditer.html#numpy.nditer)
    Efficient multi-dimensional iterator object to iterate over arrays. To get started using this object, see the [_introductory guide to array iteration_](https://docs.scipy.org/doc/numpy-1.12.0/reference/arrays.nditer.html#arrays-nditer).

## Check Version

- [python - How do I check which version of NumPy I'm using? - Stack Overflow](https://stackoverflow.com/questions/1520234/how-do-i-check-which-version-of-numpy-im-using)

    > 
    > ```py
    > >> import numpy
    > >> print numpy.__version__
    > ```
    > 
    > This is the API we numpy developers will support. numpy.version.version is an implementation detail that should not be relied upon. – Robert Kern Oct 6 '09 at 0:18
    > 
    > ---
    > 
    > If you're using ***NumPy from the Anaconda distribution***, then you can just do:
    > 
    > ```py
    > $ conda list | grep numpy
    > numpy     1.11.3     py35_0
    > ```
    > 
    > This gives the `Python` version as well.
    > 
    > ---
    > 
    > We can use `pip freeze` to get any Python package version without opening the Python shell.
    > 
    > ```py
    > pip freeze | grep 'numpy'
    > ```
    > 
    > That only works if you installed numpy via pip, not via brew or apt-get, for example.
    > 
    > ---
    > 
    > Run:
    > 
    > ```py
    > pip list
    > ```
    > 
    > Should generate a list of packages.
    > 
    > 


## get indices of max argument

- [numpy.arange — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/generated/numpy.arange.html#numpy.arange)
    Return evenly spaced values within a given interval.

- [numpy.ma.argmax — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/generated/numpy.ma.argmax.html#numpy.ma.argmax)
    Returns array of indices of the maximum values along the given axis. Masked values are treated as if they had the value fill_value.
    
    > Examples
    > ```python
    > >>> a = np.arange(6).reshape(2,3)
    > >>> a
    > array([[0, 1, 2],
    >  [3, 4, 5]])
    > >>> np.argmax(a)
    > 5
    > >>> np.argmax(a, axis=0)
    > array([1, 1, 1])
    > >>> np.argmax(a, axis=1)
    > array([2, 2])
    > ```
    > 
    
    
    
    
    
- [numpy.append — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/generated/numpy.append.html#numpy.append)
    Append values to the end of an array.

- [numpy.reshape — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/generated/numpy.reshape.html#numpy.reshape)
    Gives a new shape to an array without changing its data.

    ```python
    >>> a = np.arange(6).reshape((3, 2))
    >>> a
    array([[0, 1],
           [2, 3],
           [4, 5]]) 
    ```

    ```python
    >>> np.reshape(a, (2, 3)) # C-like index ordering
    array([[0, 1, 2],
           [3, 4, 5]])
    ```

- [numpy.ma.copy — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/generated/numpy.ma.copy.html#numpy.ma.copy)
    Return a copy of the array.

- [numpy.linspace — NumPy v1.14 Manual](https://docs.scipy.org/doc/numpy/reference/generated/numpy.linspace.html)
    Return evenly spaced numbers over a specified interval.


- [Random sampling (numpy.random) — NumPy v1.14 Manual](https://docs.scipy.org/doc/numpy/reference/routines.random.html)

    - [numpy.random.seed — NumPy v1.14 Manual](https://docs.scipy.org/doc/numpy/reference/generated/numpy.random.seed.html#numpy.random.seed)
    Seed the generator.


    - [numpy.matlib.rand — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/generated/numpy.matlib.rand.html#numpy.matlib.rand)
    Return a matrix of random values with given shape.

    - [numpy.matlib.randn — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/generated/numpy.matlib.randn.html#numpy.matlib.randn)
    Return a random matrix with data from the “standard normal” distribution.

- [numpy.clip — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/generated/numpy.clip.html#numpy.clip)
    Clip (limit) the values in an array.
    
    Given an interval, values outside the interval are clipped to the interval edges. For example, if an interval of \[0, 1\] is specified, values smaller than 0 become 0, and values larger than 1 become 1.

- [numpy.argsort — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/generated/numpy.argsort.html#numpy.argsort)
    Returns the indices that would sort an array.

- [numpy.ravel — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/generated/numpy.ravel.html#numpy.ravel)
    Return a contiguous flattened array.

- [numpy.vstack — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/generated/numpy.vstack.html#numpy.vstack)
    Stack arrays in sequence vertically (row wise).

    ```python
    >>> a = np.array([1, 2, 3])
    >>> b = np.array([2, 3, 4])
    >>> np.vstack((a,b))
    array([[1, 2, 3],
           [2, 3, 4]])
    ```

- [numpy.zeros_like — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/generated/numpy.zeros_like.html#numpy.zeros_like)
    Return an array of zeros with the same shape and type as a given array.

```python
>>> x = np.arange(6)
>>> x = x.reshape((2, 3))
>>> x
array([[0, 1, 2],
       [3, 4, 5]])
>>> np.zeros_like(x)
array([[0, 0, 0],
       [0, 0, 0]])
```

- [Indexing — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/arrays.indexing.html)
    - __numpy.newaxis__
    The [newaxis](https://docs.scipy.org/doc/numpy-1.12.0/reference/arrays.indexing.html#numpy.newaxis "numpy.newaxis") object can be used in all slicing operations to create an axis of length one. [newaxis](https://docs.scipy.org/doc/numpy-1.12.0/reference/arrays.indexing.html#numpy.newaxis "numpy.newaxis") is an alias for ‘None’, and ‘None’ can be used in place of this with the same result.
       - [python - How does numpy.newaxis work and when to use it? - Stack Overflow](https://stackoverflow.com/questions/29241056/how-does-numpy-newaxis-work-and-when-to-use-it)
            > Simply put, the [`newaxis`](https://docs.scipy.org/doc/numpy/reference/arrays.indexing.html#numpy.newaxis) is used to **_increase the dimension_** of the existing array by _one more dimension_, when used _once_. Thus,
            > 
            > -   **1D** array will become **2D** array
            >     
            > -   **2D** array will become **3D** array
            >     
            > -   **3D** array will become **4D** array
            >     
            > 
            > and so on.. Here is an illustration.
            > 
            > [![newaxis canva visualization](https://i.stack.imgur.com/zkMBy.png)](https://i.stack.imgur.com/zkMBy.png)
            > 
            > ---
            > 
            > **Scenario-1**: [`np.newaxis`](https://docs.scipy.org/doc/numpy/reference/arrays.indexing.html#numpy.newaxis) might come in handy when you want to _explicitly_ convert an 1D array to either a _row vector_ or a _column vector_, as depicted in the above picture.
            > 
            > **Example:**
            > 
            > ```
            > # 1D array
            > In [7]: arr = np.arange(4)
            > In [8]: arr.shape
            > Out[8]: (4,)
            > 
            > # make it as row vector by inserting an axis along first dimension
            > In [9]: row_vec = arr[np.newaxis, :]
            > In [10]: row_vec.shape
            > Out[10]: (1, 4)
            > 
            > # make it as column vector by inserting an axis along second dimension
            > In [11]: col_vec = arr[:, np.newaxis]
            > In [12]: col_vec.shape
            > Out[12]: (4, 1)
            > ```
            > 
            > ---
            > 
            > **Scenario-2**: When we want to make use of [numpy broadcasting](https://docs.scipy.org/doc/numpy-1.13.0/user/basics.broadcasting.html) as part of some operation, for instance while doing _addition_ of some arrays.
            > 
            > **Example:**
            > 
            > Let's say you want to add the following two arrays:
            > 
            > ```
            >  x1 = np.array([1, 2, 3, 4, 5])
            >  x2 = np.array([5, 4, 3])
            > ```
            > 
            > If you try to add these just like that, NumPy will raise the following `ValueError` :
            > 
            > ```
            > ValueError: operands could not be broadcast together with shapes (5,) (3,)
            > ```
            > 
            > In this situation, you can use [`np.newaxis`](https://docs.scipy.org/doc/numpy/reference/arrays.indexing.html#numpy.newaxis) to increase the dimension of one of the arrays so that NumPy can [broadcast](https://docs.scipy.org/doc/numpy-1.13.0/user/basics.broadcasting.html).
            > 
            > ```
            > In [2]: x1_new = x1[:, np.newaxis]
            > # now, the shape of x1_new is (5, 1)
            > # array([[1],
            > #        [2],
            > #        [3],
            > #        [4],
            > #        [5]])
            > ```
            > 
            > Now, add:
            > 
            > ```
            > In [3]: x1_new + x2
            > Out[3]:
            > array([[ 6,  5,  4],
            >        [ 7,  6,  5],
            >        [ 8,  7,  6],
            >        [ 9,  8,  7],
            >        [10,  9,  8]])
            > ```
            > 
            > ---
            > 
            > Alternatively, you can also add new axis to the array `x2`:
            > 
            > ```
            > In [6]: x2_new = x2[:, np.newaxis]
            > In [7]: x2_new     # shape is (3, 1)
            > Out[7]: 
            > array([[5],
            >        [4],
            >        [3]])
            > ```
            > 
            > Now, add:
            > 
            > ```
            > In [8]: x1 + x2_new
            > Out[8]: 
            > array([[ 6,  7,  8,  9, 10],
            >        [ 5,  6,  7,  8,  9],
            >        [ 4,  5,  6,  7,  8]])
            > ```
            > 
            > **Note**: Observe that we get the same result in both cases (but one being the transpose of the other).
            > 
            > ---
            > 
            > **Scenario-3**: This is similar to scenario-1. But, you can use [`np.newaxis`](https://docs.scipy.org/doc/numpy-1.13.0/reference/arrays.indexing.html#numpy.newaxis) more than once to _promote_ the array to higher dimensions.
            > 
            > **Example:**
            > 
            > ```
            > In [124]: arr = np.arange(5*5).reshape(5,5)
            > 
            > In [125]: arr.shape
            > Out[125]: (5, 5)
            > 
            > # promoting 2D array to a 5D array
            > In [126]: arr_5D = arr[np.newaxis, ..., np.newaxis, np.newaxis]
            > 
            > In [127]: arr_5D.shape
            > Out[127]: (1, 5, 5, 1, 1)
            > ```
            >
            > **More background on [np.newaxis](https://docs.scipy.org/doc/numpy-1.13.0/reference/arrays.indexing.html#numpy.newaxis) vs [np.reshape](https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.reshape.html)**
            > 
            > [`newaxis`](https://docs.scipy.org/doc/numpy-1.13.0/reference/arrays.indexing.html#numpy.newaxis) is also called as a pseudo-index that allows the temporary addition of an axis into a multiarray.
            > 
            > [`np.newaxis`](https://docs.scipy.org/doc/numpy-1.13.0/reference/arrays.indexing.html#numpy.newaxis) uses the slicing operator to recreate the array while [`np.reshape`](https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.reshape.html) reshapes the array to the desired layout (assuming that the dimensions match; And this is **_must_** for a [`reshape`](https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.reshape.html) to happen).
            > 
            > **Example**
            > 
            > ```
            > In [13]: A = np.ones((3,4,5,6))
            > In [14]: B = np.ones((4,6))
            > In [15]: (A + B[:, np.newaxis, :]).shape
            > Out[15]: (3, 4, 5, 6)
            > ```
            > 
            > In the above example, we inserted a temporary axis between the first and second axes of `B` (to use broadcasting). A missing axis is filled-in here using [`np.newaxis`](https://docs.scipy.org/doc/numpy-1.13.0/reference/arrays.indexing.html#numpy.newaxis) to make the [broadcasting](https://docs.scipy.org/doc/numpy-1.13.0/user/basics.broadcasting.html) operation work.
            > 
            > ---
            > 
            > **_General Tip_**: You can also use `None` in place of [`np.newaxis`](https://docs.scipy.org/doc/numpy/reference/arrays.indexing.html#numpy.newaxis); These are in fact the [same objects](https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.expand_dims.html).
            > 
            > ```
            > In [13]: np.newaxis is None
            > Out[13]: True
            > ```
            > 
            > P.S. Also see this great answer: [newaxis vs reshape to add dimensions](https://stackoverflow.com/a/28385957)
            > 

## Sorting

- [python - Efficiently sorting a numpy array in descending order? - Stack Overflow](https://stackoverflow.com/questions/26984414/efficiently-sorting-a-numpy-array-in-descending-order)
    
    > `temp[::-1].sort()` sorts the array in place, `np.sort(temp)[::-1]` create a new array.
    > 
    > ```
    > In [25]: temp = np.random.randint(1,10, 10)
    > 
    > In [26]: temp
    > Out[26]: array([5, 2, 7, 4, 4, 2, 8, 6, 4, 4])
    > 
    > In [27]: id(temp)
    > Out[27]: 139962713524944
    > 
    > In [28]: temp[::-1].sort()
    > 
    > In [29]: temp
    > Out[29]: array([8, 7, 6, 5, 4, 4, 4, 4, 2, 2])
    > 
    > In [30]: id(temp)
    > Out[30]: 139962713524944
    > ```

    > For short arrays I suggest using `np.argsort()` by finding the indices of the sorted negatived array, which is slightly faster than reversing the sorted array:
    > 
    > ```
    > In [37]: temp = np.random.randint(1,10, 10)
    > 
    > In [38]: %timeit np.sort(temp)[::-1]
    > 100000 loops, best of 3: 4.65 µs per loop
    > 
    > In [39]: %timeit temp[np.argsort(-temp)]
    > 100000 loops, best of 3: 3.91 µs per loop
    > ```

## get index of element

- [python - Index of element in NumPy array - Stack Overflow](https://stackoverflow.com/questions/18079029/index-of-element-in-numpy-array)

    > Use `np.where` to get the indices where a given condition is `True`.
    > 
    > Examples:
    > 
    > For a 2D `np.ndarray`:
    > 
    > ```python
    > i,j = np.where( a==value )
    > ```
    > 
    > For a 1D array:
    > 
    > ```python
    > i, = np.where( a==value )
    > ```
    > 
    > If also works for conditions like `>=`, `<=`, `!=` and so forth...
    > 
    > You can also create a subclass of `np.ndarray` with a `index()` method:
    > 
    > ```python
    > class myarray(np.ndarray):
    >     def __new__(cls, *args, **kwargs):
    >         return np.array(*args, **kwargs).view(myarray)
    >     def index(self, value):
    >         return np.where(self==value)
    > ```
    > 
    > Testing:
    > 
    > ```python
    > a = myarray([1,2,3,4,4,4,5,6,4,4,4])
    > a.index(4)
    > #(array([ 3,  4,  5,  8,  9, 10]),)
    > ```

## indexing & slicing

- [Numpy 笔记(二): 多维数组的切片(slicing)和索引(indexing) · ZMonster's Blog](http://www.zmonster.me/2016/03/09/numpy-slicing-and-indexing.html)

    > 切片和索引的同异
    > 
    > 切片和索引都是访问多维数组中元素的方法，这是两者的共同点，不同之处有:
    > 
    >     切片得到的是原多维数组的一个 视图(view) ，修改切片中的内容会导致原多维数组的内容也发生变化
    >     切片得到在多维数组中连续(或按特定步长连续)排列的值，而索引可以得到任意位置的值，自由度更大一些
    > 
    > 不考虑第一点的话，切片的操作是可以用索引操作来实现的，不过这没有必要就是了。
    > 
    > 对于第一点，见下面的实验:
    > 
    > ```python
    > import numpy as np
    > 
    > arr = np.arange(12).reshape(2, 6)
    > print 'array is:'
    > print arr
    > 
    > slc = arr[:, 2:5]
    > print 'slice is:'
    > print slc
    > 
    > slc[1, 2] = 10000
    > print 'modified slice is:'
    > print slc
    > print 'array is now:'
    > print arr
    > ```
    > 
    > ```python
    > array is:
    > [[ 0  1  2  3  4  5]
    >  [ 6  7  8  9 10 11]]
    > slice is:
    > [[ 2  3  4]
    >  [ 8  9 10]]
    > modified slice is:
    > [[    2     3     4]
    >  [    8     9 10000]]
    > array is now:
    > [[    0     1     2     3     4     5]
    >  [    6     7     8     9 10000    11]]
    > ```
    > 


## one-hot

- [python - How to convert 2d numpy array into binary indicator matrix for max value - Stack Overflow](https://stackoverflow.com/questions/36153638/how-to-convert-2d-numpy-array-into-binary-indicator-matrix-for-max-value)

    > Here's one way:
    > 
    > ```
    > In [112]: a
    > Out[112]: 
    > array([[ 0.2,  0.3,  0.5],
    >        [ 0.7,  0.1,  0.1]])
    > 
    > In [113]: a == a.max(axis=1, keepdims=True)
    > Out[113]: 
    > array([[False, False,  True],
    >        [ True, False, False]], dtype=bool)
    > 
    > In [114]: (a == a.max(axis=1, keepdims=True)).astype(int)
    > Out[114]: 
    > array([[0, 0, 1],
    >        [1, 0, 0]])
    > ```
    > 
    > (But this will give a True value for _each_ occurrence of the maximum in a row. See Divakar's answer for a nice way to select just the first occurrence of the maximum.)

    > In case of ties (two or more elements being the highest one in a row), where you want to select only one, here's one approach to do so with [`np.argmax`](http://docs.scipy.org/doc/numpy-1.10.1/reference/generated/numpy.argmax.html) and [`broadcasting`](http://docs.scipy.org/doc/numpy-1.10.1/user/basics.broadcasting.html) -
    > 
    > ```
    > (A.argmax(1)[:,None] == np.arange(A.shape[1])).astype(int)
    > ```
    > 
    > Sample run -
    > 
    > ```
    > In [296]: A
    > Out[296]: 
    > array([[ 0.2,  0.3,  0.5],
    >        [ 0.5,  0.5,  0. ]])
    > 
    > In [297]: (A.argmax(1)[:,None] == np.arange(A.shape[1])).astype(int)
    > Out[297]: 
    > array([[0, 0, 1],
    >        [1, 0, 0]])
    > ```
    > [name=Divakar]

## Einstein Summation

- [爱因斯坦求和约定 - Wikiwand](https://www.wikiwand.com/zh/%E7%88%B1%E5%9B%A0%E6%96%AF%E5%9D%A6%E6%B1%82%E5%92%8C%E7%BA%A6%E5%AE%9A)

    > 愛因斯坦標記法的基本點子是餘向量與向量可以形成純量：
    > 
    > $$     y=c_{1}x^{1}+c_{2}x^{2}+c_{3}x^{3}+\cdots +c_{n}x^{n}
    > $$
    > 
    > 通常會將這寫為求和公式形式：
    > 
    > $$
    >     y=\sum _{i=1}^{n}c_{i}x^{i}
    > $$
    > 
    > 在基底變換之下，純量保持不變。當基底改變時，一個向量的線性變換可以用矩陣來描述，而餘向量的線性變換則需用其逆矩陣來描述。這樣的設計為的是要保證，不論基底為何，伴隨餘向量的線性函數（即上述總和）保持不變。由於只有總和不變，而總和所涉及的每一個項目都有可能會改變，所以，愛因斯坦提出了這標記法，重複標號表示總和，不需要用到求和符號：
    > 
    > $$
    >     y=c_{i}x^{i}
    > $$
    > 
    > 採用愛因斯坦標記法，餘向量都是以下標來標記，而向量都是以上標來標記。標號的位置具有特別意義。請不要將上標與指數混淆在一起，大多數涉及的方程式都是線性，不超過變數的一次方。在方程式裏，單獨項目內的標號變數最多只會出現兩次，假若多於兩次，或出現任何其它例外，則都必須特別加以說明，才不會造成含意混淆不清。

    > __一般運算__
    > 
    > 矩陣$A$的第$m$橫排，第$n$豎排的元素，以前標記為$A_{mn}$；現在改標記為$A_{n}^{m}$各種一般運算都可以用愛因斯坦標記法來表示如下：
    > 
    > __內積__
    > 
    > 給予向量$\mathbf {a}$和餘向量$\boldsymbol {\alpha }$，其向量和餘向量的內積為純量：
    > 
    > $$
    >     \mathbf {a}\cdot \boldsymbol \alpha =a^{i}\alpha _{i}
    > $$
    > 
    > __向量乘以矩陣__
    > 
    > 給予矩陣$A$和向量$\mathbf {a}$，它們的乘積是向量$\mathbf {b}$：
    > 
    > $$
    >     b^{i}=A_{j}^{i}a^{j}
    > $$
    > 
    > 類似地，矩陣$A$的轉置矩陣$B=A^\mathrm {T}$，其與餘向量$\boldsymbol {\alpha }$的乘積是餘向量$\boldsymbol {\beta }$：
    > 
    > $$
    >     \beta _{j}=B_{j}^{i}\alpha _{i}=\alpha _{i}B_{j}^{i}
    > $$
    > 
    > __矩陣乘法__
    > 
    > 矩陣乘法表示為
    > 
    > $$
    >     C_{k}^{i}=A_{j}^{i}\,B_{k}^{j}\,\!。
    > $$
    > 
    > 這公式等價於較冗長的普通標記法：
    > 
    > $$
    >     C_{ik}={(AB)}_{ik}=\sum _{j=1}^{N}A_{ij}B_{jk}
    > $$
    > 
    > __跡__
    > 
    > 給予一個方塊矩陣$A_{j}^{i}$，總和所有上標與下標相同的元素$A_{i}^{i}$，可以得到這矩陣的跡$t$：
    > 
    > $$
    >     t=A_{i}^{i}\,\!。
    > $$
    > 
    > __外積__
    > 
    > $M$維向量$\mathbf {a}$和$N$維餘向量$\boldsymbol {\alpha }$的外積是一個$M×N$矩陣$A$：
    > 
    > $$
    >     A=\mathbf {a}\boldsymbol {\alpha }
    > $$
    > 
    > 採用愛因斯坦標記式，上述方程式可以表示為
    > 
    > $$
    >     A_{j}^{i}=a^{i}\alpha _{j}
    > $$
    > 
    > 由於$i$和$j$代表兩個不同的標號，在這案例，值域分別為$M$和$N$，外積不會除去這兩個標號，而使這兩個標號變成了新矩陣$A$的標號。
    > 


- [Einstein Summation in Numpy | Olexa Bilaniuk's IFT6266H16 Course Blog](https://obilaniu6266h16.wordpress.com/2016/02/04/einstein-summation-in-numpy/)

    >In Python’s Numpy library lives an extremely general, but little-known and used, function called einsum() that performs summation according to Einstein’s summation convention. In this tutorial article, we demystify einsum().

    > Its advantages over such things as matrix multiplication are that it liberates its user from having to think about:
    > 
    > * The correct order in which to supply the argument tensors
    > * The correct transpositions to apply to the argument tensors
    > * Ensuring that the correct tensor dimensions are lined up with one another
    > * The correct transposition to apply to the resulting tensor
    > 
    > The only things it requires are knowledge of:
    > 
    > * Along which dimensions to compute (inner/element-wise/outer) products.
    > * The desired output shape.
    > 

## Troubleshooting

### RuntimeWarning: numpy.dtype size changed, may indicate binary incompatibility

- [python - RuntimeWarning: numpy.dtype size changed, may indicate binary incompatibility - Stack Overflow](https://stackoverflow.com/questions/40845304/runtimewarning-numpy-dtype-size-changed-may-indicate-binary-incompatibility)

    > It's the issue of new numpy version (1.15.0)
    > 
    > You can downgrade numpy and this problem will be fixed:
    > ```
    > sudo pip uninstall numpy
    > sudo pip install numpy==1.14.5
    > ```
    > 
    > > Finally numpy 1.15.1 version is released so the warning issues are fixed.
    > > ```
    > > sudo pip install numpy==1.15.1
    > > ```


# Scipy

## 處理outlier
- [scipy.stats.rankdata — SciPy v0.16.1 Reference Guide](https://docs.scipy.org/doc/scipy-0.16.0/reference/generated/scipy.stats.rankdata.html)

    > Assign ranks to data, dealing with ties appropriately.
    > 
    > Examples
    > 
    > ```python
    > >>> from scipy.stats import rankdata
    > >>> rankdata([0, 2, 3, 2])
    > array([ 1. ,  2.5,  4. ,  2.5])
    > >>> rankdata([0, 2, 3, 2], method='min')
    > array([ 1.,  2.,  4.,  2.])
    > >>> rankdata([0, 2, 3, 2], method='max')
    > array([ 1.,  3.,  4.,  3.])
    > >>> rankdata([0, 2, 3, 2], method='dense')
    > array([ 1.,  2.,  3.,  2.])
    > >>> rankdata([0, 2, 3, 2], method='ordinal')
    > array([ 1.,  2.,  4.,  3.])
    > ```
    > 


- [scipy.stats.boxcox — SciPy v0.19.0 Reference Guide](https://docs.scipy.org/doc/scipy-0.19.0/reference/generated/scipy.stats.boxcox.html)

    > Return a positive dataset transformed by a Box-Cox power transformation.





# Pandas
- [pandas.DataFrame.from_records — pandas 0.22.0 documentation](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.from_records.html#pandas.DataFrame.from_records)
    Convert structured or record ndarray to DataFrame

- [pandas.DataFrame.apply — pandas 0.22.0 documentation](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.apply.html)
    Applies function along input axis of DataFrame.


## indexing

- [pandas.Series.str.contains — pandas 0.22.0 documentation](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.str.contains.html#pandas.Series.str.contains)
    Return boolean Series/`array` whether given pattern/regex is contained in each string in the Series/Index.

    ```python
    index = pd.Series([True,False,True,False]) 
    data = pd.DataFrame(['a','b_simpson','c','d_simpson'], columns=['col1'])

    # 使用 Series 做 index，丟到 dataframe 會回傳 index 為 true 的項目
    print(data[index])
    ```

    ```python
      col1
    0    a
    2    c
    ```

    ```python
    # 使用 str.contains 做 index，丟到 dataframe 會回傳 index 為 true 的項目
    # 就是 col1 中包含 'simpson' 的項目
    print(data[data.col1.str.contains('simpson')]) 
    ```

    ```python
            col1
    1  b_simpson
    3  d_simpson
    ```



- [pandas.DataFrame.iloc — pandas 0.22.0 documentation](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.iloc.html#pandas.DataFrame.iloc)
    Purely integer-location based indexing for selection by position.

    __example__
    ```python
    df.iloc[:5,-4:] # allenyllee: 顯示頭5列(row)，從第-4欄(倒數第四欄)開始列出到最後一欄
    ```
    ![](https://screenshotscdn.firefoxusercontent.com/images/552381c8-fd9c-423b-b11a-198ccd119b6c.png)

- [python - How to select the last column of dataframe - Stack Overflow](https://stackoverflow.com/questions/40144769/how-to-select-the-last-column-of-dataframe)

    > Use iloc and select all rows (`:`) against the last column (`-1`):
    > 
    > ```
    > df.iloc[:,-1]
    > ```

- [iloc, loc, and ix for data selection in Python Pandas | Shane Lynn](https://www.shanelynn.ie/select-pandas-dataframe-rows-and-columns-using-iloc-loc-and-ix/)

    ![](https://shanelynnwebsite-mid9n9g1q9y8tt.netdna-ssl.com/wp-content/uploads/2016/10/Pandas-selections-and-indexing-1024x731.png)


## remove column

- [Delete column from pandas DataFrame using python del - Stack Overflow](https://stackoverflow.com/questions/13411544/delete-column-from-pandas-dataframe-using-python-del)

    > The best way to do this in pandas is to use [`drop`](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.drop.html):
    > 
    > ```
    > df = df.drop('column_name', 1)
    > ```
    > 
    > where `1` is the _axis_ number (`0` for rows and `1` for columns.)
    > 
    > To delete the column without having to reassign `df` you can do:
    > 
    > ```
    > df.drop('column_name', axis=1, inplace=True)
    > ```
    > 
    > Finally, to drop by column _number_ instead of by column _label_, try this to delete, e.g. the 1st, 2nd and 4th columns:
    > 
    > ```
    > df.drop(df.columns[[0, 1, 3]], axis=1)  # df.columns is zero-based pd.Index 
    > ```
    > 


## correlation

- [pandas.DataFrame.corr — pandas 0.22.0 documentation](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.corr.html#pandas.DataFrame.corr)
    Compute pairwise correlation of columns, excluding NA/null values

    __example__
    ```python
    df.iloc[:,-4:].corr() # 算出倒數四欄的 correlation
    ```
    ![](https://screenshotscdn.firefoxusercontent.com/images/542f5956-ea44-4751-a8be-b1a3936c8a14.png)
    
    

## one-hot & reversing one-hot

- [pandas.get_dummies — pandas 0.22.0 documentation](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.get_dummies.html)
    Convert categorical variable into dummy/indicator variables

    ```python
    >>> import pandas as pd
    >>> s = pd.Series(list('abca'))

    >>> pd.get_dummies(s)

       a  b  c
    0  1  0  0
    1  0  1  0
    2  0  0  1
    3  1  0  0
    ```

- [python - Reversing 'one-hot' encoding in Pandas - Stack Overflow](https://stackoverflow.com/questions/38334296/reversing-one-hot-encoding-in-pandas)

    > **UPDATE:** i think [ayhan](https://stackoverflow.com/questions/38334296/reversing-one-hot-encoding-in-pandas/38334528?noredirect=1#comment64090931_38334528) is right and it should be:
    > 
    > ```
    > df.idxmax(axis=1)
    > ```
    > 
    > Demo:
    > 
    > ```
    > In [40]: s = pd.Series(['dog', 'cat', 'dog', 'bird', 'fox', 'dog'])
    > 
    > In [41]: s
    > Out[41]:
    > 0     dog
    > 1     cat
    > 2     dog
    > 3    bird
    > 4     fox
    > 5     dog
    > dtype: object
    > 
    > In [42]: pd.get_dummies(s)
    > Out[42]:
    >    bird  cat  dog  fox
    > 0   0.0  0.0  1.0  0.0
    > 1   0.0  1.0  0.0  0.0
    > 2   0.0  0.0  1.0  0.0
    > 3   1.0  0.0  0.0  0.0
    > 4   0.0  0.0  0.0  1.0
    > 5   0.0  0.0  1.0  0.0
    > 
    > In [43]: pd.get_dummies(s).idxmax(1)
    > Out[43]:
    > 0     dog
    > 1     cat
    > 2     dog
    > 3    bird
    > 4     fox
    > 5     dog
    > dtype: object
    > ```

## column assignment

- [Adding new column to existing DataFrame in Python pandas - Stack Overflow](https://stackoverflow.com/questions/12555323/adding-new-column-to-existing-dataframe-in-python-pandas)

    > A pandas dataframe is implemented as an ordered dict of columns.
    > 
    > This means that the `__getitem__` `[]` can not only be used to get a certain column, but `__setitem__` `[] =` can be used to assign a new column.
    > 
    > For example, this dataframe can have a column added to it by simply using the `[]` accessor
    > 
    > ```
    >     size      name color
    > 0    big      rose   red
    > 1  small    violet  blue
    > 2  small     tulip   red
    > 3  small  harebell  blue
    > 
    > df['protected'] = ['no', 'no', 'no', 'yes']
    > 
    >     size      name color protected
    > 0    big      rose   red        no
    > 1  small    violet  blue        no
    > 2  small     tulip   red        no
    > 3  small  harebell  blue       yes
    > ```
    > 
    > Note that this works even if the index of the dataframe is off.
    > 
    > ```
    > df.index = [3,2,1,0]
    > df['protected'] = ['no', 'no', 'no', 'yes']
    >     size      name color protected
    > 3    big      rose   red        no
    > 2  small    violet  blue        no
    > 1  small     tulip   red        no
    > 0  small  harebell  blue       yes
    > ```
    > 
    > ### \[\]= is the way to go, but watch out!
    > 
    > However, if you have a `pd.Series` and try to assign it to a dataframe where the indexes are off, you will run in to trouble. See example:
    > 
    > ```
    > df['protected'] = pd.Series(['no', 'no', 'no', 'yes'])
    >     size      name color protected
    > 3    big      rose   red       yes
    > 2  small    violet  blue        no
    > 1  small     tulip   red        no
    > 0  small  harebell  blue        no
    > ```
    > 
    > This is because a `pd.Series` by default has an index enumerated from 0 to n. And the pandas `[] =` method **tries** _to be "smart"_
    > 

## adding rows

- [python - add one row in a pandas.DataFrame - Stack Overflow](https://stackoverflow.com/questions/10715965/add-one-row-in-a-pandas-dataframe)

    ```python
    mycolumns = ['A', 'B']
    df = pd.DataFrame(columns=mycolumns)
    rows = [[1,2],[3,4],[5,6]]
    for row in rows:
        df.loc[len(df)] = row
    ```

## select rows

- [python - Select rows from a DataFrame based on values in a column in pandas - Stack Overflow](https://stackoverflow.com/questions/17071871/select-rows-from-a-dataframe-based-on-values-in-a-column-in-pandas)

    > To select rows whose column value equals a scalar, `some_value`, use `==`:
    > 
    > ```
    > df.loc[df['column_name'] == some_value]
    > ```
    > 
    > To select rows whose column value is in an iterable, `some_values`, use `isin`:
    > 
    > ```
    > df.loc[df['column_name'].isin(some_values)]
    > ```
    > 
    > Combine multiple conditions with `&`:
    > 
    > ```
    > df.loc[(df['column_name'] == some_value) & df['other_column'].isin(some_values)]
    > ```
    > 
    > ---
    > 
    > To select rows whose column value _does not equal_ `some_value`, use `!=`:
    > 
    > ```
    > df.loc[df['column_name'] != some_value]
    > ```
    > 
    > `isin` returns a boolean Series, so to select rows whose value is _not_ in `some_values`, negate the boolean Series using `~`:
    > 
    > ```
    > df.loc[~df['column_name'].isin(some_values)]
    > ```
    > 
    > ---
    > 
    > For example,
    > 
    > ```
    > import pandas as pd
    > import numpy as np
    > df = pd.DataFrame({'A': 'foo bar foo bar foo bar foo foo'.split(),
    >                    'B': 'one one two three two two one three'.split(),
    >                    'C': np.arange(8), 'D': np.arange(8) * 2})
    > print(df)
    > #      A      B  C   D
    > # 0  foo    one  0   0
    > # 1  bar    one  1   2
    > # 2  foo    two  2   4
    > # 3  bar  three  3   6
    > # 4  foo    two  4   8
    > # 5  bar    two  5  10
    > # 6  foo    one  6  12
    > # 7  foo  three  7  14
    > 
    > print(df.loc[df['A'] == 'foo'])
    > ```
    > 
    > yields
    > 
    > ```
    >      A      B  C   D
    > 0  foo    one  0   0
    > 2  foo    two  2   4
    > 4  foo    two  4   8
    > 6  foo    one  6  12
    > 7  foo  three  7  14
    > ```
    > 
    > ---
    > 
    > If you have multiple values you want to include, put them in a list (or more generally, any iterable) and use `isin`:
    > 
    > ```
    > print(df.loc[df['B'].isin(['one','three'])])
    > ```
    > 
    > yields
    > 
    > ```
    >      A      B  C   D
    > 0  foo    one  0   0
    > 1  bar    one  1   2
    > 3  bar  three  3   6
    > 6  foo    one  6  12
    > 7  foo  three  7  14
    > ```
    > 
    > ---
    > 
    > Note, however, that if you wish to do this many times, it is more efficient to make an index first, and then use `df.loc`:
    > 
    > ```
    > df = df.set_index(['B'])
    > print(df.loc['one'])
    > ```
    > 
    > yields
    > 
    > ```
    >        A  C   D
    > B              
    > one  foo  0   0
    > one  bar  1   2
    > one  foo  6  12
    > ```
    > 
    > or, to include multiple values from the index use `df.index.isin`:
    > 
    > ```
    > df.loc[df.index.isin(['one','two'])]
    > ```
    > 
    > yields
    > 
    > ```
    >        A  C   D
    > B              
    > one  foo  0   0
    > one  bar  1   2
    > two  foo  2   4
    > two  foo  4   8
    > two  bar  5  10
    > one  foo  6  12
    > ```
    > 




## NaN & None

- [Python 中 NaN 和 None 的详细比较 - Python - 伯乐在线](http://python.jobbole.com/87266/)

    > __None vs NaN要点总结__
    > 
    > 1. 在pandas中， 如果其他的数据都是数值类型， pandas会把None自动替换成NaN, 甚至能将s[s.isnull()]= None,和s.replace(NaN, None)操作的效果无效化。 这时需要用where函数才能进行替换。
    > 
    > 2. None能够直接被导入数据库作为空值处理， 包含NaN的数据导入时会报错。
    > 
    > 3. numpy和pandas的很多函数能处理NaN，但是如果遇到None就会报错。
    > 
    > 4. None和NaN都不能被pandas的groupby函数处理，包含None或者NaN的组都会被忽略。
    > 
    > 等值性比较的总结:（True表示被判定为相等）
    > 
    > ||None对None |	NaN对NaN |	None对NaN|
    > |--|--|--|--|--|
    > |单值 |	True |	False |	False|
    > |tuple(整体) |	True |	True |	False|
    > |np.array(逐个) |	True |	False |	False|
    > |Series(逐个) |	False |	False |	False|
    > |assert_equals| 	True |	True |	False|
    > |Series.equals |	True |	True |	True|
    > |merge |	True |	True |	True|
    > 
    > 由于等值性比较方面，None和NaN在各场景下表现不太一致，相对来说None表现的更稳定。
    > 
    > 为了不给自己惹不必要的麻烦和额外的记忆负担。 实践中，建议遵循以下三个原则即可
    > 
    > - 在用pandas和numpy处理数据阶段将None,NaN统一处理成NaN,以便支持更多的函数。
    > 
    > - 如果要判断Series,numpy.array整体的等值性，用专门的Series.equals,numpy.array函数去处理，不要自己用==判断 *
    > 
    > - 如果要将数据导入数据库，将NaN替换成None
    > 

- [null object in Python? - Stack Overflow](https://stackoverflow.com/questions/3289601/null-object-in-python)


    > In Python, the 'null' object is the singleton None.
    > 
    > The best way to check things for "Noneness" is to use the identity operator, is:
    > ```python
    > if foo is None:
    >     ...
    > ```
    > 


## print pandas DataFrame without index

- [python - How to print pandas DataFrame without index - Stack Overflow](https://stackoverflow.com/questions/24644656/how-to-print-pandas-dataframe-without-index)

    > ```py
    > print df.to_string(index=False)
    > ```


## Remove name of Row Index

- [python - Remove Row Index dataframe pandas - Stack Overflow](https://stackoverflow.com/questions/43716402/remove-row-index-dataframe-pandas)

    > `FACTOR` is the name of the index - you shouldn't worry about it - it doesn't affect your data:
    > 
    > ```py
    > In [78]: df
    > Out[78]:
    >               DATE  REVENUE  COST  POSITION
    > FACTOR
    > 10      2017/01/01     1000   900        10
    > 11      2017/01/01      900   700         9
    > 12      2017/01/01     1100   800         7
    > 
    > In [79]: df.index.name
    > Out[79]: 'FACTOR'
    > ```
    > 
    > If you want to rename it or to get rid of it (preserving the index values) you can use [DataFrame.rename_axis()](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.rename_axis.html) method:
    > 
    > ```py
    > In [80]: df = df.rename_axis(None)
    > 
    > In [81]: df
    > Out[81]:
    >           DATE  REVENUE  COST  POSITION
    > 10  2017/01/01     1000   900        10
    > 11  2017/01/01      900   700         9
    > 12  2017/01/01     1100   800         7
    > 
    > In [82]: df.index.name is None
    > Out[82]: True
    > ```
    > 

## batch process all the values of Dataframe

- [python - pandas how to batch process all the values - Stack Overflow](https://stackoverflow.com/questions/32840905/pandas-how-to-batch-process-all-the-values)

    > You can call [`apply`](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.apply.html#pandas.DataFrame.apply) with a lambda that calls the vectorise [`str`](http://pandas.pydata.org/pandas-docs/stable/api.html#string-handling) methods to slice your strings:
    > 
    > ```python
    > In [136]:
    > df = pd.DataFrame({'a':['asdas','asdasdsadas','123124'],'b':['554653645','546456453634','uyiyasdhnfjnas']})
    > df
    > 
    > Out[136]:
    >              a               b
    > 0        asdas       554653645
    > 1  asdasdsadas    546456453634
    > 2       123124  uyiyasdhnfjnas
    > 
    > In [138]:
    > df.apply(lambda x: x.str[:4])
    > 
    > Out[138]:
    >       a     b
    > 0  asda  5546
    > 1  asda  5464
    > 2  1231  uyiy
    > ```

## dataframe operation

### append

- [python - Formatting dataframe in appending - Stack Overflow](https://stackoverflow.com/questions/33346904/formatting-dataframe-in-appending)

    > You need to change one column name, so `append` can detect hat you want to do:
    > 
    > ```
    > data2.columns = ["a"]
    > ```
    > 
    > or
    > 
    > ```
    > data1.columns = ["b"]
    > ```
    > 
    > And then, after using `data2.columns = ["a"]`:
    > 
    > ```
    > all_data = data1.append(data2, ignore_index=True)
    > all_data
    >    a
    > 0  a
    > 1  b
    > 2  c
    > 3  d
    > 4  e
    > 5  f
    > 6  g
    > 7  h
    > 8  i
    > 9  j
    > ```
    > 
    > And here you have your column named after the column's name of data1, which you can rename if you want:
    > 
    > ```
    > all_data.columns = ["Foo"]
    > ```


## file oerpation

### read_excel(), to_execl()

- [pandas.read_excel — pandas 0.23.4 documentation](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_excel.html)
```
>>> pd.read_excel('tmp.xlsx')
```

### to_csv()

- [pandas.DataFrame.to_csv — pandas 0.23.4 documentation](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.to_csv.html#)

- [python - Pandas writing dataframe to CSV file - Stack Overflow](https://stackoverflow.com/questions/16923281/pandas-writing-dataframe-to-csv-file)

    > To delimit by a tab you can use the `sep` argument of [`to_csv`](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.to_csv.html):
    > 
    > ```
    > df.to_csv(file_name, sep='\t')
    > ```
    > 
    > To use a specific encoding (e.g. 'utf-8') use the `encoding` argument:
    > 
    > ```
    > df.to_csv(file_name, sep='\t', encoding='utf-8')
    > ```

## data operation

### random sample

- [pandas.DataFrame.sample — pandas 0.23.4 documentation](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.sample.html)

    > 
    > 3 random elements from the `Series`:
    > 
    > ```py
    > >>> s.sample(n=3)
    > ```
    > ---
    > 
    > And a random 10% of the `DataFrame` with replacement:
    > 
    > ```py
    > >>> df.sample(frac=0.1, replace=True)
    > ```
    > ---
    > 
    > You can use *random state* for reproducibility:
    > 
    > ```py
    > >>> df.sample(random_state=1)
    > ```
    > 

## batch operation

### apply with axis

- [pandas.DataFrame.apply — pandas 0.23.4 documentation](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.apply.html)

    > ```py
    > df[["filename","ID"]].apply(lambda x: copy2(x[0], save_dir+x[1]+'.json'), axis=1)
    > ```

### apply a function with arguments

- [python pandas: apply a function with arguments to a series - Stack Overflow](https://stackoverflow.com/questions/12182744/python-pandas-apply-a-function-with-arguments-to-a-series)

    > Let's created a normal function with two arguments to control the min and max values we want in our Series.
    > 
    > ```python
    > def between(x, low, high):
    >     return x >= low and x =< high
    > ```
    > 
    > We can replicate the output of the first function by passing unnamed arguments to `args`:
    > 
    > ```python
    > s.apply(between, args=(3,6))
    > ```
    > 
    > Or we can use the named arguments
    > 
    > ```python
    > s.apply(between, low=3, high=6)
    > ```
    > 
    > Or even a combination of both
    > 
    > ```python
    > s.apply(between, args=(3,), high=6)
    > ```
    > 
    > ---
    > 
    > The documentation explains this clearly. The apply method accepts a python function which should have a single parameter. If you want to pass more parameters you should use `functools.partial` as suggested by Joel Cornett in his comment.
    > 
    > An example:
    > 
    > ```python
    > >>> import functools
    > >>> import operator
    > >>> add_3 = functools.partial(operator.add,3)
    > >>> add_3(2)
    > 5
    > >>> add_3(7)
    > 10
    > ```
    > 
    > You can also pass keyword arguments using `partial`.




# scikit-learn
- [sklearn.preprocessing.MinMaxScaler — scikit-learn 0.19.1 documentation](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.MinMaxScaler.html)
    Transforms features by scaling each feature to a given range.

- [sklearn.preprocessing.StandardScaler — scikit-learn 0.19.1 documentation](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.StandardScaler.html)
    Standardize features by removing the mean and scaling to unit variance



- [scipy.sparse.csr_matrix — SciPy v1.0.0 Reference Guide](https://docs.scipy.org/doc/scipy/reference/generated/scipy.sparse.csr_matrix.html)
    > Compressed Sparse Row matrix
    > 
    > __Advantages of the CSR format__
    > 
    > -   efficient arithmetic operations CSR + CSR, CSR * CSR, etc.
    > -   efficient row slicing
    > -   fast matrix vector products
    > 
    > __Disadvantages of the CSR format__
    > 
    > -   slow column slicing operations (consider CSC)
    > -   changes to the sparsity structure are expensive (consider LIL or DOK)

    - [scipy.sparse.csr_matrix.todense — SciPy v1.0.0 Reference Guide](https://docs.scipy.org/doc/scipy/reference/generated/scipy.sparse.csr_matrix.todense.html#scipy.sparse.csr_matrix.todense)
        Return a dense matrix representation of this matrix.

    - [scipy.sparse.csr_matrix.toarray — SciPy v1.0.0 Reference Guide](https://docs.scipy.org/doc/scipy/reference/generated/scipy.sparse.csr_matrix.toarray.html)
        Return a dense ndarray representation of this matrix.

    - [scipy.sparse.csr_matrix.sum — SciPy v1.0.0 Reference Guide](https://docs.scipy.org/doc/scipy/reference/generated/scipy.sparse.csr_matrix.sum.html#scipy.sparse.csr_matrix.sum)
        Sum the matrix elements over a given axis.

- [sklearn.feature_extraction.text.CountVectorizer — scikit-learn 0.19.1 documentation](http://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.CountVectorizer.html#sklearn.feature_extraction.text.CountVectorizer)

    > Convert a collection of text documents to a matrix of token counts
    > 
    > This implementation produces a sparse representation of the counts using scipy.sparse.csr_matrix.
    > 
    > If you do not provide an a-priori dictionary and you do not use an analyzer that does some kind of feature selection then the number of features will be equal to the vocabulary size found by analyzing the data.

    - [sklearn.feature_extraction.text.CountVectorizer.fit_transform — scikit-learn 0.19.1 documentation](http://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.CountVectorizer.html#sklearn.feature_extraction.text.CountVectorizer.fit_transform)
        Learn the vocabulary dictionary and return term-document matrix.


    - [python - Can I use CountVectorizer in scikit-learn to count frequency of documents that were not used to extract the tokens? - Stack Overflow](https://stackoverflow.com/questions/22920801/can-i-use-countvectorizer-in-scikit-learn-to-count-frequency-of-documents-that-w)

        > You're right that `vocabulary` is what you want. It works like this:
        > 
        > ```
        > >>> cv = sklearn.feature_extraction.text.CountVectorizer(vocabulary=['hot', 'cold', 'old'])
        > >>> cv.fit_transform(['pease porridge hot', 'pease porridge cold', 'pease porridge in the pot', 'nine days old']).toarray()
        > array([[1, 0, 0],
        >        [0, 1, 0],
        >        [0, 0, 0],
        >        [0, 0, 1]], dtype=int64)
        > ```
        > 
        > So you pass it a dict with your desired features as the keys.
        > 
        > If you used `CountVectorizer` on one set of documents and then you want to use the set of features from those documents for a new set, use the `vocabulary_` attribute of your original CountVectorizer and pass it to the new one. So in your example, you could do
        > 
        > ```
        > newVec = CountVectorizer(vocabulary=vec.vocabulary_)
        > ```
        > 
        > to create a new tokenizer using the vocabulary from your first one.

- [MemoryError · Issue #40 · scikit-learn-contrib/imbalanced-learn](https://github.com/scikit-learn-contrib/imbalanced-learn/issues/40)
    MemoryError while using toarray(), todense()
    > This simple solution to handle sparse data is simply to turn it to dense array as you see here:  
    > `File "C:\Python34\lib\site-packages\unbalanceddataset-0.1-py3.4.egg\unbalanced_dataset\utils.py", line 36, in concatenate return sp.vstack(l).todense()`
    > 
    > Unfortunately, this implementation is simply not suited to work with sparse data intelligently, and you you turn your (probably) massive sparse matrix of 500k and probably a few thousand columns, you run out of RAM.
    > 


## score matrics

- [sklearn.metrics.roc_auc_score — scikit-learn 0.19.1 documentation](http://scikit-learn.org/stable/modules/generated/sklearn.metrics.roc_auc_score.html#sklearn.metrics.roc_auc_score)

    > Compute Area Under the Receiver Operating Characteristic Curve (ROC AUC) from prediction scores.

    > Examples
    > 
    > ```python
    > >>> import numpy as np
    > >>> from sklearn.metrics import roc_auc_score
    > >>> y_true = np.array([0, 0, 1, 1])
    > >>> y_scores = np.array([0.1, 0.4, 0.35, 0.8])
    > >>> roc_auc_score(y_true, y_scores)
    > 0.75
    > ```

## one-hot encode

- [sklearn.preprocessing.OneHotEncoder — scikit-learn 0.19.2 documentation](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html)

    > Examples
    > 
    > Given a dataset with three features and four samples, we let the encoder find the maximum value per feature and transform the data to a binary one-hot encoding.
    > 
    > 
    > ```python
    > >>> from sklearn.preprocessing import OneHotEncoder
    > >>> enc = OneHotEncoder()
    > >>> enc.fit([[0, 0, 3], [1, 1, 0], [0, 2, 1], [1, 0, 2]])
    > OneHotEncoder(categorical_features='all', dtype=<... 'numpy.float64'>,
    >  handle_unknown='error', n_values='auto', sparse=True)
    > >>> enc.n_values_
    > # 從左到右，
    > # 第一個feature 有2個值(0,1)
    > # 第二個feature 有3個值(0,1,2)
    > # 第三個feature 有4個值(0,1,2,3)
    > array([2, 3, 4])
    > >>> enc.feature_indices_
    > # 從左到右，
    > # 第一個feature轉成one-hot後使用的index為0,1 [0,2]
    > # 第二個feature轉成one-hot後使用的index為2,3,4 [2,5]
    > # 第三個feature轉成one-hot後使用的index為5,6,7,8 [5,9]
    > array([0, 2, 5, 9])
    > >>> enc.transform([[0, 1, 1]]).toarray()
    > # 從左到右，
    > # 第一個feature 為0 轉成one-hot後為[1,0]
    > # 第二個feature 為1 轉成one-hot後為[0,1,0]
    > # 第三個feature 為1 轉成one-hot後為[0,1,0,0]
    > # 合起來便是[[1,0],[0,1,0],[0,1,0,0]]
    > array([[ 1.,  0.,  0.,  1.,  0.,  0.,  1.,  0.,  0.]])
    > ```




# jieba 結巴 中文斷詞

- [Python中文分词 jieba 十五分钟入门与进阶 - CSDN博客](https://blog.csdn.net/fontthrone/article/details/72782499)
- [结巴中文分词的用法 - 简书](https://www.jianshu.com/p/e8b5d01ca073)
- 

- [fxsjy/jieba: 结巴中文分词](https://github.com/fxsjy/jieba)

    ```python
    >>> import jieba.posseg as pseg
    >>> words = pseg.cut("我爱北京天安门")
    >>> for word, flag in words:
    ...    print('%s %s' % (word, flag))
    ...
    我 r
    爱 v
    北京 ns
    天安门 ns
    ```
- [jieba（结巴）分词种词性简介 - CSDN博客](http://blog.csdn.net/suibianshen2012/article/details/53487157)

    |代號|詞性|解釋|
    |------------------|---------------------|---------------------|
    | Ag | 形语素 | 形容词性语素。形容词代码为 a，语素代码ｇ前面置以A。 |
    | a | 形容词 | 取英语形容词 adjective的第1个字母。 |
    | ad | 副形词 | 直接作状语的形容词。形容词代码 a和副词代码d并在一起。 |
    | an | 名形词 | 具有名词功能的形容词。形容词代码 a和名词代码n并在一起。 |
    | b | 区别词 | 取汉字“别”的声母。 |
    | c | 连词 | 取英语连词 conjunction的第1个字母。 |
    | dg | 副语素 | 副词性语素。副词代码为 d，语素代码ｇ前面置以D。 |
    | d | 副词 | 取 adverb的第2个字母，因其第1个字母已用于形容词。 |
    | e | 叹词 | 取英语叹词 exclamation的第1个字母。 |
    | f | 方位词 | 取汉字“方” |
    | g | 语素 | 绝大多数语素都能作为合成词的“词根”，取汉字“根”的声母。 |
    | h | 前接成分 | 取英语 head的第1个字母。|
    | i | 成语 | 取英语成语 idiom的第1个字母。|
    | j | 简称略语 | 取汉字“简”的声母。 |
    | k | 后接成分 |   |
    | l | 习用语 | 习用语尚未成为成语，有点“临时性”，取“临”的声母。 |
    | m | 数词 | 取英语 numeral的第3个字母，n，u已有他用。 |
    | Ng | 名语素 | 名词性语素。名词代码为 n，语素代码ｇ前面置以N。 |
    | n | 名词 | 取英语名词 noun的第1个字母。|
    | nr | 人名 | 名词代码 n和“人(ren)”的声母并在一起。 |
    | ns | 地名 | 名词代码 n和处所词代码s并在一起。 |
    | nt | 机构团体 | “团”的声母为 t，名词代码n和t并在一起。 |
    | nz | 其他专名 | “专”的声母的第 1个字母为z，名词代码n和z并在一起。 |
    | o | 拟声词 | 取英语拟声词 onomatopoeia的第1个字母。 |
    | p | 介词 | 取英语介词 prepositional的第1个字母。 |
    | q | 量词 | 取英语 quantity的第1个字母。|
    | r | 代词 | 取英语代词 pronoun的第2个字母,因p已用于介词。 |
    | s | 处所词 | 取英语 space的第1个字母。 |
    | tg | 时语素 | 时间词性语素。时间词代码为 t,在语素的代码g前面置以T。 |
    | t | 时间词 | 取英语 time的第1个字母。 |
    | u | 助词 | 取英语助词 auxiliary |
    | vg | 动语素 | 动词性语素。动词代码为 v。在语素的代码g前面置以V。 |
    | v | 动词 | 取英语动词 verb的第一个字母。 |
    | vd | 副动词 | 直接作状语的动词。动词和副词的代码并在一起。 |
    | vn | 名动词 | 指具有名词功能的动词。动词和名词的代码并在一起。 |
    | w | 标点符号 |   |
    | x | 非语素字 | 非语素字只是一个符号，字母 x通常用于代表未知数、符号。 |
    | y | 语气词 | 取汉字“语”的声母。 |
    | z | 状态词 | 取汉字“状”的声母的前一个字母。 |
    | un | 未知词 | 不可识别词及用户自定义词组。取英文Unkonwn首两个字母。(非北大标准，CSW分词中定义) |


# gensim

- [gensim: models.word2vec – Deep learning with word2vec](https://radimrehurek.com/gensim/models/word2vec.html)



# Graphviz

- [Download](https://graphviz.gitlab.io/download/)


# Machine Learning Algorithm

## PCA

- [PCA(主成分分析)python实现 - 简书](https://www.jianshu.com/p/4528aaa6dc48)


## XGBoost

- [XGBoost 与 Boosted Tree – 我爱计算机](http://www.52cs.org/?p=429)

- [Complete Guide to Parameter Tuning in XGBoost (with codes in Python)](https://www.analyticsvidhya.com/blog/2016/03/complete-guide-parameter-tuning-xgboost-with-codes-python/)

- [[1603.02754] XGBoost: A Scalable Tree Boosting System](https://arxiv.org/abs/1603.02754)



### Mathematics Behind XGBoost

- [Unveiling Mathematics Behind XGBoost](https://www.kdnuggets.com/2018/08/unveiling-mathematics-behind-xgboost.html)

    > ### **Curious case of John and Emily**
    > ![](https://cdn-images-1.medium.com/max/720/1*mWtNfyZwXju3-tZfRFYcng.jpeg)
    > 
    > John and Emily embarked on an adventure to pluck apples from the tree located at the lowest point of the mountain. While Emily is a smart and adventurous girl, John is a bit cautious and sluggish. However, only John can climb tree and pluck apples. We will see how they achieve their goal.\
    > ![](https://cdn-images-1.medium.com/max/720/1*LA8TV-PCjh1on6MQ1LxOVw.jpeg)
    > 
    > John and Emily start at point 'a' on the mountain and tree is located at point 'g'. There are two ways they can reach point 'g':
    > 
    > 1\. Emily calculates the slope of the curve at point 'a'; if the slope is positive, they move in the opposite direction or else in the same direction. However, slope gives direction but doesn't tell how much they need to move in that direction. Therefore, Emily decides to take small step and repeat the process, so they don't end up at the wrong point. While the direction of the step is controlled by the negative gradient, the magnitude of the step is controlled by the learning rate. If the magnitude is either too high or too low, they may end up at a wrong point or take way too long to reach to point 'g'.\
    > ![](https://cdn-images-1.medium.com/max/720/1*wQXYeg4Jrvb-4a3Nz4SP7w.jpeg)
    > 
    > John is skeptical about this approach and doesn't want to walk more if by chance they end up at the wrong point. So Emily comes up with a new approach:
    > 
    > 2\. Emily suggests that she will first go to next potential points and calculate the value of the loss function at those points. She keeps a note of the value of the function at all those points, and she will signal John to come to that point where the value is least. John loved this approach as he will never end up at a wrong point. However, poor Emily need to explore all points in her neighborhood and calculate the value of the function at all those points. The beauty of XGBoost is it intelligently tackles both these problems.
    > 
    > Please be advised I may use function/base learner/tree interchangeably.
    > 
    > ### **Gradient Boosting**
    > Many implementations of Gradient Boosting follow approach 1 to minimize the objective function. At every iteration, we fit a base learner to the negative gradient of the loss function and multiply our prediction with a constant and add it to the value from previous iteration.
    > 
    > ![](https://cdn-images-1.medium.com/max/720/1*Ghv8bGUk0zzYfUouEJYuyw.png)\
    > [Source: Wikipedia](https://en.wikipedia.org/wiki/Gradient_boosting)
    > 
    > The intuition is by fitting a base learner to the negative gradient at each iteration is essentially performing gradient descent on the loss function. The negative gradients are often called as pseudo residuals, as they indirectly help us to minimize the objective function.
    > 
    > ### **XGBoost**
    > It was a result of research by Tianqi Chen, Ph.D. student at University of Washington. XGBoost is an ensemble additive model that is composed of several base learners.\
    > ![](https://cdn-images-1.medium.com/max/720/1*hyVH1RhJaDkDksy7_f4Ocw.jpeg)
    > 
    > How should we chose a function at each iteration? we chose a function that minimizes the overall loss.\
    > ![](https://cdn-images-1.medium.com/max/720/1*pzR03dxcSOhn2tnKtAXo3A.jpeg)
    > 
    > In the gradient boosting algorithm stated above, we obtained f~t~(x~i~) at each iteration by fitting a base learner to the negative gradient of loss function with respect to previous iteration's value. In XGBoost, we explore several base learners or functions and pick a function that minimizes the loss (Emily's second approach). As I stated above, there are two problems with this approach:\
    > 1\. exploring different base learners\
    > 2\. calculating the value of the loss function for all those base learners.
    > 
    > XGBoost uses Taylor series to approximate the value of the loss function for a base learner f~t~(x~i~), thus, reducing the load on Emily to calculate the exact loss for different possible base learners.\
    > ![](https://cdn-images-1.medium.com/max/720/1*TZDFiZ8EaBUbv8POwgAwcQ.jpeg)
    > 
    > It only uses expansion up to second order derivative assuming this level of approximation would be suffice. The first term 'C' is constant irrespective of any f~t~(x~i~) we pick. 'g~i~' is the first order derivative of loss at previous iteration with respect predictions at previous iteration. 'h~i~' is the second order derivative of loss at previous iteration with respect to predictions at previous iteration. Therefore, Emily can calculate 'g~i~' and 'f~i~' before starting exploring different base learners, as it will be just a matter of multiplications thereafter. Plug and play, isn't it?
    > 
    > So XGBoost has reduced one of the burdens on Emily. Still we have a problem of exploring different base learners.\
    > ![](https://cdn-images-1.medium.com/max/720/1*Sku1s6Y2NYyh71scMy8fSA.jpeg)
    > 
    > Assume Emily fixed a base learner ft that has 'K' leaf nodes. Let I~j~ be the set of instances belonging to node 'j' and 'w~j~' be the prediction for that node. So for an instance 'i' belonging to I~j~, f~t~(x~i~)=w~j~. Therefore, we obtained equation 3 from equation 2 by substituting f~t~(x~i~) with respective predictions. After substituting the predictions, we can take the derivative of loss function with respect to each leaf node's weight, to get an optimal weight.\
    > ![](https://cdn-images-1.medium.com/max/720/1*-tt8E0OzV2O2pKH6v5wMuQ.jpeg)
    > 
    > Substituting the optimal weights back into equation 3 gives equation 4. However, this is the optimal loss for a fixed tree structure. There will be several hundreds of possible trees.
    > 
    > Let's formulate the current position of Emily. She now knows how to ease the burden of computing loss using Taylor expansion. She knows for a fixed tree structure what should be the optimal weights in the leaf node. The only thing that is still a concern is how to explore all different possible tree structures.\
    > ![](https://cdn-images-1.medium.com/max/720/1*De1hXISG0y_7iL6OhxrJIw.jpeg)
    > 
    > Instead of exploring all possible tree structures, XGBoost greedily builds a tree. The split that results in maximum loss reduction is chosen. In the above picture, the tree starts at Node 'I'. Based on some split criteria, the node is divided into left and right branches. So some instances fall in left node and other instances fall in right leaf node. Now, we can calculate the reduction in loss and pick the split that causes best reduction in loss.
    > 
    > But still Emily has one more problem. How to chose the split criteria? XGBoost uses different tricks to come up with different split points like histogram, exact, etc. I will not be dealing with that part, as this article has already grown in size.\
    > **Bullet Points to Remember**
    > 
    > 1.  While Gradient Boosting follows negative gradients to optimize the loss function, XGBoost uses Taylor expansion to calculate the value of the loss function for different base learners. Here is the best video on the internet that explains [Taylor expansion](https://www.youtube.com/watch?v=3d6DsjIBzJ4&t=447s).
    > 2.  XGBoost doesn't explore all possible tree structures but builds a tree greedily.
    > 3.  XGBoost's regularization term penalizes building complex tree with several leaf nodes.
    > 4.  XGBoost has several other tricks under its sleeve like Column subsampling, shrinkage, splitting criteria, etc. I highly recommend continue reading the original paper [here](https://arxiv.org/pdf/1603.02754.pdf).
    > 
    > You can view the complete derivation [here](https://drive.google.com/open?id=1CmNhi-7pZFnCEOJ9g7LQXwuIwom0ZN_D).
    > 
    > Read my other article on PCA [here](https://www.linkedin.com/pulse/eigendecomposition-singular-value-decomposition-ajit-samudrala/).\
    > **Bio: [Ajit Samudrala](https://www.linkedin.com/in/ajitsamudrala/)** is an aspiring Data Scientist and Data Science intern at SiriusXM.
    > 
    > [Original](https://medium.com/@samudralaajit/unveiling-mathematics-behind-xgboost-c7f1b8201e2a). Reposted with permission.
    > 


### Leaf Encoding

- [predicting-clicks-facebook.pdf](http://quinonero.net/Publications/predicting-clicks-facebook.pdf)

- [Python API Reference — xgboost 0.7 documentation](https://xgboost.readthedocs.io/en/latest/python/python_api.html#module-xgboost.sklearn)

    ![](https://screenshotscdn.firefoxusercontent.com/images/4eb1256c-81e9-4c91-af15-d5325f57f5c8.png)

### Save model & load model

- [How to Save Gradient Boosting Models with XGBoost in Python - Machine Learning Mastery](https://machinelearningmastery.com/save-gradient-boosting-models-xgboost-python/)

    > Serialize Your XGBoost Model with Pickle
    > ----------------------------------------
    > 
    > Pickle is the standard way of serializing objects in Python.
    > 
    > You can use the [Python pickle API](https://docs.python.org/2/library/pickle.html) to serialize your machine learning algorithms and save the serialized format to a file, for example:


    > ```python
    > # Train XGBoost model, save to file using pickle, load and make predictions
    > from numpy import loadtxt
    > import xgboost
    > import pickle
    > from sklearn import model_selection
    > from sklearn.metrics import accuracy_score
    > # load data
    > dataset = loadtxt('pima-indians-diabetes.csv', delimiter=",")
    > # split data into X and y
    > X = dataset[:,0:8]
    > Y = dataset[:,8]
    > # split data into train and test sets
    > seed = 7
    > test_size = 0.33
    > X_train, X_test, y_train, y_test = cross_validation.train_test_split(X, Y, test_size=test_size, random_state=seed)
    > # fit model no training data
    > model = xgboost.XGBClassifier()
    > model.fit(X_train, y_train)
    > # save model to file
    > pickle.dump(model, open("pima.pickle.dat", "wb"))
    > 
    > # some time later...
    > 
    > # load model from file
    > loaded_model = pickle.load(open("pima.pickle.dat", "rb"))
    > # make predictions for test data
    > y_pred = loaded_model.predict(X_test)
    > predictions = [round(value) for value in y_pred]
    > # evaluate predictions
    > accuracy = accuracy_score(y_test, predictions)
    > print("Accuracy: %.2f%%" % (accuracy * 100.0))
    > ```



## CatBoost

- [CatBoost — Transforming categorical features to numerical features — Yandex Technologies](https://tech.yandex.com/catboost/doc/dg/concepts/algorithm-main-stages_cat-to-numberic-docpage/)

內建 Mean Encoding = Target Encoding



## Hierarchical Clustering

- [利用 SciPy 实现层次聚类 - Haojun's Blog](https://haojunsui.github.io/2016/07/16/scipy-hac/)


# Kaggle


- [Data Science London + Scikit-learn | Kaggle](https://www.kaggle.com/c/data-science-london-scikit-learn)

- [House Prices: Advanced Regression Techniques | Kaggle](https://www.kaggle.com/c/house-prices-advanced-regression-techniques)

- [Heritage Health Prize | Kaggle](https://www.kaggle.com/c/hhp#milestone-winners)

- [Stacked Regressions : Top 4% on LeaderBoard | Kaggle](https://www.kaggle.com/serigne/stacked-regressions-top-4-on-leaderboard)



# Model Tuning

- [Scanning hyperspace: how to tune machine learning models | Cambridge Coding Academy](https://cambridgecoding.wordpress.com/2016/04/03/scanning-hyperspace-how-to-tune-machine-learning-models/)
- 


# Vectorize

- [Speeding up your code (2): vectorizing the loops with Numpy](https://hackernoon.com/speeding-up-your-code-2-vectorizing-the-loops-with-numpy-e380e939bed3)




# Trubleshooting

- [Win10下XGBoost安装方法(本地python3.5和anaconda版) | Code my word](https://denotepython.github.io/2017/03/11/install-xgboost/)

    下载xgboost.whl
    -------------

    因为现在已经出了xgboost的whl版本，所以安装变得十分便捷，首先去[xgboost whl](http://www.lfd.uci.edu/~gohlke/pythonlibs/#xgboost)下载自己对应的版本，我的是`xgboost‑0.6‑cp35‑cp35m‑win_amd64.whl`然后放到任意目录，比如我放到G盘根目录

    anaconda安装xgboost
    -----------------

    首先切换到anaconda下你安装的python3.5版本的目录，因为我是创建的虚拟环境，所以在env目录下 
    `C:\Users\rocket\Anaconda2\envs\python35\Scripts>` 
    切换成功过后，同样输入`pip install G:\xgboost-0.6-cp35-cp35m-win_amd64.whl` 

    ```shell
    Processing g:\xgboost-0.6-cp35-cp35m-win_amd64.whl
    Requirement already satisfied: scipy in c:\\users\rocket\anaconda2\envs\python35\lib\site-packages (from xgboost==0.6)
    Requirement already satisfied: numpy in c:\users\rocket\anaconda2\envs\python35\lib\site-packages (from xgboost==0.6)
    Installing collected packages: xgboost
    Successfully installed xgboost-0.6
    ```




