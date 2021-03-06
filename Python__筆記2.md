# Python__筆記2

[toc]
<!-- toc --> 

# Jupyter Notebook 

## tips

- [28 Jupyter Notebook tips, tricks and shortcuts](https://www.dataquest.io/blog/jupyter-notebook-tips-tricks-shortcuts/)


## Usage


### Keyboard Shortcuts

- [How do I comment out multiple lines in Jupyter Ipython notebook? - Stack Overflow](https://stackoverflow.com/questions/29885371/how-do-i-comment-out-multiple-lines-in-jupyter-ipython-notebook)

    > Ctrl \+ / works for me in Chrome browser in MS Windows

- [28 Jupyter Notebook tips, tricks and shortcuts](https://www.dataquest.io/blog/jupyter-notebook-tips-tricks-shortcuts/)

    1\. Keyboard Shortcuts
    ----------------------

    As any power user knows, keyboard shortcuts will save you lots of time. Jupyter stores a list of keybord shortcuts under the menu at the top: `Help > Keyboard Shortcuts`, or by pressing `H` in command mode (more on that later). It's worth checking this each time you update Jupyter, as more shortcuts are added all the time.

    Another way to access keyboard shortcuts, and a handy way to learn them is to use the command palette: `Cmd + Shift + P` (or `Ctrl + Shift + P` on Linux and Windows). This dialog box helps you run any command by name - useful if you don't know the keyboard shortcut for an action or if what you want to do does not have a keyboard shortcut. The functionality is similar to Spotlight search on a Mac, and once you start using it you'll wonder how you lived without it!

    ![](https://www.dataquest.io/blog/content/images/command-palette.gif)

    _The command palette._

    Some of my favorites:

    -   `Esc` will take you into command mode where you can navigate around your notebook with arrow keys.
    -   While in command mode:
        -   `A` to insert a new cell above the current cell, `B` to insert a new cell below.
        -   `M` to change the current cell to Markdown, `Y` to change it back to code
        -   `D + D` (press the key twice) to delete the current cell
    -   `Enter` will take you from command mode back into edit mode for the given cell.
    -   `Shift + Tab` will show you the Docstring (documentation) for the the object you have just typed in a code cell - you can keep pressing this short cut to cycle through a few modes of documentation.
    -   `Ctrl + Shift + -` will split the current cell into two from where your cursor is.
    -   `Esc + F` Find and replace on your code but not the outputs.
    -   `Esc + O` Toggle cell output.
    -   Select Multiple Cells:
        -   `Shift + J` or `Shift + Down` selects the next sell in a downwards direction. You can also select sells in an upwards direction by using `Shift + K` or `Shift + Up`.
        -   Once cells are selected, you can then delete / copy / cut / paste / run them as a batch. This is helpful when you need to move parts of a notebook.
        -   You can also use `Shift + M` to merge multiple cells.

    ![](https://www.dataquest.io/blog/content/images/multi-merge.gif)

    _Merging multiple cells._


### Restart Kernel (to release GPU memory)

- [jupyter - Restart ipython Kernel with a command from a cell - Stack Overflow](https://stackoverflow.com/questions/37751120/restart-ipython-kernel-with-a-command-from-a-cell)

    ```python
    import os
    os._exit(00)
    ```


### Using git bash in jupyter noteobok on Windows

- [Using git bash in jupyter noteobok on Windows – Konpat Ta Preechakul – Medium](https://medium.com/@konpat/using-git-bash-in-jupyter-noteobok-on-windows-c88d2c3c7b07)

    > Since [https://github.com/jupyter/notebook/pull/3087](https://github.com/jupyter/notebook/pull/3087) (notebook version 5.3.0), there is a support for terminal on Windows!
    > 
    > So if you have notebook version 5.3.0 or better installed (check by `jupyter notebook --version` ), you can new “terminal” in your menu!
    > 
    > The default shell is “powershell.exe”, but you can change it in `.jupyter/jupyter_notebook_config.py`
    > 
    > The following is a config to use **Git Bash**:
    > 
    >
    > ```
    > c.NotebookApp.terminado_settings = {  
    >     'shell_command': \['C:\\\Program Files\\\Git\\\bin\\\bash.exe'\]  
    > }
    > ```
    > Restart your notebook and see the change!
    > 

### Flush output in Jupyter notebook
- [python - Flush output in for loop in Jupyter notebook - Stack Overflow](https://stackoverflow.com/questions/43150097/flush-output-in-for-loop-in-jupyter-notebook)

    > 
    > ```
    > #Try this:
    > import sys
    > import time
    > 
    > for i in range (10):  
    >     sys.stdout.write('\r'+str(i))
    >     time.sleep(0.5)
    > ```
    > 
    > __'\\r' will print at the beginning of the line__
    > 


### Timing (%timeit, %%timeit)

- [[译]27 个Jupyter Notebook的小提示与技巧 - Focus on ML & DM](http://liuchengxu.org/pelican-blog/jupyter-notebook-tips.html)

    > #### 11\. Jupyter Magic - Timing
    > 
    > 对于计时有两个十分有用的魔法命令：`%%time` 和 `%timeit`. 如果你有些代码运行地十分缓慢，而你想确定是否问题出在这里，这两个命令将会非常方便。
    > 
    > -   `%%time` 将会给出cell的代码运行一次所花费的时间。
    > ```
    > %%time
    > import time
    > for _ in range(1000):
    >     time.sleep(0.01)# sleep for 0.01 seconds
    > ```
    > CPU times: user 196 ms, sys: 21.4 ms, total: 217 ms
    > Wall time: 11.6 s
    > 
    > -   `%timeit` 使用Python的timeit模块，它将会执行一个语句100，000次(默认情况下)，然后给出运行最快3次的平均值。
    > ```
    > import numpy
    > %timeit numpy.random.normal(size=100)
    > ```
    > The slowest run took 46.45 times longer than the fastest. This could mean that an intermediate result is being cached.
    > 100000 loops, best of 3: 6.26 µs per loop

### enable Intellisense

- [Jupyter Notebook - how to enable Intellisense - Part 1 (2017) - Deep Learning Course Forums](https://forums.fast.ai/t/jupyter-notebook-how-to-enable-intellisense/8636)

    > At the top of your note book add this line
    > ```
    > %config IPCompleter.greedy=True
    > ```
    > Then when you have an object, for example numpy (np) do this
    > 
    > np.
    > 
    > After the . press [TAB] and it will show you all the methods available.
    > 
    > ![image](https://forums.fast.ai/uploads/default/original/2X/7/74dcf4e1ed201c145dfa3abf8ec869f9d14ac7f5.png)
    > 
    > Another useful thing is method parameters. Juypter will show you these if you press [SHIFT] and [TAB] from within the method parentheses. Eg.
    > 
    > ![image](https://forums.fast.ai/uploads/default/optimized/2X/6/6f004d312808decc4b3e8abfe12a03f667becd92_1_690x125.png)
    > 
    > Cheers
    > Rich
    > 

### Enable code autocompletion menu for every keypress

- [python - iPython Code Completion / Intellisense on Dot Possible? - Stack Overflow](https://stackoverflow.com/questions/33700112/ipython-code-completion-intellisense-on-dot-possible)

    > **Answer**: Install [nbextensions](https://jupyter-contrib-nbextensions.readthedocs.io/en/latest/index.html) and enable the Hinterland extension.
    > 
    > > Enable code autocompletion menu for every keypress in a code cell, instead of only calling it with tab.
    > 
    > Here's what you do:
    > 
    > 1.  `pip install jupyter_contrib_nbextensions`
    > 2.  `jupyter contrib nbextension install --user`
    > 3.  Start `jupyter notebook` (browser launches)
    > 4.  One of the **tabs** should now show "**Nbextensions**"
    > 5.  There, you will find "**Hinterland**". Check the box to enable.
    > 
    > Hinterland has some adjustable options like:
    > 
    > -   **hinterland.hint_delay**: delay in milliseconds between keypress & hint request.
    > -   **hinterland.enable_at_start**: Whether to enable hinterland's continuous hinting when notebook is first opened, or if false, only when selected from the help-menu item.
    > -   **hinterland.hint_inside_comments**: Whether to request hints while typing code comments. Defaults to false.
    > -   **Other regex options**: hinterland.exclude_regexp, hinterland.include_regexp, hinterland.tooltip_regexp
    > 
    > * * * * *
    > 
    > [![enter image description here](https://i.stack.imgur.com/cDHlC.png)](https://i.stack.imgur.com/cDHlC.png)
    > 



## Tutorial

- [Jupyter Notebook 快速入门（上）| 编程派 | Coding Python](http://codingpy.com/article/getting-started-with-jupyter-notebook-part-1/)

- [Jupyter Notebook 快速入门（下）| 编程派 | Coding Python](http://codingpy.com/article/getting-started-with-jupyter-notebook-part-2/)

- [Jupyter + Tensorflow + Nvidia GPU + Docker + Google Compute Engine](https://medium.com/google-cloud/jupyter-tensorflow-nvidia-gpu-docker-google-compute-engine-4a146f085f17)



## using pip install in jupyter notebook


- [python - PIP module has no attribute "main" - Stack Overflow](https://stackoverflow.com/questions/43398961/pip-module-has-no-attribute-main)

    > they made a refactoring. you can support both 9 and 10 pip by using:
    > 
    > ```
    > try:
    >     from pip import main as pipmain
    > except:
    >     from pip._internal import main as pipmain
    > ```
    > 
    > and then use pipmain as you used pip.main. for example
    > 
    > ```
    > pipmain(['install', "--upgrade", "pip"])
    > pipmain(['install', "-q", "package"])
    > ```

## Shortcut

### delete selected cell(`d`,`d`)

- [Keyboard shortcuts for ipython notebook 3.1.0 / jupyter](https://gist.github.com/kidpixo/f4318f8c8143adee5b40)

    > * D,D : delete selected cell
    > 

### clear cell output(`Esc` `R` `Y`)

- [python - keyboard shortcut to clear cell output in jupyter notebook - Stack Overflow](https://stackoverflow.com/questions/39924826/keyboard-shortcut-to-clear-cell-output-in-jupyter-notebook)

    > For versions less than 5:
    > 
    > ### Option 1 -- quick hack:
    > 
    > Change the cell type to raw then back to code: `Esc``R``Y` will discard the output.
    > 
    > ---
    > 
    > You can setup your own shortcut in the UI (for the latest master version):
    > 
    > [![enter image description here](https://i.stack.imgur.com/xmPho.png)](https://i.stack.imgur.com/xmPho.png)
    > 
    > Specifically, this is under `Help > Edit Keyboard Shortcuts` in any open notebook. -- [Nate](https://stackoverflow.com/users/1250841/nate "752 reputation") [Aug 17 '17 at 0:08](https://stackoverflow.com/questions/39924826/keyboard-shortcut-to-clear-cell-output-in-jupyter-notebook#comment78407157_42622902)

## config

### where is jupyter_notebook_config.py

- [python - Ipython Notebook: where is jupyter_notebook_config.py in Mac? - Stack Overflow](https://stackoverflow.com/questions/32625939/ipython-notebook-where-is-jupyter-notebook-config-py-in-mac)

    > Look in your home directory for a `.jupyter` folder. It should contain the file according to the [docs](https://jupyter-notebook.readthedocs.org/en/latest/examples/Notebook/Configuring%20the%20Notebook%20and%20Server.html):
    > 
    > > The notebook web server can also be configured using Jupyter profiles and configuration files. The Notebook web server configuration options are set in a file named jupyter_notebook_config.py in your Jupyter directory, which itself is usually .jupyter in your home directory.
    > 
    > If the `.jupyter` folder does not contain a `jupyter_notebook_config.py` file, you need to generate it with `jupyter notebook --generate-config`.

### File save hooks

- [File save hooks — Jupyter Notebook 5.6.0 documentation](https://jupyter-notebook.readthedocs.io/en/stable/extending/savehooks.html)


- [IPython and Jupyter Notebooks: Automatically Export .py and .html - Dev pro tips](https://protips.maxmasnick.com/ipython-notebooks-automatically-export-py-and-html)


    > put the following in a file saved at ~/.jupyter/jupyter_notebook_config.py to achieve the same thing:
    > 
    > ```python
    > # Based off of https://github.com/jupyter/notebook/blob/master/docs/source/extending/savehooks.rst
    > 
    > import io
    > import os
    > from notebook.utils import to_api_path
    > 
    > _script_exporter = None
    > _html_exporter = None
    > 
    > def script_post_save(model, os_path, contents_manager, **kwargs):
    >     """convert notebooks to Python script after save with nbconvert
    >     replaces `ipython notebook --script`
    >     """
    >     from nbconvert.exporters.script import ScriptExporter
    >     from nbconvert.exporters.html import HTMLExporter
    > 
    >     if model['type'] != 'notebook':
    >         return
    > 
    >     global _script_exporter
    >     if _script_exporter is None:
    >         _script_exporter = ScriptExporter(parent=contents_manager)
    >     log = contents_manager.log
    > 
    >     global _html_exporter
    >     if _html_exporter is None:
    >         _html_exporter = HTMLExporter(parent=contents_manager)
    >     log = contents_manager.log
    > 
    >     # save .py file
    >     base, ext = os.path.splitext(os_path)
    >     script, resources = _script_exporter.from_filename(os_path)
    >     script_fname = base + resources.get('output_extension', '.txt')
    >     log.info("Saving script /%s", to_api_path(script_fname, contents_manager.root_dir))
    >     with io.open(script_fname, 'w', encoding='utf-8') as f:
    >         f.write(script)
    > 
    >     # save html
    >     base, ext = os.path.splitext(os_path)
    >     script, resources = _html_exporter.from_filename(os_path)
    >     script_fname = base + resources.get('output_extension', '.txt')
    >     log.info("Saving html /%s", to_api_path(script_fname, contents_manager.root_dir))
    >     with io.open(script_fname, 'w', encoding='utf-8') as f:
    >         f.write(script)
    > c.FileContentsManager.post_save_hook = script_post_save
    > ```
    > 

### setup automated config file with a password prompt

- [Can one set up automated config file with a password prompt? · Issue #1700 · jupyter/notebook](https://github.com/jupyter/notebook/issues/1700)
    
    > I wrote a [small python script](https://github.com/paderijk/jupyter-password) that creates the correct password entry. Although would be nice if there is a flag like `--set-password`, so for example:
    > 
    > ```source-shell
    > jupyter notebook --generate-config --set-password
    > ```
    > 
    > Or to reset it:
    > 
    > ```source-shell
    > jupyter notebook --set-password
    > ```



- [How to change a password for Jupyter notebook - Part 1 (2017) - Deep Learning Course Forums](http://forums.fast.ai/t/how-to-change-a-password-for-jupyter-notebook/2900)


    > I used a notebook to create sha1 hash with the following code:
    > 
    > > from notebook.auth import passwd\
    > > passwd()
    > 
    > I put a result in the config file at /home/ubuntu/.jupyter/jupyter_notebook_config.py something like this:
    > 
    > > c.NotebookApp.password = u'sha1:67c9e60bb8b6:9ffede0825894254b2e042ea597d771089e11aed'
    > 
    > I know that this config file is being used because I have other parameters such as a path to certificate file and a port number and they work just fine. I start Jupyter with sudo like this:
    > 
    > > sudo /home/ubuntu/anaconda2/bin/jupyter notebook --no-browser --config=/home/ubuntu/.jupyter/jupyter_notebook_config.py &
    > 
    > 
    > Basically, I need to find out where the default password is defined since it wasn't set in jupyter_notebook_config.py initially and it seems like it overrides my own password definition.
    > 
    > ---

    > 
    > My guess is that you still have the original
    > ```
    > c.NotebookApp.password = ...
    > ```
    > line at the end of the file.
    > 
    > ---
    > 
    > You are absolutely right! It was still at the end of the file. I used the entry in the middle of the file and didn't see that all parameters were defined at the end.


### '_xsrf' argument missing from POST

- [Remote Kernels: "'_xsrf' argument missing from POST" when token is empty string · Issue #922 · nteract/hydrogen](https://github.com/nteract/hydrogen/issues/922)

    > This can be solved by changing `#c.NotebookApp.disable_check_xsrf = False` to `c.NotebookApp.disable_check_xsrf = True` in jupyter_notebook_config.py.


### set env variable in Jupyter notebook

- [python - How to set env variable in Jupyter notebook - Stack Overflow](https://stackoverflow.com/questions/37890898/how-to-set-env-variable-in-jupyter-notebook)

    > You can setup environment variables in your code as follows:
    > 
    > ```python
    > import sys,os,os.path
    > sys.path.append(os.path.expanduser('~/code/eol_hsrl_python'))
    > os.environ['HSRL_INSTRUMENT']='gvhsrl'
    > os.environ['HSRL_CONFIG']=os.path.expanduser('~/hsrl_config')
    > ```
    > 
    > This if of course a temporary fix, to get a permanent one, you probably need to export the variables into your `~.profile`, more information can be found [here](https://support.enthought.com/hc/en-us/articles/204469160-How-do-I-set-PYTHONPATH-and-other-environment-variables-for-Canopy-)
    > 
    > ---
    > 
    > To set an env variable in a jupyter notebook, just use a `%` magic commands, either `%env` or `%set_env`, e.g., `%env MY_VAR=MY_VALUE` or `%env MY_VAR MY_VALUE`. (Use `%env` by itself to print out current environmental variables.)
    > 
    > See: <http://ipython.readthedocs.io/en/stable/interactive/magics.html>



- [library path not work in notebook · Issue #1290 · jupyter/notebook](https://github.com/jupyter/notebook/issues/1290)

    > Ok, i found solution, but still think that it's some problem with notebook: it's not take system variables and not using the ones that i load in code.\
    > Solution:\
    > Generate config file:\
    > `jupyter notebook --generate-config`\
    > It will be stored i:\
    > `jupyter --config-dir`\
    > Add this code at start:
    > 
    > ```python
    > import os
    > c = get_config()
    > os.environ['LD_LIBRARY_PATH'] = '/usr/local/cuda-7.5/lib64:usr/local/cuda-7.5/lib64/libcudart.so.7.5'
    > c.Spawner.env.update('LD_LIBRARY_PATH')
    > 
    > ```
    > 
    > And everything work
    > 

### launching from a GUI launcher with environments variables set in `.bashrc`

- [Unable to import tensorflow in jupyter (yet able to import tensorflow in python and ipython) · Issue #2120 · jupyter/notebook](https://github.com/jupyter/notebook/issues/2120)

    > Are you launching the Jupyter applications from a GUI launcher? If so, they won't pick up environment variables set in `.bashrc` or `.bash_profile`. A simple workaround is to launch them from a terminal.
    > 
    > On Linux, you can set environment variables in `.profile`, which is run when you log in. I don't know how to do the same on OSX.


## jupyter notebook with git workflow

- [How to use git with iPython notebooks : IPython](https://www.reddit.com/r/IPython/comments/3na2ud/how_to_use_git_with_ipython_notebooks/)

- [Remove output from IPython notebook from the command line (dev version 1.0)](https://gist.github.com/damianavila/5305869)

- [Git - Git Hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks)



- [My IPython-powered semi-automatic git workflow | Damian's blog](http://www.damian.oquanta.info/posts/my-ipython-powered-semi-automatic-git-workflow.html)

    > ### Get everything ready...
    > 
    > First, we need to set up the environment to make our work:
    > 
    > -   Check the current working directory:
    >     ```
    >     %pwd
    >     ```
    > 
    > -   Make a new folder to isolate our work and cd into it:
    >     ```
    >     !mkdir devel_example
    >     ```
    > 
    >     ```
    >     %cd devel_example/
    >     ```
    > 
    >     > **NOTE**: You can avoid these steps opening the notebook in the proper directory, but in this case I want to have the example isolated to not overwrite my current development environment.
    > 
    > -   Load variables with useful information:
    >     ```bash
    >     project_name = "ipython"
    >     project_remote = "git://github.com/ipython/ipython.git"
    >     project_remote_name = "origin"
    >     my_fork_remote = "git@github.com:damianavila/ipython.git"
    >     my_fork_remote_name = "damianavila"
    >     ```
    > 
    > -   Clone the project and connect the local repo with my **Github** fork:
    >     ```bash
    >     # Get a read-only copy of the project
    >     !git clone $project_remote
    > 
    >     # cd into the local project folder
    >     %cd $project_name
    > 
    >     # Link the local repo with my Github fork
    >     !git remote add $my_fork_remote_name $my_fork_remote
    > 
    >     # Check remotes
    >     !git remote -v
    >     ```
    > ---
    > 
    > -   Set up the `master` and `development` branch names:
    >     ```
    >     master_branch = "master"
    >     feature_branch = "doc_post_serve"
    >     ```
    > 
    > 
    > -   Create a new branch from `master`:
    >     ```
    >     # Make sure we are in master branch
    >     !git checkout $master_branch
    > 
    >     # Pull the changes from origin/master
    >     !git pull $project_remote_name
    > 
    >     # Start a new branch to work on
    >     !git checkout -b $feature_branch
    > 
    >     # Check where we are
    >     !git status
    >     ```
    > ---
    > 
    > -   Check the status and diff of your modifications:
    >     ```bash
    >     # Check status
    >     !git status
    > 
    > 
    >     # See the diff
    >     !git diff
    >     ```
    > 
    > -   Add the changes an commit them:
    >     ```bash
    >     # Add the modified files to the stage
    >     !git add .
    >     ```
    >     ```bash
    >     # And do your commit
    >     !git commit -am "Added --post-serve explanation into the nbconvert docs."
    >     ```
    > 
    > -   Finally, push your local development branch to your **Github** fork:
    >     ```bash
    >     # Push updates from your local branch to your github branch
    >     !git push $my_fork_remote_name $feature_branch
    >     ```
    > 

- [github - Is there a way to integrate git with Jupyter and have a version control over the notebooks created? - Stack Overflow](https://stackoverflow.com/questions/34941546/is-there-a-way-to-integrate-git-with-jupyter-and-have-a-version-control-over-the)

    > You can version jupyter notebooks directly using [kyso.io](https://kyso.io) (disclaimer: I founded kyso).
    > 
    > Kyso supports the Jupyter format fully so you can render them nicely, and have proper versioning, diffing and merging of .ipynb files.
    > 
    > ---
    > 
    > This extension enables users to push ipython notebooks to GitHub directly without even leaving jupyter. Currently it is a jupyter extension but can be extended for jupyterhub.
    > 
    > <https://github.com/sat28/githubcommit>
    > 
    > ---
    > Have a look at " nbdime " project, Solves all the issues in visualizing the diff in big notebook
    > 
    > [jupyter/nbdime: Tools for diffing and merging of Jupyter notebooks.](https://github.com/jupyter/nbdime)
    > 

### extension

- [An easy way to install Jupyter Notebook extensions « Robin's Blog](http://blog.rtwilson.com/an-easy-way-to-install-jupyter-notebook-extensions/comment-page-1/)

- [ipython-contrib/jupyter_contrib_nbextensions: A collection of various notebook extensions for Jupyter](https://github.com/ipython-contrib/jupyter_contrib_nbextensions)

- [Unofficial Jupyter Notebook Extensions — jupyter_contrib_nbextensions 0.5.0 documentation](https://jupyter-contrib-nbextensions.readthedocs.io/en/latest/)

- [Notebook extensions | Jupyter](https://carreau.gitbooks.io/jupyter-book/content/notebook-extensions.html)

- [Commit-and-Push to GitHub from Jupyter Notebooks – Gab41](https://gab41.lab41.org/commit-and-push-to-github-from-jupyter-notebooks-579f5743a50b)

    > To better integrate Jupyter with our existing development workflow, we wrote a custom Jupyter extension to "Commit-and-Push" directly to GitHub from a notebook. The extension has two core components:
    > 
    > -   A new button on the frontend, implemented in Javascript, captures the user's commit message and name of the current notebook
    > -   A backend Python script receives that data and uses the [gitpython](https://github.com/gitpython-developers/GitPython) module to automate the following tasks:
    > 
    > 1.  Check out a new branch
    > 2.  Commit changes to the identified notebook
    > 3.  Push commits to GitHub
    > 4.  Submit a Pull Request
    > 
    > ![](https://cdn-images-1.medium.com/max/800/0*GK_VvzrmyTU4cEXJ.png)
    > 
    > *Commit-and-push extension within a Jupyter notebook*
    > 
    > ![](https://cdn-images-1.medium.com/max/800/0*M7xOfv2FDZJiAkur.png)
    > 
    > *Commit message in Jupyter notebook*
    > 
    > ![](https://cdn-images-1.medium.com/max/800/0*MoCqFcaeDRiCltiv.png)
    > 
    > *GitHub pull request from commit-and-push extension*
    > 
    > ---
    > 
    > [sunny-side-up/frameworks/docker/keras-cuda-jupyter/config/jupyter at master · Lab41/sunny-side-up](https://github.com/Lab41/sunny-side-up/tree/master/frameworks/docker/keras-cuda-jupyter/config/jupyter)

### script

- [Keeping IPython notebooks under Git version control](https://gist.github.com/pbugnion/ea2797393033b54674af)

- [GitCheckpoints/gitcheckpoints at master · csiro-scientific-computing/GitCheckpoints](https://github.com/csiro-scientific-computing/GitCheckpoints/tree/master/gitcheckpoints)

    > A Checkpoints subclass that commits the file every checkpoint
    > 

- [Automatically commit and push IPython notebook | low order magic](http://pvh.wp.sanbi.ac.za/2015/11/06/automatically-commit-and-push-ipython-notebook/)

    > So here's my code:
    > 
    > ```python
    > import os
    > from subprocess import check_call
    > from shlex import split
    > 
    > def post_save(model, os_path, contents_manager):
    >     """post-save hook for doing a git commit / push"""
    >     if model['type'] != 'notebook':
    >         return # only do this for notebooks
    >     workdir, filename = os.path.split(os_path)
    >     if filename.startswith('Scratch') or filename.startswith('Untitled'):
    >         return # skip scratch and untitled notebooks
    >     # now do git add / git commit / git push
    >     check_call(split('git add {}'.format(filename)), cwd=workdir)
    >     check_call(split('git commit -m "notebook save" {}'.format(filename)), cwd=workdir)
    >     check_call(split('git push'), cwd=workdir)
    > 
    > c.FileContentsManager.post_save_hook = post_save
    > 
    > ```
    > 
    > This code obviously assumes that your working directory is a git repository and it has been configured with a remote to push to. For this workshop my notebooks are in [this](https://github.com/pvanheus/swc15nwu-python) git repo on GitHub.
    > 
    > I created a new IPython profile (`ipython profile create swcteaching`) for use while teaching and added that code to the `ipython_notebook_config.py` file. You can find this file's location with `ipython profile locate swcteaching`.
    > 
    > The one little niggle is that the commit message is always the same. I don't know IPython's front-end code well enough, but perhaps there is a way to pop up a window and request a commit message (going towards something more like David Dotson's solution and less like mine).


- [ipython notebook --script deprecated. How to replace with post save hook? - Stack Overflow](https://stackoverflow.com/questions/29329667/ipython-notebook-script-deprecated-how-to-replace-with-post-save-hook)

    > **Find your config files:**
    > 
    > *Jupyter / ipython >= 4.0*
    > 
    > ```
    > jupyter --config-dir
    > 
    > ```
    > 
    > *ipython <4.0*
    > 
    > ```
    > ipython locate profile default
    > 
    > ```
    > 
    > **If you need a new config:**
    > 
    > *Jupyter / ipython >= 4.0*
    > 
    > ```
    > jupyter notebook --generate-config
    > 
    > ```
    > 
    > *ipython <4.0*
    > 
    > ```
    > ipython profile create
    > 
    > ```
    > 
    > Within this directory, there will be a file called `[jupyter | ipython]_notebook_config.py`, put the following code from [ipython's GitHub issues page](https://github.com/ipython/ipython/issues/8009 "on ipython's GitHub issues page") in that file:
    > 
    > ```python
    > import os
    > from subprocess import check_call
    > 
    > c = get_config()
    > 
    > def post_save(model, os_path, contents_manager):
    >     """post-save hook for converting notebooks to .py scripts"""
    >     if model['type'] != 'notebook':
    >         return # only do this for notebooks
    >     d, fname = os.path.split(os_path)
    >     check_call(['ipython', 'nbconvert', '--to', 'script', fname], cwd=d)
    > 
    > c.FileContentsManager.post_save_hook = post_save
    > ```
    > 
    > For Jupyter, replace `ipython` with `jupyter` in check_call.
    > 
    > Note that there's a corresponding 'pre-save' hook, and also that you can call any subprocess or run any arbitrary code there...if you want to do any thing fancy like checking some condition first, notifying API consumers, or adding a git commit for the saved script.


- [Using IPython notebooks under version control - Stack Overflow](https://stackoverflow.com/questions/18734739/using-ipython-notebooks-under-version-control)

    > 
    > After digging around, I finally found [this relatively simple pre-save hook on the Jupyter docs](http://jupyter-notebook.readthedocs.io/en/latest/extending/savehooks.html#examples). It strips the cell output data. You have to paste it into the `jupyter_notebook_config.py` file (see below for instructions).
    > 
    > ```python
    > def scrub_output_pre_save(model, **kwargs):
    >     """scrub output before saving notebooks"""
    >     # only run on notebooks
    >     if model['type'] != 'notebook':
    >         return
    >     # only run on nbformat v4
    >     if model['content']['nbformat'] != 4:
    >         return
    > 
    >     for cell in model['content']['cells']:
    >         if cell['cell_type'] != 'code':
    >             continue
    >         cell['outputs'] = []
    >         cell['execution_count'] = None
    >         # Added by binaryfunt:
    >         if 'collapsed' in cell['metadata']:
    >             cell['metadata'].pop('collapsed', 0)
    > 
    > c.FileContentsManager.pre_save_hook = scrub_output_pre_save
    > 
    > ```
    > 
    > From [Rich Signell's answer](https://stackoverflow.com/a/25765194/3217306):
    > 
    > > If you aren't sure in which directory to find your `jupyter_notebook_config.py` file, you can type `jupyter --config-dir` [into command prompt/terminal], and if you don't find the file there, you can create it by typing `jupyter notebook --generate-config`.
    > 

- [Automatically export a notebook as a script upon saving · Issue #8009 · ipython/ipython](https://github.com/ipython/ipython/issues/8009)

    > [@drorata](https://github.com/drorata) yup, sorry for being short, we're in a meeting. Here is an example (in `ipython_notebook_config.py`):
    > 
    > ```source-python
    > import os
    > from subprocess import check_call
    > 
    > def post_save(model, os_path, contents_manager):
    >     """post-save hook for converting notebooks to .py scripts"""
    >     if model['type'] != 'notebook':
    >         return # only do this for notebooks
    >     d, fname = os.path.split(os_path)
    >     check_call(['ipython', 'nbconvert', '--to', 'script', fname], cwd=d)
    > 
    > c.FileContentsManager.post_save_hook = post_save
    > ```
    > 
    > That's the simple version for exporting files to scripts on save. It's more efficient but more complex to avoid instantiating an nbconvert process by using an Exporter locally.

## debugging in jupyter notebook

### Python Debugger Cheatsheet

- For complete list of available commands: <https://appletree.or.kr/quick_reference_cards/Python/Python%20Debugger%20Cheatsheet.pdf>

### pdb/ipdb
- [Jupyter Notebook Debugging | The Mouse Vs. The Python](https://www.blog.pythonlibrary.org/2018/10/17/jupyter-notebook-debugging/)

    > ### Using pdb
    > 
    > The pdb module is Python's debugger module. Just as C++ has gdb, Python has pdb.
    > 
    > Let's start by opening up a new Notebook and adding a cell with the following code in it:
    > ```python
    > def bad_function(var):
    > 	return var + 0
    > 
    > bad_function("Mike")
    > ```
    > 
    > If you run this code, you should end up with some output that looks like this:
    > ```python
    > ---------------------------------------------------------------------------
    > TypeError                                 Traceback (most recent call last)
    > <ipython-input-1-2f23ed1cac1e> in <module>()
    >       2         return var + 0
    >       3
    > ----> 4 bad_function("Mike")
    > 
    > <ipython-input-1-2f23ed1cac1e> in bad_function(var)
    >       1 def bad_function(var):
    > ----> 2         return var + 0
    >       3
    >       4 bad_function("Mike")
    > 
    > TypeError: cannot concatenate 'str' and 'int' objects
    > ```
    > 
    > What this means is that you cannot concatenate a string and an integer. This is a pretty common problem if you don't know what types a function accepts. You will find that this is especially true when working with complex functions and classes, unless they happen to be using type hinting. One way to figure out what is going on is by adding a breakpoint using pdb's **set_trace()** function:
    > ```python
    > def bad_function(var):
    >     import pdb
    >     pdb.set_trace()
    >     return var + 0
    > 
    > bad_function("Mike")
    > ```
    > 
    > Now when you run the cell, you will get a prompt in the output which you can use to inspect the variables and basically run code live. If you happen to have **Python 3.7**, then you can simplify the example above by using the new **breakpoint** built-in, like this:
    > ```python
    > def bad_function(var):
    >     breakpoint()
    >     return var + 0
    > 
    > bad_function("Mike")
    > ```
    > 
    > This code is functionally equivalent to the previous example but uses the new **breakpoint** function instead. When you run this code, it should act the same way as the code in the previous section did.
    > 
    > You can read more about how to use pdb [here](https://docs.python.org/3/library/pdb.html).
    > 
    > You can use any of pdb's command right inside of your Jupyter Notebook. Here are some examples:
    > 
    > -   w(here) -- Print the stack trace
    > -   d(own) -- Move the current frame X number of levels down. Defaults to one.
    > -   u(p) -- Move the current frame X number of levels up. Defaults to one.
    > -   b(reak) -- With a *lineno* argument, set a break point at that line number in the current file / context
    > -   s(tep) -- Execute the current line and stop at the next possible line
    > -   c(ontinue) -- Continue execution
    > 
    > Note that these are single-letter commands: w, d, u and b are the commands. You can use these commands to interactively debug your code in your Notebook along with the other commands listed in the documentation listed above.
    > 
    > * * * * *
    > 
    > ### ipdb
    > 
    > IPython also has a debugger called **ipdb**. However it does not work with Jupyter Notebook directly. You would need to connect to the kernel using something like **Jupyter console** and run it from there to use it. If you would like to go that route, you can read more about using Jupyter console [here](https://jupyter-console.readthedocs.io/en/latest/).
    > 
    > However there is an IPython debugger that we can use called **IPython.core.debugger.set_trace**. Let's create a cell with the following code:
    > ```python
    > from IPython.core.debugger import set_trace
    > 
    > def bad_function(var):
    >     set_trace()
    >     return var + 0
    > 
    > bad_function("Mike")
    > ```
    > 
    > Now you can run this cell and get the ipdb debugger. Here is what the output looked like on my machine:
    > 
    > ![](http://www.blog.pythonlibrary.org/wp-content/uploads/2018/10/ipython_debugger-1024x491.png)
    > 
    > The IPython debugger uses the same commands as the Python debugger does. The main difference is that it provides syntax highlighting and was originally designed to work in the IPython console.
    > 
    > There is one other way to open up the **ipdb** debugger and that is by using the **%pdb** magic. Here is some sample code you can try in a Notebook cell:
    > ```python
    > %pdb
    > 
    > def bad_function(var):
    >     return var + 0
    > 
    > bad_function("Mike")
    > ```
    > 
    > When you run this code, you should end up seeing the `TypeError` traceback and then the ipdb prompt will appear in the output, which you can then use as before.
    > 
    > * * * * *
    > 
    > ### What about %%debug?
    > 
    > There is yet another way that you can open up a debugger in your Notebook. You can use `%%debug` to debug the entire cell like this:
    > ```python
    > %%debug
    > 
    > def bad_function(var):
    >     return var + 0
    > 
    > bad_function("Mike")
    > ```
    > 
    > This will start the debugging session immediately when you run the cell. What that means is that you would want to use some of the commands that pdb supports to step into the code and examine the function or variables as needed.
    > 
    > Note that you could also use `%debug` if you want to debug a single line.
    > 
    > * * * * *
    > 
    > ### Wrapping Up
    > 
    > In this chapter we learned of several different methods that you can use to debug the code in your Jupyter Notebook. I personally prefer to use Python's pdb module, but you can use the IPython.core.debugger to get the same functionality and it could be better if you prefer to have syntax highlighting.
    > 
    > There is also a newer "visual debugger" package called the PixieDebugger from the [pixiedust](https://github.com/pixiedust/pixiedust) package:
    > 
    > I haven't used it myself. Some reviewers say it is amazing and others have said it is pretty buggy. I will leave that one up to you to determine if it is something you want to add to your toolset.
    > 
    > As far as I am concerned, I think using pdb or IPython's debugger work quite well and should work for you too.
    > 


- [python - What is the right way to debug in iPython notebook? - Stack Overflow](https://stackoverflow.com/questions/32409629/what-is-the-right-way-to-debug-in-ipython-notebook)

    > Use **ipdb**
    > 
    > Install it via
    > 
    > ```
    > pip install ipdb
    > ```
    > 
    > Usage:
    > 
    > ```python
    > In[1]: def fun1(a):
    >    def fun2(a):
    >        import ipdb; ipdb.set_trace() # debugging starts here
    >        return do_some_thing_about(b)
    >    return fun2(a)
    > In[2]: fun1(1)
    > ```
    > 
    > For executing line by line use `n` and for step into a function use `s` and to exit from debugging prompt use `c`.
    > 
    > For complete list of available commands: <https://appletree.or.kr/quick_reference_cards/Python/Python%20Debugger%20Cheatsheet.pdf>
    > 




### PixieDebugger

- [Install PixieDust — PixieDust Documentation](https://pixiedust.github.io/pixiedust/install.html)




- [The Visual Python Debugger for Jupyter Notebooks You’ve Always Wanted](https://medium.com/ibm-watson-data-lab/the-visual-python-debugger-for-jupyter-notebooks-youve-always-wanted-761713babc62)

<iframe width="560" height="315" src="https://www.youtube.com/embed/Z-tPeEkVqjk" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>






# JupyterHub

<iframe width="560" height="315" src="https://www.youtube.com/embed/gSVvxOchT8Y" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

- [jupyterhub/jupyterhub - Docker Hub](https://hub.docker.com/r/jupyterhub/jupyterhub/)




# IPython


## shell command in IPython

- [Built-in magic commands — IPython 7.2.0 documentation](https://ipython.readthedocs.io/en/stable/interactive/magics.html)

- [Using Shell Commands Effectively from IPython - Safari Blog](https://archive.is/GOF3A)

    <https://www.safaribooksonline.com/blog/2014/02/12/using-shell-commands-effectively-ipython/>


    > The easiest way to call shell from IPython is to prepend an exclamation point to a shell command, like this:
    > 
    > 
    > ```py
    > In [1]:
    > 
    >   !echo $SHELL
    > 
    >   /usr/local/bin/zsh
    > ```
    > 
    > IPython executes commands using the default system shell, in my case `zsh`. By default, IPython just prints the output of the command. If you need to capture the output of the command as well, you can do this by assigning the output to variable, like so:
    > 
    > 
    > ```py
    > In [2]:
    > 
    >   df_out = !df -h
    > 
    >   df_out
    > ```
    > 
    > ```py
    > Out[2]:
    > 
    >   ['Filesystem      Size  Used Avail Use% Mounted on',
    >   '/dev/disk1      465G  218G  248G  47% /',
    >   'devfs           187K  187K     0 100% /dev']
    > ```
    > 
    > Note how the result looks to be a list of the separate lines from `stdout`. This is actually an IPython [string list](https://archive.is/o/GOF3A/ipython.org/ipython-doc/stable/interactive/shell.html%23string-lists) (`SList`).
    > 
    > 
    > ```py
    > In [3]:
    > 
    >   type(df_out)
    > ```
    > 
    > ```py
    > Out[3]:
    > 
    >   IPython.utils.text.SList
    > ```
    > 
    > ---
    > 
    > The IPython magic system
    > ------------------------
    > 
    > The exclamation point syntax is part of IPython magic\
    > commands. These are special functions that provide helpful abilities to the interpreter. IPython ships many of these by default, and you can write your own if you need custom functionality. You can see a list of the ones available in your interpreter by running the `%lsmagic` command. Note that depending on which IPython interpreter you are running (console, qtconsole, notebook), not all magics are available. In particular, using cell level magics requires running the IPython notebook. For instance, on my system running the IPython notebook I have these magics available to me:
    > 
    > 
    > ```py
    > In [9]:
    > 
    >   %lsmagic
    > ```
    > 
    > ```py
    > Out [9]
    > 
    >   Available line magics:
    > 
    >   %alias  %alias_magic  %autocall  %automagic  %autosave  %bookmark  %cd  %clear  
    > 
    >   %colors  %config  %connect_info  %debug  %dhist  %dirs  %doctest_mode  %ed  
    > 
    >   %edit  %env  %gui  %hist  %history  %install_default_config  %install_ext  
    > 
    >   %install_profiles  %killbgscripts  %less  %load  %load_ext  %loadpy  %logoff  
    > 
    >   %logon  %logstart  %logstate  %logstop  %lsmagic  %macro  %magic  %man  
    > 
    >   %matplotlib  %more  %notebook  %page  %pastebin  %pdb  %pdef  %pdoc  %pfile  
    > 
    >   %pinfo  %pinfo2  %popd  %pprint  %precision  %profile  %prun  %psearch  
    > 
    >   %psource  %pushd  %pwd  %pycat  %pylab  %qtconsole  %quickref  %recall  
    > 
    >   %rehashx  %reload_ext  %rep  %rerun  %reset  %reset_selective  %run  %save  
    > 
    >   %sc  %store  %sx  %system  %tb  %time  %timeit  %unalias  %unload_ext  %who  
    > 
    >   %who_ls  %whos  %xdel  %xmode
    > 
    >   Available cell magics:
    > 
    >   %%!  %%HTML  %%SVG  %%bash  %%capture  %%debug  %%file  %%html  %%javascript  
    > 
    >   %%latex  %%perl  %%prun  %%pypy  %%python  %%python3  %%ruby  %%script  %%sh  
    > 
    >   %%svg  %%sx  %%system  %%time  %%timeit  %%writefile
    > 
    >   Automagic is ON, % prefix IS NOT needed for line magics.
    > ```
    > 

- [python - IPython 5, key for executing block of code instead of inserting new line - Stack Overflow](https://stackoverflow.com/questions/40790947/ipython-5-key-for-executing-block-of-code-instead-of-inserting-new-line)

    > `Alt + Enter` or `Esc + Enter` execute the current code block, regardless of cursor position.


- [matplotlib - Can one remotely access an IPython Notebook without using inline plotting? - Stack Overflow](https://stackoverflow.com/questions/11462621/can-one-remotely-access-an-ipython-notebook-without-using-inline-plotting)

    > Yes, it is, at least via ssh port tunneling.
    > 
    > (NOTE: the examples blow were done on Ubuntu 12.04, but the same principle should work for other platforms)
    > 
    > I was having similar problems and found that if I run the IPython notebook from within the port- and X-forwarding ssh session (ie: the one that sets up the port and X forwarding), it works. Clunky and annoying, but it works. For example:
    > 
    > ```bash
    > at-home:~$ ssh -X -L 8889:localhost:8888 my.server
    > ... login message from my.server
    > my.server:$ cd /folder/containing/my/notebooks
    > my.server:$ ipython notebook
    > [NotebookApp] .... lots of info about the IPython notebook server including
    > [NotebookApp] The IPython notebook is running at 'http://127.0.0.1:8888/'
    > ```
    > 
    > Note that I've forwarded port 8889 - this means I use `http://localhost:8889/` in a browser on my `at-home` machine. For me, this works nicely with the Qt4Agg backend.
    > 
    > I suspect that it will also work for accessing notebooks over https if you run the IPython notebook server in this way (ie: from within an `ssh -X` session). Note that the plots will appear on the machine from which the X session was forwarded. If someone runs a notebook in a browser on another machine, this could be a bit strange!
    > 
    > It may be possible to tell a running IPython notebook server how to find the X server forwarded by some new ssh session, but I'm not sure how (knowledgeable edits welcome!).
    > 


- [python - How to run an .ipynb Jupyter Notebook from terminal? - Stack Overflow](https://stackoverflow.com/questions/35545402/how-to-run-an-ipynb-jupyter-notebook-from-terminal)

    > nbconvert allows you to run notebooks with the `--execute` flag:
    > 
    > ```bash
    > jupyter nbconvert --execute <notebook>
    > ```
    > 
    > If you want to run a notebook and produce a new notebook, you can add `--to notebook`:
    > 
    > ```bash
    > jupyter nbconvert --execute --to notebook <notebook>
    > ```
    > 
    > Or if you want to *replace* the existing notebook with the new output:
    > 
    > ```bash
    > jupyter nbconvert --execute --to notebook --inplace <notebook>
    > ```
    > 
    > Since that's a really long command, you can use an alias:
    > 
    > ```bash
    > alias nbx="jupyter nbconvert --execute --to notebook"
    > nbx [--inplace] <notebook>
    > ```

## run from ipython with glob style expansion

- [run from ipython with glob style expansion? - Stack Overflow](https://stackoverflow.com/questions/8227705/run-from-ipython-with-glob-style-expansion)

    > The return of `filenames = !ls *.sbet` is a special list, with a few extra attributes:
    > 
    > -   `filenames.l` - the list
    > -   `filenames.s` - a whitespace-separated string
    > -   `filenames.n` - a newline-separated string
    > 
    > do `filenames?` in IPython for more info.
    > 
    > So to pass the args to run, you want `filenames.s`:
    > 
    > ```
    > filenames = !ls *.sbet
    > run sbet.py $filenames.s
    > 
    > ```
    > 
    > If you have a regular list, then you will need to turn it into a string yourself, before passing to run:
    > 
    > ```
    > filenames = glob.glob('*.sbet')
    > filenames_str = ' '.join(filenames) # you will need to add quotes if you allow spaces in filenames
    > run sbet.py $filenames_str
    > 
    > ```

## clear cell output in code

- [python - ipython notebook clear cell output in code - Stack Overflow](https://stackoverflow.com/questions/24816237/ipython-notebook-clear-cell-output-in-code)


    > You can use [`IPython.display.clear_output`](http://ipython.org/ipython-doc/dev/api/generated/IPython.display.html#IPython.display.clear_output) to clear the output of a cell.
    > 
    > ```python
    > from IPython.display import clear_output
    > 
    > for i in range(10):
    >     clear_output()
    >     print("Hello World!")
    > ```
    > 
    > ---
    > 
    > Using the `clear_output(wait=True)` will generally make the result nicer if you have `clear_output` inside a loop. -- [Toke Faurby](https://stackoverflow.com/users/3747801/toke-faurby "1,356 reputation") [Jun 8 '17 at 23:49](https://stackoverflow.com/questions/24816237/ipython-notebook-clear-cell-output-in-code#comment75891759_24818304)
    > 
