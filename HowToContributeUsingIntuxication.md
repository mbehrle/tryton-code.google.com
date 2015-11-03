#summary How To Publish your own repositories using Intuxication
#labels Phase-Implementation,Deprecated

# Introduction #

You are ready to start contributing your own modules to submit to tryton and want to make it easier to get them into trunk.

Go to [Intuxication](http://mercurial.intuxication.org) create your account and then init your repo.  Create as many repos as needed, remember to let your user have access to it.

## Helping in Translation ##

see HowtoTranslate


## Providing patches for repositories on tryton.org with an own repository ##

If you want to provide patches by way of an own repository hosted on intuxication.org, you can import an existing repository into you own like described on http://mercurial.intuxication.org/dev/wiki/FAQ

Example for module account:

The .hg/hgrc of your repos should read something like
```
[paths]
default = http://hg.tryton.org/modules/account
```

Make it look like

```
[paths]
default = http://hg.tryton.org/modules/account
myown = http://mercurial.intuxication.org/hg/account_myown

[ui]
username = Your Name <your@e.mail>
```
This way we let mercurial know we have a repo at intuxication named **myown** (change to suit your needs, and obviously replace **account** and **account\_myown** and your username accordingly).

Now you are ready for the updating cycle. Remember that we are working with a Distributed Version System, so you have now three repos(tryton, your own, intuxication). You'll get changes from tryton (upstream), You'll push those changes to intuxication, and your local changes will be commited to your local repo and then pushed to intuxication, finally the changes commited to intuxication will go to upstream and to your local repo, if they are approved ;)

### Updating your repo from upstream ###
```
hg pull
hg update
```

### Commiting your changes to your local repo ###
Remember to test everything you do **before** commiting, add files if needed.
```
hg commit -m "Here comes some patch"
```

### Pushing the changes to intuxication ###
```
hg push myown
```
Remember to change **myown** to whatever identifier you have used on your .hg/hgrc.

### Informing upstream of your commit ###
Fill a [bug](http://bugs.tryton.org) and with it let the maintainers and #tryton know about the new changeset.