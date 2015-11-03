#summary General facts for a Tryton release
#labels Phase-Requirements,Phase-Deploy


# Introduction #

The Tryton Release process is inspired by the [OpenBSD](http://www.openbsd.org/) Release Process. To get a conception of the process please have a look at a video of [The OpenBSD Release Process at AsiaBSDCon 2009](http://www.youtube.com/watch?v=i7pkyDUX5uM)
The next release date is chosen after a release and published at [Tryton's calendar](http://www.tryton.org/community/calendar.html)

# What is released? #

  * Every part of Tryton, the user needs to install and run the complete application.
  * Development and build-for-release specific parts are not released, they are always current in the development tree.

# Maintenance #

Major releases are maintained for at least 2.5 years which means there will be minor releases for this series during this period.

# Version number of Tryton releases #

The Tryton version number is made of thee parts like the following example:
```
Tryton Version 2.3.5
```

## Major release ##
The first and second number are major version numbers.
These general version numbers ...
  * ... are used to indicate a major step in the evolution of Tryton;
  * ... are published twice per year;
  * ... can change parts of the database structure;
  * ... could need manual steps for database upgrade;

## Minor release ##
The third number is the minor version number of Tryton.
Releases changing this number...
  * ... are published to fix bugs;
  * ... don't change the database structure;
  * ... don't need a database upgrade;
  * ... are considered as unproblematic for update;

## Development state ##
The second number indicates development state:
  * even number and null: Release version
  * odd number: Development version

# Major release preparation #
The development is frozen about 1 month before the scheduled date.
> "freezing" is handled by maintainers discipline.

During freezing:
  * Leaders check their modules (and documentation) and fix reported issues.
  * Translation teams update the translation of each repositories.
  * Everybody test and report issues until release.
  * The reviews related to new features are not reviewed and should not be created.

# Release process #

We use the scripts from https://hg.tryton.org/tryton-tools/ from within the repository to release.

It just requires to have the environment variable ```TRYTON_GPG_KEY```.

## Major release ##

```
# do_major_release
```

## Minor release ##

```
# do_minor_release
```