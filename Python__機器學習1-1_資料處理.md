# Python__機器學習1-1_資料處理

[toc]
<!-- toc --> 


# Numpy

## API

- [Routines — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/reference/routines.html)
    - [Index — NumPy v1.12 Manual](https://docs.scipy.org/doc/numpy-1.12.0/genindex.html)

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

- [numpy.digitize — NumPy v1.15 Manual](https://docs.scipy.org/doc/numpy-1.15.1/reference/generated/numpy.digitize.html)
    Return the indices of the bins to which each value in input array belongs.


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


## create an empty array/matrix

- [python - How do I create an empty array/matrix in NumPy? - Stack Overflow](https://stackoverflow.com/questions/568962/how-do-i-create-an-empty-array-matrix-in-numpy)

    > In the case of adding rows, your best bet is to create an array that is as big as your data set will eventually be, and then add data to it row-by-row:
    > 
    > ```python
    > >>> import numpy
    > >>> a = numpy.zeros(shape=(5,2))
    > >>> a
    > array([[ 0.,  0.],
    >    [ 0.,  0.],
    >    [ 0.,  0.],
    >    [ 0.,  0.],
    >    [ 0.,  0.]])
    > >>> a[0] = [1,2]
    > >>> a[1] = [2,3]
    > >>> a
    > array([[ 1.,  2.],
    >    [ 2.,  3.],
    >    [ 0.,  0.],
    >    [ 0.,  0.],
    >    [ 0.,  0.]])
    > ```


## Resize an existing array and fill with zeros

- [Python: Resize an existing array and fill with zeros - Stack Overflow](https://stackoverflow.com/questions/9251635/python-resize-an-existing-array-and-fill-with-zeros)

    > This solution works with `resize` function
    > 
    > Take a sample array
    > 
    > ```
    > S= np.ones((3))
    > print (S)
    > # [ 1.  1.  1.]
    > d= np.diag(S)
    > print(d)
    > """
    > [[ 1.  0.  0.]
    >  [ 0.  1.  0.]
    >  [ 0.  0.  1.]]
    > 
    > """
    > ```
    > 
    > This **dosent** work, it just add a repeating values
    > 
    > ```
    > np.resize(d,(6,3))
    > """
    > adds a repeating value
    > array([[ 1.,  0.,  0.],
    >        [ 0.,  1.,  0.],
    >        [ 0.,  0.,  1.],
    >        [ 1.,  0.,  0.],
    >        [ 0.,  1.,  0.],
    >        [ 0.,  0.,  1.]])
    > """
    > ```
    > 
    > This **does** work
    > 
    > ```
    > d.resize((6,3),refcheck=False)
    > print(d)
    > """
    > [[ 1.  0.  0.]
    >  [ 0.  1.  0.]
    >  [ 0.  0.  1.]
    >  [ 0.  0.  0.]
    >  [ 0.  0.  0.]
    >  [ 0.  0.  0.]]
    > """
    > ```
    > 

## Zero pad numpy array

- [python - Zero pad numpy array - Stack Overflow](https://stackoverflow.com/questions/38191855/zero-pad-numpy-array)

    > `numpy.pad` with `constant` mode does what you need, where we can pass a tuple as second argument to tell how many zeros to pad on each size, a `(2, 3)` for instance will pad **2** zeros on the left side and **3** zeros on the right side:
    > 
    > Given `A` as:
    > 
    > ```python
    > A = np.array([1,2,3,4,5])
    > 
    > np.pad(A, (2, 3), 'constant')
    > # array([0, 0, 1, 2, 3, 4, 5, 0, 0, 0])
    > ```
    > 
    > It's also possible to pad a 2D numpy arrays by passing a tuple of tuples as padding width, which takes the format of `((top, bottom), (left, right))`:
    > 
    > ```python
    > A = np.array([[1,2],[3,4]])
    > 
    > np.pad(A, ((1,2),(2,1)), 'constant')
    > 
    > #array([[0, 0, 0, 0, 0],           # 1 zero padded to the top
    > #       [0, 0, 1, 2, 0],           # 2 zeros padded to the bottom
    > #       [0, 0, 3, 4, 0],           # 2 zeros padded to the left
    > #       [0, 0, 0, 0, 0],           # 1 zero padded to the right
    > #       [0, 0, 0, 0, 0]])
    > ```
    > 

## reshape array(np.reshape)

- [python - Converting a List of Tuples to numpy array results in single dimension - Stack Overflow](https://stackoverflow.com/questions/40596672/converting-a-list-of-tuples-to-numpy-array-results-in-single-dimension)

    > If I understand your desired output correctly, you can use [`numpy.reshape`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.reshape.html)
    > 
    > ```
    > >>> spp = np.asarray(splist, dt)
    > >>> spp
    > array([(2002, 10.502535211267606),
    >        (2003, 10.214794520547946),
    >        (2004, 9.811578947368423),
    >        (2015, 9.093658536585366),
    >        (2016, 9.244272537935139)],
    >       dtype=[('f0', '<i4'), ('f1', '<f8')])
    > 
    > >>> np.reshape(spp, (spp.size, 1))
    > array([[(2002, 10.502535211267606)],
    >        [(2003, 10.214794520547946)],
    >        [(2004, 9.811578947368423)],
    >        [(2015, 9.093658536585366)],
    >        [(2016, 9.244272537935139)]],
    >       dtype=[('f0', '<i4'), ('f1', '<f8')])
    > ```

## convert list of tuples to structured numpy array(np.dtype)

- [python - convert list of tuples to structured numpy array - Stack Overflow](https://stackoverflow.com/questions/28176949/convert-list-of-tuples-to-structured-numpy-array)

    > A list of tuples is the correct way of providing data to a structured array:
    > 
    > ```
    > In [273]: xlist = [(1, 1.1), (2, 1.2), (3, 1.3)]
    > 
    > In [274]: dt=np.dtype('int,float')
    > 
    > In [275]: np.array(xlist,dtype=dt)
    > Out[275]:
    > array([(1, 1.1), (2, 1.2), (3, 1.3)],
    >       dtype=[('f0', '<i4'), ('f1', '<f8')])
    > 
    > In [276]: xarr = np.array(xlist,dtype=dt)
    > 
    > In [277]: xarr['f0']
    > Out[277]: array([1, 2, 3])
    > 
    > In [278]: xarr['f1']
    > Out[278]: array([ 1.1,  1.2,  1.3])
    > ```
    > 
    > or if the names are important:
    > 
    > ```
    > In [280]: xarr.dtype.names=['name1','name2']
    > 
    > In [281]: xarr
    > Out[281]:
    > array([(1, 1.1), (2, 1.2), (3, 1.3)],
    >       dtype=[('name1', '<i4'), ('name2', '<f8')])
    > ```



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

## Indexing a numpy array with a list of tuples [(idx1,score1),(idx2,score2),...,(idxN,scoreN)]

- [Indexing a numpy array with a list of tuples - Stack Overflow](https://stackoverflow.com/questions/28491230/indexing-a-numpy-array-with-a-list-of-tuples)
    > 
    > ```python
    > def assign_score_without_vectorize(topics,topicsVector):
    >     # convert list [(idx1,score1),(idx2,score2),...,(idxN,scoreN)] to [(idx1,idx2,...,idxN),(socre1,score2,...,scoreN)]
    >     idx = list(list(zip(*topics))[0])
    >     score = list(list(zip(*topics))[1])
    >     #print(idx, score)
    >     topicsVector.setflags(write=1)
    >     # direct assign score with list idx
    >     topicsVector[idx] = score
    >     #print(topicsVector)
    > ```
    > [name=Ya-Lun Li]

## use np.digitize to remap value to array

- [python - Replace values of a numpy index array with values of a list - Stack Overflow](https://stackoverflow.com/questions/13572448/replace-values-of-a-numpy-index-array-with-values-of-a-list)

    > Instead of replacing the values one by one, it is possible to remap the entire array like this:
    > 
    > ```python
    > import numpy as np
    > a = np.array([1,2,2,1]).reshape(2,2)
    > # palette must be given in sorted order
    > palette = [1, 2]
    > # key gives the new values you wish palette to be mapped to.
    > key = np.array([0, 10])
    > index = np.digitize(a.ravel(), palette, right=True)
    > print(key[index].reshape(a.shape))
    > ```
    > 
    > yields
    > 
    > ```
    > [[ 0 10]
    >  [10  0]]
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


## one-hot encode

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


## Make Read-only array writable

- [python - Replace values of a numpy index array with values of a list - Stack Overflow](https://stackoverflow.com/questions/13572448/replace-values-of-a-numpy-index-array-with-values-of-a-list)

    > Read-only array in numpy can be made writable:
    > 
    > ```
    > nArray.flags.writeable = True
    > ```
    > 
    > This will then allow assignment operations like this one:
    > 
    > ```
    > nArray[nArray == 10] = 9999 # replace all 10's with 9999's
    > ```
    > 
    > The real problem was not assignment itself but the writable flag.
    > 


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

## Vectorize

- [Speeding up your code (2): vectorizing the loops with Numpy](https://hackernoon.com/speeding-up-your-code-2-vectorizing-the-loops-with-numpy-e380e939bed3)



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

## API

- [SciPy — SciPy v1.0.0 Reference Guide](https://docs.scipy.org/doc/scipy-1.0.0/reference/)
    - [Index — SciPy v1.0.0 Reference Guide](https://docs.scipy.org/doc/scipy-1.0.0/reference/genindex.html)


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


# scikit-learn

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



# Pandas

## API 

- [API Reference — pandas 0.22.0 documentation](https://pandas.pydata.org/pandas-docs/stable/api.html?highlight=dataframe#dataframe)

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

## selecting rows

- [python - Select rows from a DataFrame based on values in a column in pandas - Stack Overflow](https://stackoverflow.com/questions/17071871/select-rows-from-a-dataframe-based-on-values-in-a-column-in-pandas)

    > To select rows whose column value equals a scalar, `some_value`, use `==`:
    > 
    > ```python
    > df.loc[df['column_name'] == some_value]
    > ```
    > 
    > To select rows whose column value is in an iterable, `some_values`, use `isin`:
    > 
    > ```python
    > df.loc[df['column_name'].isin(some_values)]
    > ```
    > 
    > Combine multiple conditions with `&`:
    > 
    > ```python
    > df.loc[(df['column_name'] == some_value) & df['other_column'].isin(some_values)]
    > ```
    > 
    > ---
    > 
    > To select rows whose column value _does not equal_ `some_value`, use `!=`:
    > 
    > ```python
    > df.loc[df['column_name'] != some_value]
    > ```
    > 
    > `isin` returns a boolean Series, so to select rows whose value is _not_ in `some_values`, negate the boolean Series using `~`:
    > 
    > ```python
    > df.loc[~df['column_name'].isin(some_values)]
    > ```
    > 
    > ---
    > 
    > For example,
    > 
    > ```python
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
    > ```python
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
    > ```python
    > print(df.loc[df['B'].isin(['one','three'])])
    > ```
    > 
    > yields
    > 
    > ```python
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
    > ```python
    > df = df.set_index(['B'])
    > print(df.loc['one'])
    > ```
    > 
    > yields
    > 
    > ```python
    >        A  C   D
    > B              
    > one  foo  0   0
    > one  bar  1   2
    > one  foo  6  12
    > ```
    > 
    > or, to include multiple values from the index use `df.index.isin`:
    > 
    > ```python
    > df.loc[df.index.isin(['one','two'])]
    > ```
    > 
    > yields
    > 
    > ```python
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

- [pandas - create a new dataframe from selecting specific rows from existing dataframe python - Stack Overflow](https://stackoverflow.com/questions/40885318/create-a-new-dataframe-from-selecting-specific-rows-from-existing-dataframe-pyth)

    > You nedd add `()` because `&` has higher precedence than `==`:
    > 
    > ```python
    > df3 = df[(df['count'] == '2') & (df['price'] == '100')]
    > print (df3)
    >   id count price
    > 0  1     2   100
    > ```
    > 
    > If need check multiple values use [`isin`](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.isin.html):
    > 
    > ```python
    > df4 = df[(df['count'].isin(['2','7'])) & (df['price'].isin(['100', '221']))]
    > print (df4)
    >   id count price
    > 0  1     2   100
    > 3  4     7   221
    > ```
    > 
    > But if check numeric, use:
    > 
    > ```python
    > df3 = df[(df['count'] == 2) & (df['price'] == 100)]
    > print (df3)
    > 
    > df4 = df[(df['count'].isin([2,7])) & (df['price'].isin([100, 221]))]
    > print (df4)
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

- [python - Append an empty row in dataframe using pandas - Stack Overflow](https://stackoverflow.com/questions/39998262/append-an-empty-row-in-dataframe-using-pandas)

    > Or `df.append(pd.DataFrame([np.nan],columns=['A']))`, where 'A' is the name of any column in the df. Pandas will automatically fill up NaN to empty columns. -- [allenyllee](https://stackoverflow.com/users/1851492/allenyllee "91 reputation") [46 secs ago](https://stackoverflow.com/questions/39998262/append-an-empty-row-in-dataframe-using-pandas#comment91799915_47956101)




### Changing some column types to categories

- [numpy - Python Pandas - Changing some column types to categories - Stack Overflow](https://stackoverflow.com/questions/28910851/python-pandas-changing-some-column-types-to-categories)

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


### Combine two columns of text

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


### copy dataframe object

- [pandas.DataFrame.copy — pandas 0.23.4 documentation](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.copy.html)

    > Notes
    > 
    > When `deep=True`, data is copied but actual Python objects will not be copied recursively, only the reference to the object. This is in contrast to *copy.deepcopy* in the Standard Library, which recursively copies object data (see examples below).
    > 
    > While `Index` objects are copied when `deep=True`, the underlying numpy array is not copied for performance reasons. Since `Index` is immutable, the underlying data can be safely shared and a copy is not needed.
    > 
    > Examples
    > ```python
    > >>> s = pd.Series([1, 2], index=["a", "b"])
    > >>> s
    > a    1
    > b    2
    > dtype: int64
    > ```
    > ```python
    > >>> s_copy = s.copy()
    > >>> s_copy
    > a    1
    > b    2
    > dtype: int64
    > ```
    > 
    > ---
    > 
    > Note that when copying an object containing Python objects, a deep copy will copy the data, but will not do so recursively. Updating a nested data object will be reflected in the deep copy.
    > ```python
    > >>> s = pd.Series([[1, 2], [3, 4]])
    > >>> deep = s.copy()
    > >>> s[0][0] = 10
    > >>> s
    > 0    [10, 2]
    > 1     [3, 4]
    > dtype: object
    > >>> deep
    > 0    [10, 2]
    > 1     [3, 4]
    > dtype: object
    > ```


### Transpose

- [python - How do I transpose dataframe in pandas without index? - Stack Overflow](https://stackoverflow.com/questions/42381639/how-do-i-transpose-dataframe-in-pandas-without-index)

    > Can you simple set the index to your first column in your dataframe first, then transpose?
    > 
    > ```
    > df.set_index('Attribute',inplace=True)
    > df.transpose()
    > ```
    > 
    > Or
    > 
    > ```
    > df.set_index('Attribute').T
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





















