

# TL;DR / Quick Start #

Make sure to install the [root CACert](http://wiki.cacert.org/FAQ/ImportRootCert). Optionally, add this to your hg configuration file (~/.hgrc):

```
[hostfingerprints]
hg.tryton.org = 55:aa:20:09:ac:42:0d:aa:e1:b8:78:dd:a4:8e:82:96:62:af:61:65
```

Then, clone the repository

```
hg clone https://hg.tryton.org/trytond
cd trytond
vi ...
curl -o ~/.local/bin/upload.py https://codereview.tryton.org/static/upload.py
python ~/.local/bin/upload.py --oauth2
```

# Easy Issues #

In order to ease the introduction of newcomers to the project
development there is a list of easy issues on the issue tracker. You can find them using the [Show easy](https://bugs.tryton.org/issue?status=-1,1,2,3,4,5,6,7&@sort=-activity&@search_text=&@columns=id,activity,title,creator,status&@dispname=Show%20Easy&keyword=27&@group=priority&@filter=status,keyword&@pagesize=50&@startwith=0) button on the [issue tracker (Roundup)](https://bugs.tryton.org/)

# Introduction #

  1. Check if the issue has not already been [reported](https://bugs.tryton.org/).
  1. Get the code:
    * Tryton GTK client: `hg clone https://hg.tryton.org/tryton`
    * Tryton server: `hg clone https://hg.tryton.org/trytond`
    * Tryton server with all modules: `hg nclone https://hg.tryton.org/trytond` ([mercurial extension hgnested needed](https://pypi.python.org/pypi/hgnested/))
    * Tryton web client: `hg clone https://hg.tryton.org/sandbox/sao/`
    * or you could use a [Git mirror](https://github.com/tryton/)
  1. If the fix isn't trivial, create an [issue](https://bugs.tryton.org/), it could be useful to discuss it before coding.
  1. Check the [Coding Guidelines](CodingGuidelines.md), make the patch and test.
  1. Submit your patch to the [codereview](http://codereview.tryton.org/) using [upload.py](http://codereview.tryton.org/static/upload.py) or [mercurial extension hgreview](https://pypi.python.org/pypi/hgreview). The title of the review must be prefixed with the name of the repository (`tryton`, `trytond` or the module name).
  1. The commit message will be the review subject (with module name) and the review description. The review description must contains a reference to the issue (`issue1234`). The reference of the review (eg `review10004567`) will be automatically added to the commit message.
  1. Modify your patch according to the comments until a core developer puts a `LGTM` (it means _looks good to me_) comment.
  1. The patch will be committed and pushed by a core developer.
  1. Once done, a comment with the mercurial changeset will automatically be added to the review. Then you must close the review: use the link `Edit issue`, then check `Closed` and validate with the `Update Issue` button.

## Contributions ##

### Requirements ###

Your contribution should meet the following requirements ([according to the Vote results performed on 2010-07-05](http://article.gmane.org/gmane.comp.python.tryton/1641)):

#### Must ####
  * All contributions must be licensed under the same license as the existing code, which is the [GNU General Public License, version 3](http://www.gnu.org/licenses/gpl-3.0.html)
  * The contributor email must be a valid email address
  * The domain of the contributor email must not contain tryton
  * The username of a mercurial patch must be in the form: `Name <email>`

#### Nice to have, but not required ####
  * The contributor name should be the real name of the natural person who submits the code
  * The contributor email should be linked to only one contributor name

### Rules ###
If the contributor has a significant amount of code, he can add himself to the `COPYRIGHT` file.

Core developers are people which have SSH access to the repositories. They are allowed to push small fixes without `LGTM`. Bigger fixes need approval an (`LGTM`) comment of another core developer. `LGTM` means _Looks Good To Me_, acronym is used while reviewing patches ([example](http://codereview.tryton.org/6451002/)). Core developers are flagged as committer in their profile ([example](https://bugs.tryton.org/user12)) and they can be distinguished on the bugtracker by their small Tryton logo ([example](https://bugs.tryton.org/issue4392)).

For bigger fixes, in case of disagreement, a consensus should be reached. At last the [project leader (Cédric)](ProjectOrganization#Organization.md) takes a decision.

Approved contributions are pushed by the core developers.

## Testing/Bugtracking ##
  * Test your issue on the latest development version.
  * Create an issue in our [issue tracker (Roundup)](https://bugs.tryton.org/).
  * Set the affected components on the issue.
  * Assign the issue to you (your username on Roundup) with a comment that you are working on it and you will provide a fix.

## Submitting a code review ##

  * Check the [Coding Guidelines](CodingGuidelines.md).
  * Don't create codereview related to new feature during feature freeze (See [ReleaseGeneral#Major\_release\_preparation](ReleaseGeneral#Major_release_preparation.md)).
  * Submit your patch to [Rietveld](https://codereview.tryton.org/) (with the module name in front of the title).
  * The commit message will be the review subject (with module name) and the review description. The review description must contain a reference to the issue (`issue1234`). The reference of the review (eg `review10004567`) will be automatically added to the commit message.
  * Close the codereview once your patch is applied: use the link `Edit issue`, then check `Closed` and validate with the `Update Issue` button.

There are two options for uploading and working with Rietveld:

### upload.py ###

One is using [upload.py](https://codereview.tryton.org/static/upload.py) (see the [Help](http://code.google.com/p/rietveld/wiki/CodeReviewHelp)).

### hgreview ###

The other and recommended one is using [hgreview](https://bitbucket.org/nicoe/hgreview). Which simplifies, not only patch uploading but also testing.

To install it use:

```
pip install hgreview
```

Then you should enable the extension either in your ~/.hgrc or the repository-specific .hgrc:

```
[extensions]
hgreview =

[review]
server = https://codereview.tryton.org
oauth2 = true
send_email = True
```

Then you can upload your patch (do not commit before upload):

```
hg review -m "repository_name: Improve things a lot"
```

_For non-trunk fixes append the series number to repository name._

You can get the issue ID:

```
hg review --id
```

In order to test this patch (or another one) you can simply get latest version from within the repository:

```
hg review --fetch -i <issue id>
```

## Committing a validated patch ##

Once your review validated by a `LGTM` comment of a core developer, your contribution will be commited and pushed, you don't need to do anything else.

## Pushing your commit ##

The patch will be committed and pushed by a commiter or a core developer. As said above: the commit message will be the review subject (with module name) and the review description. The review description must contains a reference to the issue.

## Back port ##

The patch will be back ported to older series by the maintainer on his own discretion after 1 week in the development branch. The decision is based on the importance of the bug, the availability of workaround and the feasibilities.

Those rules don't apply for security bugs which are applied at once on all affected series followed a release.

# Instructions for committers #

See [Mercurial#Usage](Mercurial#Usage.md) for details.