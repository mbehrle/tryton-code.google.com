# Mercurial #

## Configuration ##

The username must be set in [Mercurial configuration](http://www.selenic.com/mercurial/hgrc.5.html) like this:

```
 [ui]
 username = Firstname Lastname <user@example.com>
```

The contributor email must be a valid email address. The domain of the contributor email must not contain "tryton".

## Usage ##

### Fetch the code ###

Clone the repository or update (`hg pull ; hg update`) an existing copy
```
hg clone ssh://hg@hg.tryton.org/trytond
```
Use the right repository (replace `trytond` by `tryton` or `modules/<name>` as needed).

Use one of the ssh keys defined in your [roundup](https://bugs.tryton.org)'s details.

### Fix ###

Change the files to fix the issue.

### Commit ###

Commit the fix into your local repository with an explicit message:
For well formed and informative comments please have a look at [Writing good changeset comments](http://www.selenic.com/mercurial/wiki/ChangeSetComments)
```
  hg commit
```

Comment format:
```
Short comment

Long description
on multi-lines.

issue1234
review1234
```

### Check ###

Use `hg outgoing` command and check the changes.

Find out the revisions created.
```
  hg log
```

### Push ###

Use: `hg push`

**Use `rebase` instead of `merge`**

Sometimes, when we try to push we got a failure because we create a new head on the server. It happens generally because we forgot to update the repository before committing.

Merge doesn't generate a good history so we rebase the changeset we just did on top of the head:
```
hg rebase -r <my new changeset>
```

## Tips ##

Here are few tips to speed-up usage of the mercurial repositories:

  * Clone using `--uncompressed` option:
```
hg clone --uncompressed http://hg.tryton.org/trytond
```
  * Use a local mirror:
> Keep a local clean repository that you update daily and work on local clone of this repository. You will update only once from the internet, others update will be local and fast. Using local clone doesn't waste space because it uses hard-link and is very fast.