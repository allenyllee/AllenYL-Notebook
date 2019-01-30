# Python__機器學習1-2_可視化

[toc]
<!-- toc --> 

# pyplot

## API

- [The Matplotlib API — Matplotlib 2.1.1 documentation](https://matplotlib.org/api/index.html)
    - [The Pyplot API — Matplotlib 2.1.1 documentation](https://matplotlib.org/api/pyplot_summary.html)
        - [Pyplot tutorial — Matplotlib 2.0.2 documentation](https://matplotlib.org/users/pyplot_tutorial.html)
        - [Tight Layout guide — Matplotlib 2.0.2 documentation](https://matplotlib.org/users/tight_layout_guide.html)
        - [A simple plot with a custom dashed line — Matplotlib 2.1.0 documentation](https://matplotlib.org/2.1.0/gallery/lines_bars_and_markers/line_demo_dash_control.html)
        - [Line-style reference — Matplotlib 2.1.2 documentation](https://matplotlib.org/gallery/lines_bars_and_markers/line_styles_reference.html?highlight=line%20style%20reference)

## imshow

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


## scatter plot with different text at each data point(annotate)

- [matplotlib scatter plot with different text at each data point - Stack Overflow](https://stackoverflow.com/questions/14432557/matplotlib-scatter-plot-with-different-text-at-each-data-point)

    > I'm not aware of any plotting method which takes arrays or lists but you could use `annotate()` while iterating over the values in `n`.
    > 
    > ```
    > y = [2.56422, 3.77284, 3.52623, 3.51468, 3.02199]
    > z = [0.15, 0.3, 0.45, 0.6, 0.75]
    > n = [58, 651, 393, 203, 123]
    > 
    > fig, ax = plt.subplots()
    > ax.scatter(z, y)
    > 
    > for i, txt in enumerate(n):
    >     ax.annotate(txt, (z[i], y[i]))
    > ```
    > 
    > There are a lot of formatting options for `annotate()`, see the [matplotlib website:](http://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.annotate)
    > 
    > ![enter image description here](https://i.stack.imgur.com/6g4Et.png)

## 3d example code

- [mplot3d example code: text3d_demo.py — Matplotlib 2.0.2 documentation](https://matplotlib.org/examples/mplot3d/text3d_demo.html)


    > ![../../_images/text3d_demo1.png](https://matplotlib.org/_images/text3d_demo1.png)
    > 
    > ```python
    > '''
    > ======================
    > Text annotations in 3D
    > ======================
    > 
    > Demonstrates the placement of text annotations on a 3D plot.
    > 
    > Functionality shown:
    > - Using the text function with three types of 'zdir' values: None,
    >   an axis name (ex. 'x'), or a direction tuple (ex. (1, 1, 0)).
    > - Using the text function with the color keyword.
    > - Using the text2D function to place text on a fixed position on the ax object.
    > '''
    > 
    > from mpl_toolkits.mplot3d import Axes3D
    > import matplotlib.pyplot as plt
    > 
    > 
    > fig = plt.figure()
    > ax = fig.gca(projection='3d')
    > 
    > # Demo 1: zdir
    > zdirs = (None, 'x', 'y', 'z', (1, 1, 0), (1, 1, 1))
    > xs = (1, 4, 4, 9, 4, 1)
    > ys = (2, 5, 8, 10, 1, 2)
    > zs = (10, 3, 8, 9, 1, 8)
    > 
    > for zdir, x, y, z in zip(zdirs, xs, ys, zs):
    >     label = '(%d, %d, %d), dir=%s' % (x, y, z, zdir)
    >     ax.text(x, y, z, label, zdir)
    > 
    > # Demo 2: color
    > ax.text(9, 0, 0, "red", color='red')
    > 
    > # Demo 3: text2D
    > # Placement 0, 0 would be the bottom left, 1, 1 would be the top right.
    > ax.text2D(0.05, 0.95, "2D Text", transform=ax.transAxes)
    > 
    > # Tweaking display region and labels
    > ax.set_xlim(0, 10)
    > ax.set_ylim(0, 10)
    > ax.set_zlim(0, 10)
    > ax.set_xlabel('X axis')
    > ax.set_ylabel('Y axis')
    > ax.set_zlabel('Z axis')
    > 
    > plt.show()
    > ```
    > 

## plot

- [matplotlib.pyplot — Matplotlib 3.0.2 documentation](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.html)


### subplot

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

### scatter
- [matplotlib.pyplot.scatter — Matplotlib 3.0.0 documentation](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.scatter.html)


### make Matplotlib scatterplots transparent as a group

- [python - How to make Matplotlib scatterplots transparent as a group? - Stack Overflow](https://stackoverflow.com/questions/30108372/how-to-make-matplotlib-scatterplots-transparent-as-a-group?rq=1)

    > Yes, interesting question. You can get this scatterplot with [Shapely](https://pypi.python.org/pypi/Shapely). Here is the code :
    > 
    > ```python
    > import matplotlib.pyplot as plt
    > import matplotlib.patches as ptc
    > import numpy as np
    > from shapely.geometry import Point
    > from shapely.ops import cascaded_union
    > 
    > n = 100
    > size = 0.02
    > alpha = 0.5
    > 
    > def points():
    >     x = np.random.uniform(size=n)
    >     y = np.random.uniform(size=n)
    >     return x, y
    > 
    > x1, y1 = points()
    > x2, y2 = points()
    > polygons1 = [Point(x1[i], y1[i]).buffer(size) for i in range(n)]
    > polygons2 = [Point(x2[i], y2[i]).buffer(size) for i in range(n)]
    > polygons1 = cascaded_union(polygons1)
    > polygons2 = cascaded_union(polygons2)
    > 
    > fig = plt.figure(figsize=(4,4))
    > ax = fig.add_subplot(111, title="Test scatter")
    > for polygon1 in polygons1:
    >     polygon1 = ptc.Polygon(np.array(polygon1.exterior), facecolor="red", lw=0, alpha=alpha)
    >     ax.add_patch(polygon1)
    > for polygon2 in polygons2:
    >     polygon2 = ptc.Polygon(np.array(polygon2.exterior), facecolor="blue", lw=0, alpha=alpha)
    >     ax.add_patch(polygon2)
    > ax.axis([-0.2, 1.2, -0.2, 1.2])
    > 
    > fig.savefig("test_scatter.png")
    > ```
    > 
    > and the result is :
    > 
    > ![Test scatter](https://i.stack.imgur.com/u9neg.png)
    > 
    > ---
    > 
    > Thanks ! Yes, the `descartes` package can be used. After the `cascaded_union`: create patches with `descartes.PolygonPatch`, use `matplotlib.collections.PathCollection` and replace `add_patch` by `add_collection`. This will do the job with fewer lines. -- [Flabetvibes](https://stackoverflow.com/users/2225883/flabetvibes "1,936 reputation") [May 7 '15 at 22:19](https://stackoverflow.com/questions/30108372/how-to-make-matplotlib-scatterplots-transparent-as-a-group?rq=1#comment48336176_30110950)
    > 


### change the size of figures ( plt.figure(figsize=()))

- [matplotlib.pyplot.figure — Matplotlib 3.0.2 documentation](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.figure.html)

- [python - How do you change the size of figures drawn with matplotlib? - Stack Overflow](https://stackoverflow.com/questions/332289/how-do-you-change-the-size-of-figures-drawn-with-matplotlib)

    > plt.subplots(figsize=(20, 10))

### bar plot

- [matplotlib.pyplot.bar — Matplotlib 3.0.2 documentation](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.bar.html)

- [Stacked Bar Graph — Matplotlib 3.0.2 documentation](https://matplotlib.org/gallery/lines_bars_and_markers/bar_stacked.html#sphx-glr-gallery-lines-bars-and-markers-bar-stacked-py)

    > ![](https://i.imgur.com/zOUI38K.jpg)
    > 
    > ```python
    > import numpy as np
    > import matplotlib.pyplot as plt
    > 
    > 
    > N = 5
    > menMeans = (20, 35, 30, 35, 27)
    > womenMeans = (25, 32, 34, 20, 25)
    > menStd = (2, 3, 4, 1, 2)
    > womenStd = (3, 5, 2, 3, 3)
    > ind = np.arange(N)    # the x locations for the groups
    > width = 0.35       # the width of the bars: can also be len(x) sequence
    > 
    > p1 = plt.bar(ind, menMeans, width, yerr=menStd)
    > p2 = plt.bar(ind, womenMeans, width,
    >              bottom=menMeans, yerr=womenStd)
    > 
    > plt.ylabel('Scores')
    > plt.title('Scores by group and gender')
    > plt.xticks(ind, ('G1', 'G2', 'G3', 'G4', 'G5'))
    > plt.yticks(np.arange(0, 81, 10))
    > plt.legend((p1[0], p2[0]), ('Men', 'Women'))
    > 
    > plt.show()
    > ```


- [System Monitor — Matplotlib 3.0.2 documentation](https://matplotlib.org/gallery/specialty_plots/system_monitor.html#sphx-glr-gallery-specialty-plots-system-monitor-py)

    > ![](https://i.imgur.com/dY9yFip.jpg)
    > 
    > ```python
    > import time
    > import matplotlib.pyplot as plt
    > import numpy as np
    > 
    > 
    > def get_memory(t):
    >     "Simulate a function that returns system memory"
    >     return 100 * (0.5 + 0.5 * np.sin(0.5 * np.pi * t))
    > 
    > 
    > def get_cpu(t):
    >     "Simulate a function that returns cpu usage"
    >     return 100 * (0.5 + 0.5 * np.sin(0.2 * np.pi * (t - 0.25)))
    > 
    > 
    > def get_net(t):
    >     "Simulate a function that returns network bandwidth"
    >     return 100 * (0.5 + 0.5 * np.sin(0.7 * np.pi * (t - 0.1)))
    > 
    > 
    > def get_stats(t):
    >     return get_memory(t), get_cpu(t), get_net(t)
    > 
    > fig, ax = plt.subplots()
    > ind = np.arange(1, 4)
    > 
    > # show the figure, but do not block
    > plt.show(block=False)
    > 
    > 
    > pm, pc, pn = plt.bar(ind, get_stats(0))
    > pm.set_facecolor('r')
    > pc.set_facecolor('g')
    > pn.set_facecolor('b')
    > ax.set_xticks(ind)
    > ax.set_xticklabels(['Memory', 'CPU', 'Bandwidth'])
    > ax.set_ylim([0, 100])
    > ax.set_ylabel('Percent usage')
    > ax.set_title('System Monitor')
    > 
    > start = time.time()
    > for i in range(200):  # run for a little while
    >     m, c, n = get_stats(i / 10.0)
    > 
    >     # update the animated artists
    >     pm.set_height(m)
    >     pc.set_height(c)
    >     pn.set_height(n)
    > 
    >     # ask the canvas to re-draw itself the next time it
    >     # has a chance.
    >     # For most of the GUI backends this adds an event to the queue
    >     # of the GUI frameworks event loop.
    >     fig.canvas.draw_idle()
    >     try:
    >         # make sure that the GUI framework has a chance to run its event loop
    >         # and clear any GUI events.  This needs to be in a try/except block
    >         # because the default implementation of this method is to raise
    >         # NotImplementedError
    >         fig.canvas.flush_events()
    >     except NotImplementedError:
    >         pass
    > 
    > stop = time.time()
    > print("{fps:.1f} frames per second".format(fps=200 / (stop - start)))
    > ```


### gridspec

- [matplotlib.gridspec.GridSpec — Matplotlib 3.0.2 documentation](https://matplotlib.org/api/_as_gen/matplotlib.gridspec.GridSpec.html#matplotlib.gridspec.GridSpec)

- [python - Matplotlib different size subplots - Stack Overflow](https://stackoverflow.com/questions/10388462/matplotlib-different-size-subplots)

    > You can use [`gridspec`](http://matplotlib.org/users/gridspec.html) and `figure`:
    > 
    > ```python
    > import numpy as np
    > import matplotlib.pyplot as plt
    > from matplotlib import gridspec
    > 
    > # generate some data
    > x = np.arange(0, 10, 0.2)
    > y = np.sin(x)
    > 
    > # plot it
    > fig = plt.figure(figsize=(8, 6))
    > gs = gridspec.GridSpec(1, 2, width_ratios=[3, 1])
    > ax0 = plt.subplot(gs[0])
    > ax0.plot(x, y)
    > ax1 = plt.subplot(gs[1])
    > ax1.plot(y, x)
    > 
    > plt.tight_layout()
    > plt.savefig('grid_figure.pdf')
    > ```
    > 
    > ![resulting plot](https://i.stack.imgur.com/AAnMK.png)
    > 

### interactive figure

- [Clear MatPlotLib figure in Jupyter Python notebook - Stack Overflow](https://stackoverflow.com/questions/42998009/clear-matplotlib-figure-in-jupyter-python-notebook)

    > What you call overhead is the source of the problem. Or in other words: If in each call to the function, a new figure is created, is it surprising that you will end up with a lot of figures?
    > 
    > The idea is of course to draw a single figure. In order to be able to later update the figure the `%matplotlib notebook` backend is needed.
    > 
    > The function that gets called when changing the slider will then only need to update the viewing angle and redraw the canvas.
    > 
    > ```python
    > import numpy as np
    > import matplotlib.pyplot as plt
    > from mpl_toolkits.mplot3d import Axes3D
    > import ipywidgets as widgets
    > from IPython.display import display
    > %matplotlib notebook
    > 
    > # generate test data
    > x = np.random.rand(100)
    > y = np.random.rand(100)
    > z = np.random.rand(100)
    > 
    > fig = plt.figure(figsize=(6,6))
    > ax = fig.add_subplot(111, projection='3d')
    > ax.set_xlabel('X axis')
    > ax.set_ylabel('Y axis')
    > ax.set_zlabel('Z axis')
    > ax.scatter(x, y, z)
    > ax.view_init(20, 40)
    > # show plot
    > plt.show()
    > 
    > def update_plot(angle1 = 20, angle2 = 40):
    >     # set view angle
    >     ax.view_init(angle1, angle2)
    >     fig.canvas.draw_idle()
    > 
    > # prepare widgets
    > angle1_slider = widgets.IntSlider(20, min = 0, max = 60)
    > angle1_label = widgets.Label(value = 'Angle 1 value is: ' + str(angle1_slider.value))
    > display(angle1_slider, angle1_label)
    > 
    > # handle angle 1 update
    > def update_angle1(value):
    >     update_plot(angle1 = value['new'])
    >     angle1_label.value = 'Angle 1 value is: ' + str(value.new)
    > 
    > angle1_slider.observe(update_angle1, names = 'value')
    > ```
    > 
    > This is how it would look like:
    > 
    > [![enter image description here](https://i.stack.imgur.com/sECXb.png)](https://i.stack.imgur.com/sECXb.png)
    > 
    > 
    > ---
    > 
    > Excellent! I did not know `fig.canvas.draw_idle()` which solved the issue indeed. And even better, I always used `%matplotlib inline` but `%matplotlib notebook` is very useful too! Thanks! -- [Pieter](https://stackoverflow.com/users/1411378/pieter "946 reputation") [Mar 24 '17 at 20:56](https://stackoverflow.com/questions/42998009/clear-matplotlib-figure-in-jupyter-python-notebook#comment73107552_43003316)
    > 

## color

### Choosing Colormaps
- [Choosing Colormaps — Matplotlib 2.0.2 documentation](https://matplotlib.org/users/colormaps.html)


### transparent marker

- [python - Plotting with a transparent marker but non-transparent edge - Stack Overflow](https://stackoverflow.com/questions/23596575/plotting-with-a-transparent-marker-but-non-transparent-edge)

    > This is tricky in Matplotlib... you have to use a string `"None"` instead of the value `None`, then you can just do:
    > 
    > ```
    > plt.plot(x,y2, 'o', ms=14, markerfacecolor="None",
    >          markeredgecolor='red', markeredgewidth=5)
    > ```
    > 
    > ---
    > 
    > As a side note, there is a very good reason for the difference between `None` and `'None'`. The first means 'do the default thing', the later means "I don't want a color". -- [tacaswell](https://stackoverflow.com/users/380231/tacaswell "54,140 reputation") [May 12 '14 at 13:34](https://stackoverflow.com/questions/23596575/plotting-with-a-transparent-marker-but-non-transparent-edge#comment36245323_23596637)
    > 

### select colors in colormap 

- [python - Matplotlib change colormap tab20 to have three colors - Stack Overflow](https://stackoverflow.com/questions/43938425/matplotlib-change-colormap-tab20-to-have-three-colors)

    > ```python
    > skip = []
    > for i in range(0,len(cm.colors)//4+1):
    >     skip.append(4*i)
    > # the colormap is called Vega in my Matplotlib version
    > cm = plt.cm.get_cmap('Vega20c')
    > cm_skip = [cm.colors[i] for i in range(len(cm.colors)) if i not in skip]
    > 
    > for i, c in enumerate(cm_skip):
    >     x = np.linspace(0,1)
    >     y = (i+1)*x + i
    >     plt.plot(x, y, color=c, linewidth=4)[![enter image description here][2]]
    > ```


### get continuous colors from colormap

- [python - Matplotlib Plot Lines with Colors Through Colormap - Stack Overflow](https://stackoverflow.com/questions/38208700/matplotlib-plot-lines-with-colors-through-colormap)

    > The Matplotlib colormaps accept an argument (`0..1`, scalar or array) which you use to get colors from a colormap. For example:
    > 
    > ```
    > col = pl.cm.jet([0.25,0.75])
    > ```
    > 
    > Gives you an array with (two) RGBA colors:
    > 
    > > array([[ 0. , 0.50392157, 1. , 1. ], [ 1. , 0.58169935, 0. , 1. ]])
    > 
    > You can use that to create `N` different colors:
    > 
    > ```
    > import numpy as np
    > import matplotlib.pylab as pl
    > 
    > x = np.linspace(0, 2*np.pi, 64)
    > y = np.cos(x)
    > 
    > pl.figure()
    > pl.plot(x,y)
    > 
    > n = 20
    > colors = pl.cm.jet(np.linspace(0,1,n))
    > 
    > for i in range(n):
    >     pl.plot(x, i*y, color=colors[i])
    > ```
    > 
    > [![enter image description here](https://i.stack.imgur.com/pWHiD.png)](https://i.stack.imgur.com/pWHiD.png)
    > 
    > 
    > ---
    > 
    > An anternative to Bart's answer, in which you do not specify the color in each call to `plt.plot` is to define a new color cycle with `set_prop_cycle`. His example can be translated into the following code (I've also changed the import of matplotlib to the recommended style):
    > 
    > ```
    > import numpy as np
    > import matplotlib.pyplot as plt
    > 
    > x = np.linspace(0, 2*np.pi, 64)
    > y = np.cos(x)
    > 
    > n = 20
    > ax = plt.axes()
    > ax.set_prop_cycle('color',[plt.cm.jet(i) for i in np.linspace(0, 1, n)])
    > 
    > for i in range(n):
    >     plt.plot(x, i*y)
    > ```
    > 


### generate colormap

- [python - matplotlib generic colormap from tab10 - Stack Overflow](https://stackoverflow.com/questions/47222585/matplotlib-generic-colormap-from-tab10)

    > You may use the HSV system to obtain differently saturated and luminated colors for the same hue. Suppose you have at most 10 categories, then the `tab10` map can be used to get a certain number of base colors. From those you can choose a couple of lighter shades for the subcategories.
    > 
    > The following would be a function `categorical_cmap`, which takes as input the number of categories (`nc`) and the number of subcategories (`nsc`) and returns a colormap with `nc*nsc` different colors, where for each category there are `nsc` colors of same hue.
    > 
    > ```python
    > import numpy as np
    > import matplotlib.pyplot as plt
    > import matplotlib.colors
    > 
    > def categorical_cmap(nc, nsc, cmap="tab10", continuous=False):
    >     if nc > plt.get_cmap(cmap).N:
    >         raise ValueError("Too many categories for colormap.")
    >     if continuous:
    >         ccolors = plt.get_cmap(cmap)(np.linspace(0,1,nc))
    >     else:
    >         ccolors = plt.get_cmap(cmap)(np.arange(nc, dtype=int))
    >     cols = np.zeros((nc*nsc, 3))
    >     for i, c in enumerate(ccolors):
    >         chsv = matplotlib.colors.rgb_to_hsv(c[:3])
    >         arhsv = np.tile(chsv,nsc).reshape(nsc,3)
    >         arhsv[:,1] = np.linspace(chsv[1],0.25,nsc)
    >         arhsv[:,2] = np.linspace(chsv[2],1,nsc)
    >         rgb = matplotlib.colors.hsv_to_rgb(arhsv)
    >         cols[i*nsc:(i+1)*nsc,:] = rgb
    >     cmap = matplotlib.colors.ListedColormap(cols)
    >     return cmap
    > 
    > c1 = categorical_cmap(4, 3, cmap="tab10")
    > plt.scatter(np.arange(4*3),np.ones(4*3)+1, c=np.arange(4*3), s=180, cmap=c1)
    > 
    > c2 = categorical_cmap(2, 5, cmap="tab10")
    > plt.scatter(np.arange(10),np.ones(10), c=np.arange(10), s=180, cmap=c2)
    > 
    > c3 = categorical_cmap(5, 4, cmap="tab10")
    > plt.scatter(np.arange(20),np.ones(20)-1, c=np.arange(20), s=180, cmap=c3)
    > 
    > plt.margins(y=0.3)
    > plt.xticks([])
    > plt.yticks([0,1,2],["(5, 4)", "(2, 5)", "(4, 3)"])
    > plt.show()
    > ```
    > 
    > [![enter image description here](https://i.stack.imgur.com/JNiAo.png)](https://i.stack.imgur.com/JNiAo.png)
    > 




# seaborn

## Building color palettes

- [Choosing color palettes — seaborn 0.9.0 documentation](https://seaborn.pydata.org/tutorial/color_palettes.html)

    > Seaborn makes it easy to select and use color palettes that are suited to the kind of data you are working with and the goals you have in visualizing it.
    > 
    > ```python
    > import numpy as np
    > import seaborn as sns
    > import matplotlib.pyplot as plt
    > sns.set()
    > ```
    > ---
    > 
    > When importing seaborn, the default color cycle is changed to a set of six colors that evoke the standard matplotlib color cycle while aiming to be a bit more pleasing to look at.
    > 
    > ```python
    > current_palette = sns.color_palette()
    > sns.palplot(current_palette)
    > ```
    > ![../_images/color_palettes_6_0.png](https://seaborn.pydata.org/_images/color_palettes_6_0.png)
    > 
    > There are six variations of the default theme, called `deep`, `muted`, `pastel`, `bright`, `dark`, and `colorblind`.
    > 
    > ![../_images/color_palettes_8_0.png](https://seaborn.pydata.org/_images/color_palettes_8_0.png)
    > 
    > ---
    > 
    > The most common way to do this uses the `hls` color space, which is a simple transformation of RGB values.
    > 
    > ```python
    > sns.palplot(sns.color_palette("hls", 8))
    > ```
    > 
    > ![../_images/color_palettes_10_0.png](https://seaborn.pydata.org/_images/color_palettes_10_0.png)
    > 
    > There is also the [`hls_palette()`](https://seaborn.pydata.org/generated/seaborn.hls_palette.html#seaborn.hls_palette "seaborn.hls_palette") function that lets you control the lightness and saturation of the colors.
    > 
    > ```python
    > sns.palplot(sns.hls_palette(8, l=.3, s=.8))
    > ```
    > 
    > ![../_images/color_palettes_12_0.png](https://seaborn.pydata.org/_images/color_palettes_12_0.png)
    > 

# Graphviz

- [Download](https://graphviz.gitlab.io/download/)

## API

- [API Reference — graphviz 0.8.2 documentation](https://graphviz.readthedocs.io/en/stable/api.html)
    - [User Guide — graphviz 0.8.2 documentation](https://graphviz.readthedocs.io/en/stable/manual.html)

## install

- [python - "RuntimeError: Make sure the Graphviz executables are on your system's path" after installing Graphviz 2.38 - Stack Overflow](https://stackoverflow.com/questions/35064304/runtimeerror-make-sure-the-graphviz-executables-are-on-your-systems-path-aft)

    > You should install the graphviz package in your system (not just the python package). On **Ubuntu** you should try:
    > 
    > ```
    > sudo apt-get install graphviz
    > ```

- [python安装Graphviz及其应用 - jinruoyanxu的博客 - CSDN博客](https://blog.csdn.net/jinruoyanxu/article/details/79762085)

    > 输入dot -version，然后按回车，如果显示graphviz的相关版本信息，则安装配置成功。


# visdom

- [facebookresearch/visdom: A flexible tool for creating, organizing, and sharing visualizations of live, rich data. Supports Torch and Numpy.](https://github.com/facebookresearch/visdom)

- [gensim/Training_visualizations.ipynb at develop · RaRe-Technologies/gensim](https://github.com/RaRe-Technologies/gensim/blob/develop/docs/notebooks/Training_visualizations.ipynb)

    > Setup Visdom 
    > ============
    > 
    > Install it with:
    > 
    > `pip install visdom`
    > 
    > Start the server:
    > 
    > `python -m visdom.server`
    > 
    > Visdom now can be accessed at <http://localhost:8097> in the browser.
    > 

## Visdom 动态图 示例

- [Visdom 动态图 示例 (pytorch) - 知乎](https://zhuanlan.zhihu.com/p/32815374)

    > 之前介绍了visdom 的一些基本的用法, 这里放几个 动态图的示例教程
    > 
    > 首先要搞明白, Visdom 里, 有 windows(win), Name(name)
    > 
    > 他们的关系是, 一个win里面可以有多个name. 也就是说一个win里面可以有几个不同的曲线实例. 每个实例都是由一个name来控制的
    > 
    > 首先是开启visdom后检查服务器的连接并清空窗口,
    > 
    > ```
    > from __future__ import absolute_import
    > from __future__ import division
    > from __future__ import print_function
    > from __future__ import unicode_literals
    > 
    > from visdom import Visdom
    > import numpy as np
    > import math
    > import os.path
    > import getpass
    > from sys import platform as _platform
    > from six.moves import urllib
    > import numpy as np
    > viz = Visdom()
    > 
    > assert viz.check_connection()
    > viz.close()
    > 
    > ```
    > 
    > 这里首先是一个窗口多条曲线
    > 
    > ```
    > ##首先是建立一个win, 下面建立了一个曲线的win
    > win=viz.line(
    >     X=np.array([0,1]),
    >     Y=np.array([0,1]),
    >     opts=dict(
    >         xtickmin=-2,
    >         xtickmax=2,
    >         xtickstep=1,
    >         ytickmin=-1,
    >         ytickmax=5,
    >         ytickstep=1,
    >         markersymbol='dot',
    >         markersize=5,
    >     ),
    >     name="1"
    > )
    > 
    > ## 添加新的line到之前的win中去. 这里要注意参数win, update,name
    > viz.line(
    >     X=np.array([0,1]),
    >     Y=np.array([1,2]),
    >     opts=dict(markercolor=np.array([50]),
    >              markersymbol='dot',),
    >     ##选择之前的窗口win
    >     win=win,
    >     ##选择更新图像的方式,另外有"append"/"new"
    >     update="new",
    >     ## 对当前的line新命名, 这个必须要
    >     name="2",
    > )
    > 
    > ```
    > 
    > 效果如下所示
    > 
    > ![](https://pic4.zhimg.com/80/v2-be1921742ee2100fbdb6142ec2092412_hd.jpg)
    > 
    > 在这之后我们就可以用updateTrace这个函数对两条线进行更新了, 注意的是updateTrace目前只支持line和scatter
    > 
    > ![](https://pic2.zhimg.com/80/v2-58486cb6dc08807c06bbfd55fc310335_hd.jpg)
    > 
    > 在这里每条line 的控制都需要指明win和name,这样就可以把数据update到win上了. 不同的name 可以控制同一个win下的不同的line
    > 
    > ```
    > import time
    > for a in range(10):
    >     viz.updateTrace(
    >         X=np.array([a]),
    >         Y=np.array([a]),
    >         win=win,
    >         name="1"
    >     )
    > 
    >     viz.updateTrace(
    >         X=np.array([a]),
    >         Y=np.array([a+1]),
    >         win=win,
    >         name="2"
    >     )
    >     time.sleep(1)
    > 
    > ```
    > 
    > ![](https://pic3.zhimg.com/v2-988823af1f9041c3deb98ec15475389d_b.jpg)


# plotly

## location and length of color scale in heatmap

- [javascript - plotly js: location and length of color scale in heatmap - Stack Overflow](https://stackoverflow.com/questions/41081474/plotly-js-location-and-length-of-color-scale-in-heatmap)

    > You can set the [position](https://plot.ly/javascript/reference/#heatmap-colorbar-x) and [length](https://plot.ly/javascript/reference/#heatmap-colorbar-len) of the `colorbar` by adding the following line to your `data`:
    > 
    > ```
    > colorbar: {x: -.5, len: 0.5}
    > ```
    > 
    > * * * * *
    > 
    > Below is a snippet with a colorbar pushed to the left and half the regular size.
    > 
    > ```
    > Plotly.d3.json('https://raw.githubusercontent.com/plotly/datasets/master/custom_heatmap_colorscale.json', function(figure) {
    > var data = [{
    >     z: figure.z,
    >     colorscale: 'Jet',
    >     type: 'heatmap',
    >     colorbar: {x: -.5, len: 0.5}
    >   }
    > ];
    > var layout = {title: 'Jet'};
    > Plotly.newPlot('myDiv', data, layout);
    > });
    > ```
    > 

## Subplots

- [Python Subplots | Examples | Plotly](https://plot.ly/python/subplots/)

    > Multiple Subplots with Titles
    > 
    > ```
    > from plotly import tools
    > import plotly.plotly as py
    > import plotly.graph_objs as go
    > 
    > trace1 = go.Scatter(x=[1, 2, 3], y=[4, 5, 6])
    > trace2 = go.Scatter(x=[20, 30, 40], y=[50, 60, 70])
    > trace3 = go.Scatter(x=[300, 400, 500], y=[600, 700, 800])
    > trace4 = go.Scatter(x=[4000, 5000, 6000], y=[7000, 8000, 9000])
    > 
    > fig = tools.make_subplots(rows=2, cols=2, subplot_titles=('Plot 1', 'Plot 2',
    >                                                           'Plot 3', 'Plot 4'))
    > 
    > fig.append_trace(trace1, 1, 1)
    > fig.append_trace(trace2, 1, 2)
    > fig.append_trace(trace3, 2, 1)
    > fig.append_trace(trace4, 2, 2)
    > 
    > fig['layout'].update(height=600, width=600, title='Multiple Subplots' +
    >                                                   ' with Titles')
    > 
    > py.iplot(fig, filename='make-subplots-multiple-with-titles')
    > ```
    > 
    > Custom Sized Subplot with Subplot Titles
    > ```
    > from plotly import tools
    > import plotly.plotly as py
    > import plotly.graph_objs as go
    > 
    > trace0 = go.Scatter(
    >     x=[1, 2],
    >     y=[1, 2]
    > )
    > trace1 = go.Scatter(
    >     x=[1, 2],
    >     y=[1, 2]
    > )
    > trace2 = go.Scatter(
    >     x=[1, 2, 3],
    >     y=[2, 1, 2]
    > )
    > fig = tools.make_subplots(rows=2, cols=2, specs=[[{}, {}], [{'colspan': 2}, None]],
    >                           subplot_titles=('First Subplot','Second Subplot', 'Third Subplot'))
    > 
    > fig.append_trace(trace0, 1, 1)
    > fig.append_trace(trace1, 1, 2)
    > fig.append_trace(trace2, 2, 1)
    > 
    > fig['layout'].update(showlegend=False, title='Specs with Subplot Title')
    > py.iplot(fig, filename='custom-sized-subplot-with-subplot-titles')
    > 
    > ```
    > 

## Invalid value of type 'builtins.str'

- [python - Plotly Value error - Invalid property for colour - Stack Overflow](https://stackoverflow.com/questions/51691172/plotly-value-error-invalid-property-for-colour)

    > The error thrown for that lines is.
    > 
    > ```
    > ValueError:
    > Invalid value of type 'builtins.str' received for the 'bgcolor' property of
    > layout.legend
    > ```

    > After further looking into the issue, the problem is with the cufflinks internal files. Cufflinks is having compatibility issues with the plotly latest version, which is dicussed in this [`Github Issue`](https://github.com/santosjorge/cufflinks/issues/119), You could try either downgrading to `plotly 2.7' using the below commands. So that these errors can be eliminated.
    > 
    > ```
    > pip uninstall plotly
    > pip install plotly==2.7.0
    > ```
    > 

## Get and Replot a Public Figure with URL

- [Python Get Requests | Examples | Plotly](https://plot.ly/python/get-requests/)

    > Get and Replot a Public Figure with URL
    > 
    > ```
    > import plotly.plotly as py
    > # Learn about API authentication here: https://plot.ly/python/getting-started
    > # Find your api_key here: https://plot.ly/settings/api
    > 
    > fig = py.get_figure("https://plot.ly/~PlotBot/5")
    > 
    > plot_url = py.plot(fig, filename="python-replot1")
    > ```

## EDA and interactive figures with Plotly

- [EDA and interactive figures with Plotly | Cambridge Coding Academy](https://cambridgecoding.wordpress.com/2016/02/07/eda-and-interactive-figures-with-plotly/)




# pyLDAvis

- [bmabey/pyLDAvis: Python library for interactive topic model visualization. Port of the R LDAvis package.](https://github.com/bmabey/pyLDAvis)

    > Python library for interactive topic model visualization. This is a port of the fabulous [R package](https://github.com/cpsievert/LDAvis) by [Carson Sievert](https://cpsievert.me/) and [Kenny Shirley](http://www.kennyshirley.com/).
    > 
    > [![LDAvis icon](https://camo.githubusercontent.com/9322054a979e54f1dc0bf670a853b06db766be9e/687474703a2f2f7777772e6b656e6e79736869726c65792e636f6d2f666967757265732f6c64617669732d7069632e706e67)](https://camo.githubusercontent.com/9322054a979e54f1dc0bf670a853b06db766be9e/687474703a2f2f7777772e6b656e6e79736869726c65792e636f6d2f666967757265732f6c64617669732d7069632e706e67)
    > 
    > **pyLDAvis** is designed to help users interpret the topics in a topic model that has been fit to a corpus of text data. The package extracts information from a fitted LDA topic model to inform an interactive web-based visualization.
    > 
    > The visualization is intended to be used within an IPython notebook but can also be saved to a stand-alone HTML file for easy sharing.