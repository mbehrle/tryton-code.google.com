#summary How to translate Tryton.
#labels Phase-Implementation,Phase-Support,Phase-QA,Featured


# How to translate Modules #

This describes the internals of the translation process.

The translation community shares the effort on the [Tryton Pootle](http://pootle.tryton.org/).

If your language doesn't exist yet, you can request its creation by opening an issue on the [Tryton bugtracker](http://bugs.tryton.org/).

_Translations patches are merged only during the merge window before a major release._

### Create the language ###

  * You must first create the language in "Administration>Localization>Languages" if it doesn't exist.
> We follow the [RFC 4646](http://tools.ietf.org/html/rfc4646) for the code naming but replace `-` by `_` (it is the POSIX [Locale](http://en.wikipedia.org/wiki/Locale)).
> Here is a [validator](http://schneegans.de/lv/).

### Set the language translatable ###

  * You must check the translatable checkbox of the language to be able to translate it.

### Update installed modules ###

  * You must update the installed modules if you are not working on a new language.
  * You must also install all extras\_depend of the modules you are translating.

### Set translations ###

  * You must update the translations records for the reports and views with the wizard "Administration>Localization>Set Translations".

### Clean translations ###

  * You must clean the translations that are no longer needed with the wizard "Administration>Localization>Clean Translations".

### Synchronize translations for the language ###

  * You must synchronize the translations records for the language with the wizard "Administration>Localization>Synchronize Translations".
> This may take some time depending on the number of modules you have installed.

  * Now you can translate the terms.
> The fuzzy field is checked when the source term have been changed since the last update, so you must verify that the translation is always correct and uncheck the fuzzy field.

> _**Hint:**_
    * _The task can be facilitated by filtering on various fields - module, src, value..._
    * _For a convenient display of multiline items just click on "Form>Switch View". You simply move between the items using "Form>Next" / "Form>Previous"._

### Export translations ###

#### Manual Export ####

  * You must now export the translation with the wizard "Administration>Localization>Export Translations" and save the file in the module directory.
    * Select language and module name to export
    * Click on icon "Save as..." and select module's repository
    * The name of the file must be the language code with the extension ".po" (e.g. de\_DE.po).
    * You must also declare the filename in the ` __tryton__.py ` of the module using the key 'translation' (see for an example in [ir module](http://hg.tryton.org/trytond/file/tip/trytond/ir/__tryton__.py)).

> _**If you edit the file with an editor, limit all lines to a maximum of the 80 characters**_

#### Scripted Export ####

  * You can use the script [localize\_modules.py](http://hg.tryton.org/tryton-tools/file/tip/localize_modules.py) that will put translation for each modules in the right place.

> _**Before updating a module or the whole database, changes should be exported, because otherwise your changes can be overwritten with old values from old po file**._

### Submit translations ###

  * see [HowtoContribute](HowtoContribute.md)

# How to translate Tryton client #

For the client translation we use [Babel](http://babel.edgewall.org/wiki/Documentation/setup.html).

### Change directory ###
  * Change to the `tryton` client directory.

### Prepare po file ###

  * Extract translation strings into the translation template file:
```
python ./setup.py extract_messages --no-location --omit-header
```
  * Update the translation file with the generated translation template:
```
python ./setup.py update_catalog --ignore-obsolete=true -l de_DE
```

### Edit po file ###

  * Translate the missing and fuzzy terms in the translation file (`share/locale/de_DE/LC_MESSAGES/tryton.po`) with your favorite editor (example: [poedit](http://www.poedit.net/)).
  * Remove unused terms.

> _**Limit all lines to a maximum of the 80 characters**_

### Generate mo file ###

```
python ./setup.py compile_catalog --locale de_DE
```

> _**Hint:**_
> if you are using poedit, this is already done automatically

### tryton.desktop ###

  * Create a line for `GenericName[de]`
  * Create a line for `Comment[de]`

### Create nsh file ###

  * Copy `english.nsh` into `german.nsh`
  * Set proper encoding for new `*.nsh` file (It must not be UTF8)
  * Translate the file

### Submit translations ###

  * see [HowtoContribute](HowtoContribute.md)

# How to translate Documentation #

**Not yet supported**

For the documentation translation we use [translate-toolkit](http://translate.sourceforge.net/wiki/toolkit/index)

### Change directory ###

  * Change to the `doc` directory of the repository.

### Prepare po files ###

  * For each rst file extract translation strings into translation template file:

```
txt2po index.rst index.pot -P
```

  * Update the translation files with the generated translation templates:

```
pot2po index.pot de_DE/index.po -t de_DE/index.po
```

### Edit po files ###

  * Translate the missing and fuzzy terms in each translation files (`de_DE/index.po`) with your favorite editor.

### Generate rst files ###

```
po2txt de_DE/index.po de_DE/index.rst -t index.rst
```

> _**Never edit directly the `*.rst` files**_

### Edit nsh file ###

  * Copy the file `english.nsh` into `german.nsh`
  * Translate the strings
  * Add the new language in `setup.nsi` and `setup-single.nsi` under the `;Languages` section

### Submit translations ###

  * the files to submit are `*.pot`, `de_DE/*.po`, `de_DE/*.rst`, `german.nsh`, `setup.nsi` and `setup-single.nsi`
  * see [HowtoContribute](HowtoContribute.md)