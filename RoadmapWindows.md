#summary Roadmap for better integration with Windows
#labels Deprecated

# Roadmap for better integration with Windows #

## Objectives ##

  * Ease installation of the Tryton-Server for Windows users (client is already okay.)
  * Ease setting up a deployment environment. This should allow Windows users to bundle Tryton tailored to their environment using one of the stable releases.
  * Ease setting up a development environment. This is quite like for the deployment environment, but uses the in-development branch and checks out from Mercurial.

## Milestones ##

  * Create scripts for downloading all requirements
  * Enable building an installer package for the server (based on whatever is currently installed)
  * Convince b2ck to officially release this server package for each release
  * Implement some Control-Panel like the one at [XAMMP](http://www.apachefriends.org/en/xampp-windows.html)
    * Start and stop the server
    * Edit server configuration, esp. passwords
  * Improve download scripts to handle different cases (e.g. deploy, develop, fetch Mercurial, etc.)
  * Improve setup.py to allow some more build-options:
    * path to GTK installation
    * include GTK runtime installer instead of bundling gtk libraries
    * adjust py2exe "bundle" value for different cases
  * Maybe: Move configuration into the registry
  * Think about building a GUI (using tk) for the download scripts. Welcome to luxury :-)