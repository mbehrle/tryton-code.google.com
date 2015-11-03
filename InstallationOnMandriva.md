#summary Installation hints for the Mandriva distribution (aka Mandrake)
#labels Phase-Deploy

# Introduction #

This page contains some additional installation hints for installing on a Mandriva based system.

For installing the packages, simply open a console window with administration rights (a so called "root console") and paste the lines below into the console.

`urpmi` is the command-line version of the software installation center (also known as rpmdrake). Pasting  the lines into a window is much easier than selecting the packages via the GUI :-) plus for the server you need additional Python packages which are not available via the software installation center. For more information please visit http://wiki.mandriva.com/en/Tools/urpmi

# For the Client #

  * Mandriva Linux 2008.1, 2009.0, 2009.1:
```
urpmi python-egenix-mx-base pygtk2.0 librsvg python-pytz
```
> > N.B.: Python is build with SSL support, thus an extra pyOpenSSL package is not required.
    * _Recommended_: OpenOffice, KOffice or another [OpenDocument viewer](http://en.wikipedia.org/wiki/OpenDocument_software) for displaying reports.
    * _Recommended_: xpdf, kpdf, epdfview or another [PDF viewer](http://en.wikipedia.org/wiki/List_of_PDF_software) if you convert reports into PDF.


# For the Server #

  * Mandriva Linux 2009.0, 2009.1:
```
urpmi python-psycopg2 python-egenix-mx-base python-lxml python-genshi python-yaml
# needed for installing additional modules from PyPI
urpmi python-setuptools
easy_install -U relatorio pycha # may take a while (NB: pycha, not PyChart)

# optional dependencies
urpmi python-dot python-pytz python-beautifulsoup python-vobject
urpmi openoffice.org-writer openoffice.org-pyuno
easy_install -U pywebdav openoffice-python vatnumber
```

  * Mandriva Linux 2008.1:
```
urpmi python-psycopg2 python-egenix-mx-base python-lxml python-pytz
# needed for installing additional modules from PyPI
urpmi python-setuptools
# Mandrivas Genshi and lxml are to old
urpmi libxslt-devel
easy_install -U Genshi lxml relatorio # may take a while

# optional dependencies (list based on Tytron 1.0)
urpmi openoffice.org-writer
easy_install pywebdav openoffice-python pydot
```

# Database installation #

  * Mandriva Linux 2008.1, 2009.0, 2009.1
```
urpmi postgresql8.3-server  # postgresql8.2-server is okay, too
```

Please refer to the appropriate [documentation](http://www.postgresql.org/docs/) for more information about how to set up PostgreSQL once you installed the package.