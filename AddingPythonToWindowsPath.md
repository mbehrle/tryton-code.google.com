#summary How to add python.exe to Windows PATH

You may also want to read this summary: http://groups.google.com/group/comp.lang.python/msg/37fcd0676039bc24

# Method 1: Add via Control Panel #

Well you can do by selecting 'System' from the Control Panel,
selecting the 'Advanced' tab, the 'Environment Variables'
button and then finding the PATH (user or system) and editing
it in the agonisingly small edit control which doesn't seem
to have changed since Windows 3.1. (He says, exaggerating only
a little)...

Source: http://groups.google.com/group/comp.lang.python/msg/dea9f45e03406828

# Method 2: Add via a Python script #

... or, I was going to say, you could run Christian Heimes'
win\_add2path.py script which is in c:\python26\lib\tools.
Except that it wasn't added until python26 and uses
`_winreg.ExpandEnvironmentStrings` which also wasn't added
until then. (I think). But for anyone else still watching
the show...

Source: http://groups.google.com/group/comp.lang.python/msg/dea9f45e03406828

# Method 3: using a small .bat file #

Source: http://groups.google.com/group/comp.lang.python/msg/5656baf6e811ccb0

I highly recommend against adding C:\Python25 to your %PATH%. You can
get the same effect by adding a simple bat file to C:\Windows\System32

```
@C:\Python25\python.exe %*
```

Call it python25.bat and you are done. Apropos call, don't forget to
"call python25" in batch files. :)

...

My way doesn't add the dlls to the search path. It allows you to have
multiple python commands at once, too. I have shortcuts for python24,
python25 and python26 on my Windows box.