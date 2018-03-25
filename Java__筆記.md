# Java__筆記

## Java applet

- [Running legacy Java applets without a browser or security exceptions (Windows)：sysadmin](https://www.reddit.com/r/sysadmin/comments/69m2ol/running_legacy_java_applets_without_a_browser_or/)

    > I recently worked on this problem on behalf of a classroom instructor that utilizes these really well-made Java applet-based simulations by NASA:
    > 
    > [https://wright.nasa.gov/airplane/shortw.html](https://wright.nasa.gov/airplane/shortw.html)
    > 
    > The ones marked 'interactive' are the applets!
    > 
    > Up until now we were able to add the specific URLs to the Exception Site List and they'd begrudgingly run in Chrome and Firefox (after clicking "allow" a lot); with the latest updates to both, this is no longer the case. I didn't want to deploy an outdated fixed-version legacy browser just for the sake of one application, and the simulations are useful enough to justify the time invested, so suggesting to "find something else" seemed inappropriate in this scenario.
    > 
    > I learned about an application called "appletviewer", which is included in the [JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) for development purposes and acts as a small standalone browser emulator. You can use it to run applets locally, regardless of OS version (I've tested it in 7, 8 and 10 as well as OS X 10.12).
    > 
    > ---
    > 
    > Local Files
    > -----------
    > 
    > You don't need to install the entire JDK on clients or add the `PATH` variables; instead, copy the `appletviewer.exe` and `jli.dll` from a JDK installation, and deploy them together in the same directory to the destination (I put them in `C:\Java\`). Both of these files are (typically) found in:
    > 
    > ```
    > C:\Program Files\Java\jdk1.(version)\bin
    > ```
    > 
    > Then you save the page containing your Java applet locally and call it via the following method:
    > 
    > ```
    > appletviewer.exe Yourpage.html
    > ```
    > 
    > The result looks like this:
    > 
    > ![https://i.imgur.com/If09Naf.png](https://i.imgur.com/If09Naf.png)
    > 
    > ---
    > 
    > Remote Files
    > ------------
    > 
    > Depending on the server-side permission and file structure, you can also pass an URL to it directly:
    > 
    > ```
    > appletviewer.exe https://www.grc.nasa.gov/WWW/K-12/airplane/foil3.html
    > ```
    > 
    > This will not work for every site, but it removes the step of deploying applet files to clients. Naturally, if the site becomes unavailable for any reason, you will no longer be able to use the content (which is why I set it up as a local copy instead).
    > 
    > ---
    > 
    > Launcher
    > --------
    > 
    > For a single applet, you can just use a batch script to call appletviewer and the target path. I made a little Python program that lets you invoke a list of applets, which is handy if you have quite a few of them.
    > 
    > Source code is here (it uses [easygui](https://pypi.python.org/pypi/easygui) because I'm terribly lazy):
    > 
    > [https://gist.github.com/Kibbles/3016367843a166faaa44443abd9ac354](https://gist.github.com/Kibbles/3016367843a166faaa44443abd9ac354)
    > 
    > Screenshot of the launcher:
    > 
    > ![https://i.imgur.com/lT2OjUJ.jpg](https://i.imgur.com/lT2OjUJ.jpg)
    > 

- [Run Java-applets directly ( without html page ) - Stack Overflow](https://stackoverflow.com/questions/3012124/run-java-applets-directly-without-html-page)

    > Use below code with your code, where AppletClass is your Applet class.
    > 
    > ```
    > AppletClass appletClass = new AppletClass ();
    > 
    > JFrame frame = new JFrame();
    > frame.setLayout(new GridLayout(1, 1));
    > frame.add(appletClass );
    > 
    > // Set frame size and other properties
    > ...
    > 
    > // Call applet methods
    > appletClass .init();
    > appletClass .start();
    > 
    > frame.setVisible(true);
    > ```
    > 
    > More customizations can be done as required.

    > Appletviewer is the way to go, BUT, **it still requires a webpage with an applet-tag**.
    > 
    > An alternative solution is to write a stub class, with a main method, that instantiates the applet, calls `init()`, `start()`, `stop()` and `destroy()` as would otherwise have been done by the browser or appletviewer.

- [Build and run Java applets without browser (appletviewer) - Study Korner](https://www.studykorner.org/build-run-java-applets-without-browser-appletviewer/)

    [Java-Applet.pptx](https://drive.google.com/file/d/1ROUCiIZZ6UYCPgkuKFb7Op1vHMXt_5j9/view?usp=sharing)

    > Applet are executed in two ways
    > 
    > 1. Web browser- Applet tag is included in HTML file
    > 
    > 2. Applet Viewer- applet tag is included in Java source file itself.
    > 
    > ```htmlmixed
    > <APPLET code = “class file name”
    > 
    >   height= maximum height of applet in pixels
    > 
    >   width = maximum width of applet in pixels>
    > 
    > </APPLET>
    > ```

