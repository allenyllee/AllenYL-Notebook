# Python__筆記3_Packages

[toc]
<!-- toc --> 


# Packages


## Unofficial Windows Binaries for Python Extension Packages
- [Python Extension Packages for Windows - Christoph Gohlke](https://www.lfd.uci.edu/~gohlke/pythonlibs/)


## How to package a python application to make it pip-installable

- [How to package a python application to make it pip-installable](https://marthall.github.io/blog/how-to-package-a-python-app/)

    > How to package a python application to make it pip-installable
    > ==============================================================
    > 
    > Python scripts are usable for a lot of stuff, i.e. fetching tha latest posts from /r/python or counting the total number of lines in your project folder. However, remembering where a script is placed and having to type `python dest/to/script/myscript.py` every time can be a lot of pain. Of course, you can make an alias so you only have to type `myscript` to run it, but it would be much nicer to make the script available from any computer, any place, and in addition possibly helping others with the same problem.
    > 
    > It only takes three simple steps to make you python app pip-installable.
    > 
    > 1.  Write your script or application
    > 2.  Add a setup script
    > 3.  Upload to [PyPI](https://pypi.python.org)
    > 
    > After this, you and anyone else can install it by typing:
    > 
    > ```sh
    > pip install my_awesome_script
    > 
    > ```
    > 
    > Write your script
    > -----------------
    > 
    > The script can really simple or big and advanced. We'll cover the most basic example
    > 
    > ```sh
    > 1 #!/usr/bin/env python
    > 2 print "Hello World"
    > 
    > ```
    > 
    > You can name the script anything, but this name will be the name you'll be typing every time, so make sure it's not to difficult. We'll name our script `helloworld`.
    > 
    > Add a setup script
    > ------------------
    > 
    > The `setup.py` file is is the centre of building, distributing and installing modules using the Distutils.
    > 
    > ```sh
    > 1 from setuptools import setup
    > 2
    > 3 setup(
    > 4     name='my-awesome-helloworld-script',    # This is the name of your PyPI-package.
    > 5     version='0.1',                          # Update the version number for new releases
    > 6     scripts=['helloworld']                  # The name of your scipt, and also the command you'll be using for calling it
    > 7 )
    > 
    > ```
    > 
    > **Optional**: We can now package the script using `python setup.py sdist`. This will create a `dist` folder containing all your distributions. After unpacking the distribution file, you can simply install it using `sudo python setup.py install`.
    > 
    > Upload to PyPI
    > --------------
    > 
    > First, you need to register the package on PyPi. This is simply done by typing `python setup.py register`. If you haven't registered a package from this computer before, you'll be prompted with this message:
    > 
    > ```sh
    > $ python setup.py register
    > running register
    > We need to know who you are, so please choose either:
    > 1. use your existing login,
    > 2. register as a new user,
    > 3. have the server generate a new password for you (and email it to you), or
    > 4. quit
    > Your selection [default 1]:
    > ...
    > 
    > ```
    > 
    > Once this is done, register will ask you if you want to save your login information in the `.pypirc` file. By default, this will store the login name and the password. The next step is to upload your package. Just type `python setup.py sdist upload`, and the package is now available on PyPI! You can save a few keystrokes by doing it all in one command: `python setup.py register sdist upload`.
    > 
    > Install using pip
    > -----------------
    > 
    > Finally, you can now install you package with `pip install my-awesome-helloworld-script`. You probably want to `sudo` that line. You can now run the script with:
    > 
    > ```sh
    > $ helloworld
    > Hello world!
    > 
    > ```
    > 
    > What's next?
    > ------------
    > 
    > All code from this guide can be found [here](https://gist.github.com/marthall/8122805). For more advanced programs and packages, I recommend [this guide](http://www.scotttorborg.com/python-packaging/) by Scott Torborg.


## pip install from git repo branch

- [python - pip install from git repo branch - Stack Overflow](https://stackoverflow.com/questions/20101834/pip-install-from-git-repo-branch)

    > Prepend the url prefix `git+` (See [VCS Support](https://pip.pypa.io/en/stable/reference/pip_install/#vcs-support)):
    > 
    > ```
    > pip install git+https://github.com/tangentlabs/django-oscar-paypal.git@issue/34/oscar-0.6
    > ```
    > 
    > And specify the branch name without the leading `/`.
    > 
    > ---
    > 
    > Using pip with git+ to clone a repository can be extremely slow (test with <https://github.com/django/django@stable/1.6.x> for example, it will take a few minutes). The fastest thing I've found, which works with GitHub and BitBucket, is:
    > 
    > ```
    > pip install https://github.com/user/repository/archive/branch.zip
    > ```
    > 
    > which becomes for django master:
    > 
    > ```
    > pip install https://github.com/django/django/archive/master.zip
    > ```
    > 
    > for django stable/1.7.x:
    > 
    > ```
    > pip install https://github.com/django/django/archive/stable/1.7.x.zip
    > ```
    > 
    > With BitBucket it's about the same predictable pattern:
    > 
    > ```
    > pip install https://bitbucket.org/izi/django-admin-tools/get/default.zip
    > ```
    > 
    > Here, the master branch is generally named default. This will make your requirements.txt installing much faster.
    > 
    > Some other answers mention variations required when placing the package to be installed into your `requirements.txt`. Note that with this archive syntax, the leading `-e` and trailing `#egg=blah-blah` are *not* required, and you can just simply paste the URL, so your requirements.txt looks like:
    > 
    > ```
    > https://github.com/user/repository/archive/branch.zip
    > ```
    > 
    > ---
    > 
    > **Note:** from Django 1.9 on, Django ships with a file that has a [unicode filename](https://github.com/django/django/commit/bd059e3f8c6311dcaf8afe5e29ef373f7f84cf26). The zip extractor used by pip chokes on that. An easy workaround is to replace `.zip` with `.tar.gz`, as the tar extractor works. -- [spectras](https://stackoverflow.com/users/3212865/spectras "6,888 reputation") [Jul 3 '16 at 11:56](https://stackoverflow.com/questions/20101834/pip-install-from-git-repo-branch#comment63766323_24811490)
    > 
    > ---
    > 
    > This also works for commit hashes! `pip install https://github.com/django/django/archive/ebaa08b.zip` -- [Fush](https://stackoverflow.com/users/648176/fush "1,110 reputation") [Apr 12 '17 at 3:31](https://stackoverflow.com/questions/20101834/pip-install-from-git-repo-branch#comment73781929_24811490)




## find the location of pip install packages

- [installation - How do I find the location of my Python site-packages directory? - Stack Overflow](https://stackoverflow.com/questions/122327/how-do-i-find-the-location-of-my-python-site-packages-directory)

    > There are two types of site-packages directories, *global* and *per user*.
    > 
    > 1.  **Global** site-packages ("[dist-packages](https://stackoverflow.com/questions/9387928/whats-the-difference-between-dist-packages-and-site-packages)") directories are listed in `sys.path` when you run:
    > 
    >     ```python
    >     python -m site
    >     ```
    > 
    >     For a more concise list run `getsitepackages` from the [site module](https://docs.python.org/3.5/library/site.html#site.getsitepackages) in Python code:
    > 
    >     ```python
    >     python -c "import site; print(site.getsitepackages())"
    >     ```
    > 
    >     *Note:* With virtualenvs [getsitepackages is not available](https://github.com/pypa/virtualenv/issues/228), `sys.path` from above will list the virtualenv's site-packages directory correctly, though.
    > 
    > 2.  The **per user** site-packages directory ([PEP 370](https://www.python.org/dev/peps/pep-0370/)) is where Python installs your local packages:
    > 
    >     ```python
    >     python -m site --user-site
    >     ```
    > 
    >     If this points to a non-existing directory check the exit status of Python and see `python -m site --help` for explanations.
    > 
    >     *Hint:* Running `pip list --user` or `pip freeze --user` gives you a list of all installed *per user* site-packages.
    >     
    > ---
    > 
    > Let's say you have installed the package 'django'. import it and type in dir(django). It will show you, all the functions and attributes with that module. Type in the python interpreter -
    > 
    > ```python
    > >>> import django
    > >>> dir(django)
    > ['VERSION', '__builtins__', '__doc__', '__file__', '__name__', '__package__', '__path__', 'get_version']
    > >>> print django.__path__
    > ['/Library/Python/2.6/site-packages/django']
    > ```



## Pexpect

- [Pexpect version 4.5 — Pexpect 4.5 documentation](https://pexpect.readthedocs.io/en/stable/)

## 靜態型別檢查

### Pyre

- [Facebook 推出了 Python 靜態型別檢查工具 – Pyre | Soft & Share](https://softnshare.com/2018/05/14/facebookpyretool/)

    > 由於 [Python](https://softnshare.com/tag/pythonlang/) 並不是一個編譯式程式語言，這也代表你要發現程式中的型別錯誤問題只能透過幾種方式來檢查這種因為型別使用不當所產生的 runtime 錯誤問題
    > 
    > -   撰寫 unit test
    > -   code review
    > -   靜態型別檢查工具
    > 
    > Facebook 推出的 Pyre 就是靜態型別檢查工具，**可以得知 Facebook 內部也大量在使用 Python 程式語言開發專案，也遇到這種惱人的型別檢查問題**
    > 
    > Facebook 釋出這麼棒的開源工具，當然要馬上安裝來使用看看，但是在使用上卻遇到問題，Pyre 並沒有像官方網站的展示影片一樣回傳 python 程式碼中的型別錯誤訊息，花了一些時間仔細看了文件，找到了問題發生原因，以下是我的整理筆記，希望大家都可以順利使用這個自動化工具，讓自己的生產力與專案品質大增
    > 
    > 安裝 Pyre 
    > --------
    > 
    > 安裝 Pyre 很簡單使用 pip 套件管理工具安裝就可以了
    > 
    > ```shell
    > pip install pyre-check
    > ```
    > 
    > 使用 Pyre
    > -------
    > 
    > 先建立一個測試目錄 testpy，到這個目錄寫一個回傳錯誤型別的 python 程式
    > 
    > ```python
    > def foo() -> int
    >     return 'string' # 應該要回傳 int 型別才對
    > ```
    > 
    > 進入 testpy 目錄，執行 pyre check
    > 
    > ![pyrecheck.jpg](https://i1.wp.com/softnshare.com/wp-content/uploads/2018/05/pyrecheck.jpg?resize=770%2C78&ssl=1)
    > 
    > 這時候 pyre 就會幫你檢查目錄中的所有 python 程式碼，並告訴你那些程式碼有型別使用錯誤的狀況
    > 
    > 要注意的是 pyre check 會全部將你的 source code 做一次檢查，在每日的專案開發上，一個目錄中有上百個 python 程式碼檔案時，這會很沒效率，**還好 pyre 有支援 incremental mode**
    > 
    > Pyre 的 **incremental mode** 依靠 Watchman 來獲取關於檔案系統變化的通知。如果沒有安裝 Watchman ，**incremental mode 就無法正常使用**
    > 
    > Pyre 官網上的 pyre 展示就是使用 incremental mode，但是要使用 incremental mode 之前，你必須先安裝 Watchman ，並啟動 Watchman ，這部分沒有做，你就無法像影片中那樣優雅地使用 pyre
    > 
    > 安裝 Watchman
    > -----------
    > 
    > Watchman 也是 Facebook 釋出的開源工具，是一個檔案系統的監控工具，有支援 Windows/Linux/Mac ，安裝可參考 [Watchman 官方的安裝網頁](https://facebook.github.io/watchman/docs/install.html)
    > 
    > 使用 Pyre incremental mode
    > ------------------------
    > 
    > 1\. 進入剛剛建立的 testpy 目錄，執行 pyre init
    > 
    > ```shell
    > cd testpy
    > pyre init
    > ```
    > 
    > ![watchman](https://i2.wp.com/softnshare.com/wp-content/uploads/2018/05/watchman.jpg?resize=770%2C125&ssl=1)
    > 
    > pyre init 會問你是否要初始化 Watchman 的設定，default 是 yes ，按下 enter 就可以了
    > 
    > 執行 Watchman 
    > ------------
    > 
    > 在 testpy 目錄中執行
    > 
    > ```shell
    > watchman watch .
    > ```
    > 
    > 這代表要讓 watchman 監控 testpy 目錄中任何檔案的變動
    > 
    > 這時候只要你在 testpy 目錄中修改的任何程式碼，然後只要輸入 pyre 就會幫你做型別使用錯誤檢查，而且是使用 incremental mode ，會比使用 pyre check 快很多


# Solve Differential Equations

- [Programming for Engineers Main/Solve Differential Equations in Python](http://apmonitor.com/che263/index.php/Main/PythonDynamicSim)

## ODEINT

- [Solve Differential Equations with ODEINT](https://apmonitor.com/pdc/index.php/Main/SolveDifferentialEquations)

## GEKKO

- [Solve Differential Equations with GEKKO](https://apmonitor.com/pdc/index.php/Main/PythonDifferentialEquations)


## PyDSTool

- [pydstool/forced_spring.py at master · robclewley/pydstool](https://github.com/robclewley/pydstool/blob/master/examples/forced_spring.py)

- [Differential Equations in Python - Stack Overflow](https://stackoverflow.com/questions/5847201/differential-equations-in-python)

    > If you need to solve large nonlinear systems (especially stiff ones), the scipy tools will be slow and awkward. The [PyDSTool](http://pydstool.sourceforge.net/ "PyDSTool") package is now quite commonly used in this situation. It lets your equations be automatically converted into C code and integrates them with good solvers. It's especially good if you want to define state-defined events such as threshold crossings, add external input signals from arrays, or have other analyses done (such as bifurcation analysis, as the package includes an interface to AUTO).
    > 

## symPy (symbolic solve)

- [20-ordinary-differential-equations](https://www.sympy.org/scipy-2017-codegen-tutorial/notebooks/20-ordinary-differential-equations.html)


## Differential Equations for TensorFlow

- [Differential Equations for TensorFlow](https://dwd31415.github.io/tensorflow-diff-eq/)

- [dwd31415/tensorflow-diff-eq: Simulate differential equations using TensorFlow](https://github.com/dwd31415/tensorflow-diff-eq/tree/master)


## Euler method

- [20-ordinary-differential-equations](https://www.sympy.org/scipy-2017-codegen-tutorial/notebooks/20-ordinary-differential-equations.html)

    > ### Explicit methods[¶](https://www.sympy.org/scipy-2017-codegen-tutorial/notebooks/20-ordinary-differential-equations.html#Explicit-methods)
    > 
    > For each step taken we would update 
    > 
    > $y$ by multiplying the derivative with the step size (assuming that the derivate is approximately constant on the scale of the step-size), formally this method is known as "forward Euler":
    > 
    > $$y_{n+1} = y_n + y'(t_n)\cdot \Delta h$$
    > 
    > this is known as an _explicit_ method, i.e. the derivative at the current time step is used to calculate the next step _forward_.
    > 
    > ---
    > 
    > ### Implicit methods[¶](https://www.sympy.org/scipy-2017-codegen-tutorial/notebooks/20-ordinary-differential-equations.html#Implicit-methods)
    > 
    > For a large class of problems we need to base the step not on the derivative at the current time point, but rather at the next one (giving rise to an implicit expression). The simplest implicit stepper is "backward euler":
    > 
    > $$y_{n+1} = y_n + y'(t_{n+1})\cdot \Delta h$$
    > 
    > Problems requiring this type of steppers are known as "stiff". We will not go into the details of this (LSODA actually uses something more refined and switches between explicit and implicit steppers).
    > 


## Runge–Kutta method

- [Runge–Kutta methods - Wikiwand](https://www.wikiwand.com/en/Runge%E2%80%93Kutta_methods)


    > ![](https://upload.wikimedia.org/wikipedia/commons/7/7e/Runge-Kutta_slopes.svg)
    > 
    > The most widely known member of the Runge--Kutta family is generally referred to as "**RK4**", "**classical Runge--Kutta method**" or simply as "***the* Runge--Kutta method**".
    > 
    > Let an [initial value problem](https://www.wikiwand.com/en/Initial_value_problem) be specified as follows:
    > 
    > ![{\dot {y))=f(t,y),\quad y(t_{0})=y_{0}.](https://wikimedia.org/api/rest_v1/media/math/render/svg/25f03454fd25957cc63be11ec534efdce349c52f)
    > 
    > Here *y* is an unknown function (scalar or vector) of time *t*, which we would like to approximate; we are told that ![{\dot {y))](https://wikimedia.org/api/rest_v1/media/math/render/svg/ea068ce646833369cccf19795f23613159b5f89f), the rate at which *y* changes, is a function of *t* and of *y* itself. At the initial time ![t_{0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/02d3006c4190b1939b04d9b9bb21006fb4e6fa4a) the corresponding *y* value is ![y_{0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6d943dbbb0b56ca750c4d62c5b54b4ae29a773da). The function *f* and the data ![t_{0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/02d3006c4190b1939b04d9b9bb21006fb4e6fa4a), ![y_{0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6d943dbbb0b56ca750c4d62c5b54b4ae29a773da) are given.
    > 
    > Now pick a step-size *h* > 0 and define
    > 
    > ![{\displaystyle {\begin{aligned}y_{n+1}&=y_{n}+{\tfrac {1}{6))\left(k_{1}+2k_{2}+2k_{3}+k_{4}\right),\\t_{n+1}&=t_{n}+h\\\end{aligned))}](https://wikimedia.org/api/rest_v1/media/math/render/svg/95bdbb2e3aa83735085c0aadd577162c69e4056a)
    > 
    > for *n* = 0, 1, 2, 3, ..., using^[[2]](https://www.wikiwand.com/en/Runge%E2%80%93Kutta_methods#citenote2)^
    > 
    > ![{\displaystyle {\begin{aligned}k_{1}&=h\ f(t_{n},y_{n}),\\k_{2}&=h\ f\left(t_{n}+{\frac {h}{2)),y_{n}+{\frac {k_{1)){2))\right),\\k_{3}&=h\ f\left(t_{n}+{\frac {h}{2)),y_{n}+{\frac {k_{2)){2))\right),\\k_{4}&=h\ f\left(t_{n}+h,y_{n}+k_{3}\right).\end{aligned))}](https://wikimedia.org/api/rest_v1/media/math/render/svg/81398071e8f180ac143bfdf4598ff47bf79eb689)
    > 
    > *(Note: the above equations have different but equivalent definitions in different texts).*^[[3]](https://www.wikiwand.com/en/Runge%E2%80%93Kutta_methods#citenotenotation3)^
    > 
    > Here ![y_{n+1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6477fbeae2962cc55973c2298b8653cfd4f5e5d1) is the RK4 approximation of ![y(t_{n+1})](https://wikimedia.org/api/rest_v1/media/math/render/svg/133012f12e18d14d5b42375210936b3224fc9758), and the next value (![y_{n+1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6477fbeae2962cc55973c2298b8653cfd4f5e5d1)) is determined by the present value (![y_{n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2c5fbb0c89590b028eba7239a8803fd0cd2e698e)) plus the [weighted average](https://www.wikiwand.com/en/Weighted_average "Weighted average") of four increments, where each increment is the product of the size of the interval, *h*, and an estimated slope specified by function *f* on the right-hand side of the differential equation.
    > 
    > -   ![k_{1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/376315fd4983f01dada5ec2f7bebc48455b14a66) is the increment based on the slope at the beginning of the interval, using ![y](https://wikimedia.org/api/rest_v1/media/math/render/svg/b8a6208ec717213d4317e666f1ae872e00620a0d) ([Euler's method](https://www.wikiwand.com/en/Euler%27s_method "Euler's method"));
    > -   ![k_{2}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c51b4ba57ee596d8435fc4ed76703ca3a2fc444a) is the increment based on the slope at the midpoint of the interval, using ![y](https://wikimedia.org/api/rest_v1/media/math/render/svg/b8a6208ec717213d4317e666f1ae872e00620a0d) and ![k_{1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/376315fd4983f01dada5ec2f7bebc48455b14a66);
    > -   ![k_{3}](https://wikimedia.org/api/rest_v1/media/math/render/svg/40d32e1c66b85257bfd6ad8be93186742d71a804) is again the increment based on the slope at the midpoint, but now using ![y](https://wikimedia.org/api/rest_v1/media/math/render/svg/b8a6208ec717213d4317e666f1ae872e00620a0d) and ![k_{2}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c51b4ba57ee596d8435fc4ed76703ca3a2fc444a);
    > -   ![k_{4}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cc27eb9313ff47331edc6b7c20b35e138eaa2ef8) is the increment based on the slope at the end of the interval, using ![y](https://wikimedia.org/api/rest_v1/media/math/render/svg/b8a6208ec717213d4317e666f1ae872e00620a0d) and ![k_{3}](https://wikimedia.org/api/rest_v1/media/math/render/svg/40d32e1c66b85257bfd6ad8be93186742d71a804).
    > 
    > In averaging the four increments, greater weight is given to the increments at the midpoint. If ![f](https://wikimedia.org/api/rest_v1/media/math/render/svg/132e57acb643253e7810ee9702d9581f159a1c61) is independent of ![y](https://wikimedia.org/api/rest_v1/media/math/render/svg/b8a6208ec717213d4317e666f1ae872e00620a0d), so that the differential equation is equivalent to a simple integral, then RK4 is [Simpson's rule](https://www.wikiwand.com/en/Simpson%27s_rule "Simpson's rule").^[[4]](https://www.wikiwand.com/en/Runge%E2%80%93Kutta_methods#citenoteSli20033284)^
    > 
    > The RK4 method is a fourth-order method, meaning that the [local truncation error](https://www.wikiwand.com/en/Truncation_error_(numerical_integration)) is [on the order of](https://www.wikiwand.com/en/Big_O_notation "Big O notation") ![O(h^{5})](https://wikimedia.org/api/rest_v1/media/math/render/svg/f4f84b0c10beca633d2f744701aa5fdbe05576d3), while the [total accumulated error](https://www.wikiwand.com/en/Truncation_error_(numerical_integration) "Truncation error (numerical integration)") is on the order of ![O(h^{4})](https://wikimedia.org/api/rest_v1/media/math/render/svg/02f1837b7abfa7284a6f1f45ae38fa1795f1a3d2).
    > 
    > In many practical applications the function ![f](https://wikimedia.org/api/rest_v1/media/math/render/svg/132e57acb643253e7810ee9702d9581f159a1c61) is independent of ![t](https://wikimedia.org/api/rest_v1/media/math/render/svg/65658b7b223af9e1acc877d848888ecdb4466560) (so called [autonomous system](https://www.wikiwand.com/en/Autonomous_system_(mathematics) "Autonomous system (mathematics)"), or time-invariant system, especially in physics), and their increments are not computed at all and not passed to function ![f](https://wikimedia.org/api/rest_v1/media/math/render/svg/132e57acb643253e7810ee9702d9581f159a1c61), with only the final formula for ![t_{n+1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9eee8b33262d27347fd5fe66aebe13305038a71a) used.
    > 

### RK4 in python

- [allenyllee/runge-kutta: An implementation of the Runge-Kutta-methods for solving systems of ODEs with Python.](https://github.com/allenyllee/runge-kutta)

    > ```python
    >     def _solve(self, y, t, h):
    > 
    >         functions = self.f
    > 
    >         k1 = []
    >         for f in functions:
    >             k1.append(h * f(t, *y))
    > 
    >         k2 = []
    >         for f in functions:
    >             k2.append(h * f(t + .5*h, *[y[i] + .5*h*k1[i] for i in xrange(0, len(y))]))
    > 
    >         k3 = []
    >         for f in functions:
    >             k3.append(h * f(t + .5*h, *[y[i] + .5*h*k2[i] for i in xrange(0, len(y))]))
    > 
    >         k4 = []
    >         for f in functions:
    >             k4.append(h * f(t + h, *[y[i] + h*k3[i] for i in xrange(0, len(y))]))
    > 
    >         return [y[i] + (k1[i] + 2*k2[i] + 2*k3[i] + k4[i]) / 6.0 for i in xrange(0, len(y))]
    > ```

- [Fourth Order Runge-Kutta Method in Python - CodeProject](https://www.codeproject.com/Tips/792927/Fourth-Order-Runge-Kutta-Method-in-Python)

    > ```python
    > def rKN(x, fx, n, hs):
    >     k1 = []
    >     k2 = []
    >     k3 = []
    >     k4 = []
    >     xk = []
    >     for i in range(n):
    >         k1.append(fx[i](x)*hs)
    >     for i in range(n):
    >         xk.append(x[i] + k1[i]*0.5)
    >     for i in range(n):
    >         k2.append(fx[i](xk)*hs)
    >     for i in range(n):
    >         xk[i] = x[i] + k2[i]*0.5
    >     for i in range(n):
    >         k3.append(fx[i](xk)*hs)
    >     for i in range(n):
    >         xk[i] = x[i] + k3[i]
    >     for i in range(n):
    >         k4.append(fx[i](xk)*hs)
    >     for i in range(n):
    >         x[i] = x[i] + (k1[i] + 2*(k2[i] + k3[i]) + k4[i])/6
    >     return x
    > ```


- [Runge-Kutta 4th Order Method to Solve Differential Equation - GeeksforGeeks](https://www.geeksforgeeks.org/runge-kutta-4th-order-method-solve-differential-equation/)

    > ```python
    > 
    > # Python program to implement Runge Kutta method 
    > # A sample differential equation "dy / dx = (x - y)/2" 
    > def dydx(x, y): 
    >     return ((x - y)/2) 
    >   
    > # Finds value of y for a given x using step size h 
    > # and initial value y0 at x0. 
    > def rungeKutta(x0, y0, x, h): 
    >     # Count number of iterations using step size or 
    >     # step height h 
    >     n = (int)((x - x0)/h)  
    >     # Iterate for number of iterations 
    >     y = y0 
    >     for i in range(1, n + 1): 
    >         "Apply Runge Kutta Formulas to find next value of y"
    >         k1 = h * dydx(x0, y) 
    >         k2 = h * dydx(x0 + 0.5 * h, y + 0.5 * k1) 
    >         k3 = h * dydx(x0 + 0.5 * h, y + 0.5 * k2) 
    >         k4 = h * dydx(x0 + h, y + k3) 
    >   
    >         # Update next value of y 
    >         y = y + (1.0 / 6.0)*(k1 + 2 * k2 + 2 * k3 + k4) 
    >   
    >         # Update next value of x 
    >         x0 = x0 + h 
    >     return y 
    >   
    > # Driver method 
    > x0 = 0
    > y = 1
    > x = 2
    > h = 0.2
    > print 'The value of y at x is:', rungeKutta(x0, y, x, h) 
    >   
    > # This code is contributed by Prateek Bhindwar 
    > 
    > ```



### RK4 for Stochastic Differential Equations(SED) in tensorflow

- [Using Deep Learning Libraries to Solve Stochastic Differential Equations](http://www.martinholub.com/eth/code/2018/05/01/TheanoTensorflowSDE.html)

- [demos-blogs-examples/sde_tflow.py at master · allenyllee/demos-blogs-examples](https://github.com/allenyllee/demos-blogs-examples/blob/master/dl-bio/sde_tflow.py)

    > ```python
    >     def rk4_sde(self, x, rv_n):
    >         """Runge-Kutta 4th order method for SDE
    >         @reference http://people.sc.fsu.edu/~jburkardt/c_src/stochastic_rk/stochastic_rk.html
    >         @reference `https://en.wikipedia.org/wiki/Runge%E2%80%93Kutta_method_(SDE)`
    >         """
    >         a21 =   2.71644396264860
    >         a31 = - 6.95653259006152
    >         a32 =   0.78313689457981
    >         a41 =   0.0
    >         a42 =   0.48257353309214
    >         a43 =   0.26171080165848
    >         a51 =   0.47012396888046
    >         a52 =   0.36597075368373
    >         a53 =   0.08906615686702
    >         a54 =   0.07483912056879
    > 
    >         q1 =    2.12709852335625
    >         q2 =    2.73245878238737
    >         q3 =   11.22760917474960
    >         q4 =   13.36199560336697
    > 
    >         n = self.mp.params[0]; k = self.mp.params[1];
    >         gamma = self.mp.params[2]; dt = self.mp.params[3];
    > 
    >         if x.get_shape()[1] > 1:
    >             evolve_fun = self.evolve_system
    >         else:
    >             evolve_fun = self.evolve
    > 
    >         x1 = x
    >         k1 = dt * evolve_fun(x1, n, k, gamma) + tf.sqrt(dt) * x * rv_n
    > 
    >         x2 = x1 + a21 * k1
    >         k2 = dt * evolve_fun(x2, n, k, gamma) + tf.sqrt(dt) * x * rv_n
    > 
    >         x3 = x1 + a31 * k1 + a32 * k2
    >         k3 = dt * evolve_fun(x3, n, k, gamma) + tf.sqrt(dt) * x * rv_n
    > 
    >         x4 = x1 + a41 * k1 + a42 * k2
    >         k4 = dt * evolve_fun(x4, n, k, gamma) + tf.sqrt(dt) * x * rv_n
    > 
    >         x_new = x1 + a51 * k1 + a52 * k2 + a53 * k3 + a54 * k4
    > 
    >         return tf.cast(x_new, tf.float32)
    > ```






# 其他

## Python制作CSDN免积分下载器

- [Python制作CSDN免积分下载器 - Python开发社区 | CTOLib码库](https://www.ctolib.com/topics-43904.html)

    > CSDN免积分下载 你懂的。
    > 1、输入资源地址如：http://download.csdn.net/download/gengqkun/4127808
    > 2、输入验证码
    > 3、点击下载，会弹出浏览器下载。
    > 注：成功率在70-80% ，界面很丑，请将就着用。
    > 
    > ```python
    >  #-*-coding:utf-8-*-
    >  #python3.3.5
    >  import urllib.parse,urllib.request,http.cookiejar,io,webbrowser
    >  import tkinter as tk
    >  from tkinter import *
    >  from tkinter.ttk import *
    >  from urllib.request import urlopen
    >  from PIL import Image, ImageTk
    >  global root
    >  #设置cookie
    >  cookie = http.cookiejar.CookieJar()
    >  cookieProc = urllib.request.HTTPCookieProcessor(cookie)
    >  opener = urllib.request.build_opener(cookieProc)
    >  urllib.request.install_opener(opener)
    >  #根据路径和POST内容来提交表单
    >  def getUrlRequest(iUrl,iStrPostData):
    >      postdata = urllib.parse.urlencode(iStrPostData)
    >      postdata = postdata.encode(encoding='UTF8')
    >      header = {'User-Agent':'Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; WOW64; Trident/5.0)'}
    >      req= urllib.request.Request(
    >                 url = iUrl,
    >                 data = postdata,
    >                 headers = header)
    >      data = urllib.request.urlopen(req).read()
    >      try:
    >          data = data.decode('utf-8')
    >      except:
    >          data = data.decode('gbk', 'ignore')
    >      return data
    >  #获取验证码图片
    >  def getCodeImg():
    >      urlCode='http://csdn.juming.com/code.htm'
    >      image_bytes = urlopen(urlCode).read()
    >      # internal data file
    >      data_stream = io.BytesIO(image_bytes)
    >      # open as a PIL image object
    >      pil_image = Image.open(data_stream)
    >      tk_image = ImageTk.PhotoImage(pil_image)
    >      return tk_image
    >  #构建界面
    >  def createGui(msg=''):
    >      global root
    >      root = tk.Tk()
    >      root.title("CSDN免积分下载器 v0.1")
    >      root.resizable(False, False)   #禁止修改窗口大小
    >      root.geometry('+400+250')  #屏幕位置
    >      #-------------------------------------------
    >      tk_image = getCodeImg()
    >      # put the image on a typical widget
    >      frm_top_label = tk.Label(root,compound = 'top',image=tk_image,text="验证码图片",fg="blue",bg="brown",font=('Tempus Sans ITC',20))
    >      frm_top_label.grid(row = 0, column = 0, padx = 15, pady = 2)
    >      #-------------------------------------------
    >      frm_bottom = tk.LabelFrame(root)
    >      frm_bottom.grid(row = 1, column = 0, padx = 15, pady = 2)
    >      frm_bottom_label_0 = tk.Label(frm_bottom,text="下载地址:", font=('Tempus Sans ITC',15))
    >      frm_bottom_label_0.grid(row = 0, column = 0, padx = 5, pady = 2,sticky = "e") #控件右对齐
    >      frm_bottom_label_1 = tk.Label(frm_bottom,text="  验证码:", font=('Tempus Sans ITC',15))
    >      frm_bottom_label_1.grid(row = 1, column = 0, padx = 5, pady = 2,sticky = "e")
    >      frm_bottom_entry_var_0 = StringVar()
    >      frm_bottom_entry_0 = tk.Entry(frm_bottom,textvariable=frm_bottom_entry_var_0)
    >      frm_bottom_entry_0.grid(row = 0, column = 1, padx = 15, pady = 2)
    >      frm_bottom_entry_var_1 = StringVar()
    >      frm_bottom_entry_1 = tk.Entry(frm_bottom,textvariable=frm_bottom_entry_var_1) #设置密码输入框，熟悉show
    >      frm_bottom_entry_1.grid(row = 1, column = 1, padx = 15, pady = 2)
    >      frm_bottom_btn_0 = tk.Button(frm_bottom,text="下   载",relief=RIDGE,bd=4,width=10, font=('Tempus Sans ITC',12),command=lambda:downloadSource(frm_bottom_entry_var_0,frm_bottom_entry_var_1,frm_top_label,frm_foot_label))
    >      frm_bottom_btn_0.grid(row = 3, column = 1, padx = 15, pady = 2,sticky = "w")
    >      frm_foot_label = tk.Label(root,text=msg ,font=('Tempus Sans ITC',10))
    >      frm_foot_label.grid(row = 3, column = 0, padx = 15, pady = 2)
    >      root.mainloop() 
    >  #获取下载资源地址
    >  def getSourceUrl(code,ziyuandz):
    >      #资源信息
    >      strLoginInfo = {'csdn_zh': '用户名',
    >                      'csdn_mm': '密码',
    >                      're_yzm':code,
    >                      'ziyuandz':ziyuandz #'http://download.csdn.net/detail/shinian1987/8430743' #
    >                      }
    >      #下载资源地址
    >      urlLogin='http://csdn.juming.com/index.htm'
    >      returnHtml = str(getUrlRequest(urlLogin,strLoginInfo))
    >      a = returnHtml.find('电信下载地址：<strong>') + 15
    >      b = returnHtml.find('</strong><br>网通下载地址：')
    >      durl = returnHtml[a:b]
    >      return durl
    >  #下载资源
    >  def downloadSource(frm_bottom_entry_var_0,frm_bottom_entry_var_1,frm_top_label,frm_foot_label):
    >      try:
    >          ziyuandz = frm_bottom_entry_var_0.get()
    >          code = frm_bottom_entry_var_1.get()
    >          durl = getSourceUrl(code,ziyuandz)
    >          print('资源地址：'+ durl)
    >          reMsg = "已经打开浏览器，请下载..."
    >          yzm = durl.find("验证码")
    >          #yzm += durl.find("验证码验证错误")
    >          #yzm += durl.find("验证码输入不正确")
    >          fs = durl.find("封杀本工具特意加")
    >          gs = durl.find("正确的格式如")
    >          jf = durl.find("成功获取到0点积分")
    >          xzzy = durl.find("http:")
    >          if fs > 0:
    >              reMsg = "该资源被封杀，请稍后再下载..."
    >          elif code=='':
    >              reMsg = "验证码不能为空..."
    >          elif ziyuandz=='':
    >              reMsg = "下载地址不能为空..."
    >          elif gs > 0:
    >              reMsg = "资源地址错误，请重新输入..."
    >          elif yzm > 0:
    >              reMsg = "验证码输入错误..."
    >          elif jf > 0:
    >              reMsg = "积分不足，资源无法下载..."
    >          elif xzzy >= 0: 
    >              webbrowser.open(durl, new=0, autoraise=True)
    >          else:
    >              reMsg = "资源错误或没有找到下载资源..."
    >          #print(xzzy)
    >          frm_foot_label['text'] = reMsg
    >          tk_image = getCodeImg()
    >          frm_top_label.configure(image = tk_image)
    >          frm_top_label.image= tk_image
    >      except:
    >          root.destroy()
    >          createGui('程序错误，请重新下载...')
    >  #MAIN
    >  createGui()
    > ```