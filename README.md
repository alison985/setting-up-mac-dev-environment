# How To Setup a Mac Development Environment (from scratch)

Everytime I get a new computer I have this problem. Here's my documentation.

## Table of Contents
* [Package Managers](#package-managers)
* [Python Specific Environment](#python-specific-environment)
  * [Python Sublime Packages](#python-sublime-packages)
  * [Python Libraries](#python-libraries)
  * [Python Web Frameworks](#python-web-frameworks)
    * [Flask](#flask)
    * [Django](#django)
* [Ruby Specific Environment](#ruby-specific-environment)
  * [Ruby Sublime Packages](#ruby-sublime-packages)
  * [Gems](#gems)
  * [Ruby Web Frameworks](#ruby-web-frameworks)
    * [Rails](#rails)
* [Local Databases](#local-databases)
  * [mySQL](#mysql)
  * [PostgreSQL](#postgresql)

## Assumptions

* Mac OS X 10.10.4
* Sublime Text 2 (3 isn't stable yet)
* You're logged in as an administrative user of the computer.

## Package Managers

* [Homebrew](http://brew.sh/)

   ```ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"```
* [PIP](https://pip.pypa.io/en/latest/installing.html)

   ```sudo easy_install pip```
* [Sublime Text 2 Package Control](https://packagecontrol.io/installation#st2) `View > Show Console`

   ```bash
import urllib2,os,hashlib; h = 'eb2297e1a458f27d836c04bb0cbaf282' + 'd0e7a3098092775ccb37ca9d6b2e4b7d'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler()) ); by = urllib2.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); open( os.path.join( ipp, pf), 'wb' ).write(by) if dh == h else None; print('Error validating download (got %s instead of %s), please try manual install' % (dh, h) if dh != h else 'Please restart Sublime Text to finish installation')
```

## Python Specific Environment

### Python Sublime Packages

### Python Libraries

### Python Web Frameworks

#### Flask

#### Django

## Ruby Specific Environment

### Ruby Sublime Packages

### Gems

### Ruby Web Frameworks

#### Rails

## Local Databases

### mySQL

### Postgresql

* [Postgres.app](http://postgresapp.com/)

