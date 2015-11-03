

<font color='darkred' size='larger'>This page is intended for those who want to build Mac OS X installer packages. For those of you who just want to <i>use</i> Tryton, simply follow the instructions for <a href='InstallationMacOSX.md'>installing Tryton on Mac OS X</a>.</font> (Note: At this time, instructions are only provided for packaging the Mac OS X client.)

# Building a Mac OS X Client Application Bundle #
## Preparing the gtk-osx Environment ##
(NB: At this time, these instructions will create an i386 <b>only</b> client that will run on Mac OS X 10.5 (Leopard) and later.)

  1. Validate that gcc-4.0 and the 10.5 sdk are present
```
/usr/bin/gcc-4.0 -v
ls -ld /Developer/SDKs/MacOSX10.5.sdk
```
  1. Install git
```
curl -O http://git-osx-installer.googlecode.com/files/git-1.7.2.3-intel-leopard.dmg
open git-1.7.2.3-intel-leopard.dmg
sudo installer -pkg /Volumes/Git\ 1.7.2.3\ Intel\ Leopard/git-1.7.2.3-intel-leopard.pkg -target /
hdiutil eject "/Volumes/Git 1.7.2.3 Intel Leopard"
```
  1. Create a user just for this build, become that user, and prepare the environment
```
sudo su - gtkosxbuilder
cat << EOF > ~/.profile
export PATH=~/.local/bin:~/gtk/inst/bin:/bin:/usr/bin:/sbin:/usr/sbin:/usr/local/git/bin
export DYLD_FALLBACK_LIBRARY_PATH=~/gtk/inst/lib
EOF
. ~/.profile
```
  1. Download and run the gtk-osx build setup script
```
curl -L -O http://downloads.sourceforge.net/sourceforge/gtk-osx/gtk-osx-build-setup.sh
sh gtk-osx-build-setup.sh
```
  1. Modify .jhbuildrc-custom
```
sed -i -e 's/^setup_sdk/#setup_sdk/g' .jhbuildrc-custom
cat << EOF >> .jhbuildrc-custom
_gtk_osx_use_jhbuild_python = True
branches["python"] = "http://www.python.org/ftp/python/2.6.4/Python-2.6.4.tar.bz2"
setup_sdk(target="10.5", sdk_version="10.5", architectures=["i386"])
os.environ["CC"] = "/usr/bin/gcc-4.0"
os.environ["DYLD_LIBRARY_PATH"] = ""
build_policy = "updated-deps"
modules = [ "meta-gtk-osx-bootstrap", "meta-gtk-osx-core", "meta-gtk-osx-python", "librsvg", "meta-gtk-osx-themes", "gtk-quartz-engine" ]
EOF
```
  1. Build (This may take 30 minutes)
```
jhbuild bootstrap --ignore-system && jhbuild build
```
  1. Install mercurial, and satisfy the tryton client dependencies
```
mkdir -p tmp
cd ~/tmp
curl -O http://pypi.python.org/packages/source/s/setuptools/setuptools-0.6c11.tar.gz
tar zxvf setuptools-0.6c11.tar.gz
cd setuptools-0.6c11
python ./setup.py install
easy_install mercurial python-dateutil py2app
```
## Running the Client ##
  1. Checkout Tryton client source
```
cd ~
hg clone http://hg.tryton.org/tryton
```
> > Please see [HowtoContribute](HowtoContribute.md) for a more thorough introduction to the use of mercurial within the Tryton project.
  1. Execute using the gtk-osx built python interpreter
```
~gtkosxbuilder/gtk/inst/bin/python path/to/tryton/client
```
## Packaging the Client ##
  1. Once again, become the gtkosxbuilder user, and invoke py2app within the source tree.  Take care to ensure the path is writable by this user.
```
sudo su - gtkosxbuilder
cd path/to/tryton/client
python ./setup.py py2app
```
  1. The application bundle is built, then packaged along with other various distribution files and added to tryton-x.y.z.dmg, which is located at the top level of the source tree.