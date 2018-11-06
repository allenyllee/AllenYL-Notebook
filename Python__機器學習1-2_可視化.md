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

## subplot

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

### scatter
- [matplotlib.pyplot.scatter — Matplotlib 3.0.0 documentation](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.scatter.html)

### Choosing Colormaps
- [Choosing Colormaps — Matplotlib 2.0.2 documentation](https://matplotlib.org/users/colormaps.html)



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
