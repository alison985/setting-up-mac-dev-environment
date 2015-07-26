# How To Setup a Mac Development Environment (from scratch)

Everytime I get a new computer I have this problem. Here's my documentation.

## Table of Contents
* [Assumptions](#assumptions)
* [Basic Configuration](#basic-configuration)
* [Package Managers](#package-managers)
  * [Default Sublime Packages](#default-sublime-packages)
* [Python Specific Environment](#python-specific-environment)
  * [Virtual Environment](#virtual-environment)
  * [Python Sublime Packages](#python-sublime-packages)
  * [Python Libraries](#python-libraries)
  * [Python Web Frameworks](#python-web-frameworks)
    * [Flask](#flask)
    * [Django](#django)
* [Ruby Specific Environment](#ruby-specific-environment)
  * [Gems](#gems)
  * [Ruby Web Frameworks](#ruby-web-frameworks)
    * [Rails](#rails)
* [Local Databases](#local-databases)
  * [mySQL](#mysql)
  * [PostgreSQL](#postgresql)
* [Other Helpful Tools](#other-helpful-tools)

## Assumptions

* Mac OS X 10.10.4
* Sublime Text 2 (3 isn't stable yet)
* You're logged in as an administrative user of the computer.
* You want Python 2.7.x

## Basic Configuration

[Source](http://hackercodex.com/guide/mac-osx-mavericks-10.9-configuration/)

* Unhide Library Folder
  * Open Finder.
  * Press `shift-command-H` and then `command-J`, which will bring up a window that configures Finder view options.
  * Check the “Show Library Folder” and close the window.

* Bash Profile Setup
  * `vim ~/.bash_profile`

```bash
# Finder: show hiddeh files
defaults write com.apple.finder AppleShowAllFiles TRUE

# Always use colour output for ls.
[[ "$OSTYPE" =~ ^darwin ]] && alias ls='command ls -G' || alias ls='command ls --color';

######ALIASES###############
alias subl='open -a "Sublime Text 2"'
alias reload='source ~/.bash_profile'

######EXPORT#############
export EDITOR=subl
# Setting PATH for Python 3.4
# The orginal version is saved in .bash_profile.pysave
PATH="/Library/Frameworks/Python.framework/Versions/3.4/bin:${PATH}"
export PATH=$PATH:/Applications/Postgres.app/Contents/Versions/9.4/bin
# Ignore duplicate commands in the history
export HISTCONTROL=ignoredups
# Increase the maximum number of lines contained in the history file
# (default is 500)
export HISTFILESIZE=10000
# Increase the maximum number of commands to remember
# (default is 500)
export HISTSIZE=10000
# Make new shells get the history lines from all previous
# shells instead of the default "last window closed" history
export PROMPT_COMMAND="history -a; $PROMPT_COMMAND"
# Append to the Bash history file, rather than overwriting it
shopt -s histappend;
```

  * `source ~/.bash_profile`

* Get the XCode pieces you need
  * `xcode-select --install`
  * Will prompt for full version of Xcode or just command line tools

[Back to TOC](#table-of-contents)

## Package Managers

* [Homebrew](http://brew.sh/)

   ```ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"```
* [PIP](https://pip.pypa.io/en/latest/installing.html)

   ```sudo easy_install pip```
* [Sublime Text 2 Package Control](https://packagecontrol.io/installation#st2) `View > Show Console`

   ```bash
import urllib2,os,hashlib; h = 'eb2297e1a458f27d836c04bb0cbaf282' + 'd0e7a3098092775ccb37ca9d6b2e4b7d'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler()) ); by = urllib2.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); open( os.path.join( ipp, pf), 'wb' ).write(by) if dh == h else None; print('Error validating download (got %s instead of %s), please try manual install' % (dh, h) if dh != h else 'Please restart Sublime Text to finish installation')
```

### Default Sublime Packages

* [Markdown Preview](https://packagecontrol.io/packages/Markdown%20Preview)
* [Color Highlighter](https://packagecontrol.io/packages/Color%20Highlighter)

[Back to TOC](#table-of-contents)

## Python Specific Environment

### Virtual Environment

*
```bash
pip install virtualenv
pip install virtualenvwrapper`
export WORKON_HOME=~/Envs
source /usr/local/bin/virtualenvwrapper.sh
```
* Close Terminal and Re-open Terminal.
* `cd` to your directory
* `mkvirtualenv venv`
* `workon venv`

### Python Sublime Packages

* [Jedi - python autocompletion](https://packagecontrol.io/packages/Jedi%20-%20Python%20autocompletion)

### Python Libraries

* pandas
* psycopg2
* See Also [Awesome-Python](https://github.com/vinta/awesome-python)

### Python Web Frameworks

#### Flask

* Flask 
  * `pip install Flask`
  * [Flask Homepage](http://flask.pocoo.org/)
* Flask-bootstrap
  * `pip install flask-bootstrap`
  * [Flask-Bootstrap Homepage](http://pythonhosted.org/Flask-Bootstrap/)

#### Django

* `pip install django`
* Sublime Plugins
  * [Djaneiro](https://packagecontrol.io/packages/Djaneiro)
* Django Plugins
  * [Django Bootstrap 3](https://github.com/dyve/django-bootstrap3)
* [Official First Django App Tutorial](https://docs.djangoproject.com/en/1.8/intro/tutorial01/)

[Back to TOC](#table-of-contents)

## Ruby Specific Environment

### Ruby Version Manager (RVM)

* Install
  * `gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3`
  * `\curl -sSL https://get.rvm.io | bash -s stable`
* [RVM](https://rvm.io/)

### Gems

* Postgresql = `gem install pg`
* [Other Gems listed by Category](https://www.ruby-toolbox.com/categories)

### Ruby Web Frameworks

#### Rails

* `gem install rails`
* [Official Getting Started Guide](http://guides.rubyonrails.org/getting_started.html)

[Back to TOC](#table-of-contents)

## Local Databases

### mySQL

### Postgresql

* [Postgres.app](http://postgresapp.com/)
* Sublime Plugin
  * [PostgreSQL Syntax Highlighting](https://packagecontrol.io/packages/PostgreSQL%20Syntax%20Highlighting)

[Back to TOC](#table-of-contents)

## Other Helpful Tools

* [Dash](https://kapeli.com/dash)
* [Github for Mac](https://mac.github.com/)
* [Google Chrome](https://www.google.com/intl/en/chrome/browser/)
* [Mozilla Firefox](https://www.mozilla.org/en-US/firefox/desktop/)

[Back to TOC](#table-of-contents)
