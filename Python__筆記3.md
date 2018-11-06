# Python__筆記3

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