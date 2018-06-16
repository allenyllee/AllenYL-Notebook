# Firefox__筆記

## Enable WebGL

- [1365492 – Firefox refuses to use my nvidia GPU, it uses the intel integrated GPU instead](https://bugzilla.mozilla.org/show_bug.cgi?format=default&id=1365492)

    Just so that we're on the same page, I'm assuming you're in Nvidia control panel, and in the Manage 3D Settings->Program settings, you find Mozilla Firefox (firefox.exe) and set the preferred graphics processor to High-performance Nvidia processor.


- [How can I enable WebGL in my browser? - Super User](https://superuser.com/questions/836832/how-can-i-enable-webgl-in-my-browser)

    > Firefox
    > 
    > First, enable WebGL:
    > 
    >     Go to about:config
    >     Search for webgl.disabled
    >     Ensure that its value is false (any changes take effect immediately without relaunching Firefox)
    > 
    > Then inspect the status of WebGL:
    > 
    >     Go to about:support
    >     Inspect the WebGL Renderer row in the Graphics table:
    >         If the status contains a graphics card manufacturer, model and driver (eg: "NVIDIA Corporation -- NVIDIA GeForce GT 650M OpenGL Engine"), then WebGL is enabled.
    >         If the status is something like "Blocked for your graphics card because of unresolved driver issues" or "Blocked for your graphics driver version", then your graphics card/driver is blacklisted.
    > 
    > If your graphics card/drivers are blacklisted, you can override the blacklist. Warning: this is not recommended! (see blacklists note below). To override the blacklist:
    > 
    >     Go to about:config
    >     Search for webgl.force-enabled
    >     Set it to true
    > 
    > (Like Chrome, Firefox has a Use hardware acceleration when available checkbox, in Preferences > Advanced > General > Browsing. However, unlike Chrome, Firefox does not require this checkbox to be checked for WebGL to work.)
    > 


## Disable content security policy

- [javascript - How to override content security policy while including script in browser JS console? - Stack Overflow](https://stackoverflow.com/questions/27323631/how-to-override-content-security-policy-while-including-script-in-browser-js-con)

    > You can turn off the CSP for your entire browser in Firefox by disabling security.csp.enable in the about:config menu.
    > 
