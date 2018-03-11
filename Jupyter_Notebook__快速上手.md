# Jupyter_Notebook__快速上手

<!-- toc --> 
[toc]


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






