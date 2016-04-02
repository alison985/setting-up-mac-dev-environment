# How To Setup a Mac Development Environment (from scratch)

Everytime I get a new computer I have this problem. Here's my documentation.

## Table of Contents
* [Assumptions](#assumptions)
* [Basic Configuration](#basic-configuration)
* [Mac OS Configuration](#mac-os)
* [Package Managers](#package-managers)
  * [Default Sublime Packages](#default-sublime-packages)
* [Local Databases](#local-databases)
  * [mySQL](#mysql)
  * [PostgreSQL](#postgresql)
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
* [Other Helpful Tools](#other-helpful-tools)

## Assumptions

* Mac OS X 10.10.4+
* Sublime Text 3
* You're logged in as an administrative user of the computer.
* You want Python 2.7.x

## Basic Configuration

* Start the Xcode download/updates first through the App Store. This takes awhile.
* [Github for Mac](https://mac.github.com/)  [ [Source](http://hackercodex.com/guide/mac-osx-mavericks-10.9-configuration/) ]

* Unhide Library Folder
  * Open Finder.
  * Press `shift-command-H` and then `command-J`, which will bring up a window that configures Finder view options.
  * Check the “Show Library Folder” and close the window.

* Bash Profile Setup
  * `vim ~/.bash_profile`

```bashsi
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

* mergetool/difftool
  * [Kaleidoscope](http://www.kaleidoscopeapp.com/)
  * Other options: 
    * [Diff Tools on Mac OS X Blog Entry](http://www.git-tower.com/blog/diff-tools-mac/) 
    * [Meld](http://meldmerge.org/) through [MacPorts](https://www.macports.org/install.php)

[Back to TOC](#table-of-contents)

## Mac OS Configuration

* Change background of login screen [Lifehacker article](http://lifehacker.com/customize-the-login-screen-on-os-x-yosemite-1683740565)

  If you're running Yosemite, all you need to do is save your desired image as: /Library/Caches/com.apple.desktop.admin.png.

## Package Managers

* [Homebrew](http://brew.sh/)

   ```ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"```
* [PIP](https://pip.pypa.io/en/latest/installing.html)

   ```sudo easy_install pip```
* [Sublime Text 3 Package Control](https://packagecontrol.io/installation) `View > Show Console`

   ```bash
import urllib.request,os,hashlib; h = '2915d1851351e5ee549c20394736b442' + '8bc59f460fa1548d1514676163dafc88'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```

### Default Sublime Packages

* [Markdown Preview](https://packagecontrol.io/packages/Markdown%20Preview)
* [Color Highlighter](https://packagecontrol.io/packages/Color%20Highlighter)
* [PostgreSQL Syntax Highlighting](https://packagecontrol.io/packages/PostgreSQL%20Syntax%20Highlighting)
* [Djaneiro](https://github.com/squ1b3r/Djaneiro)
* [Bracket Highlighter](https://packagecontrol.io/packages/BracketHighlighter)
* [HTML-CSS-JS Prettify](https://packagecontrol.io/packages/HTML-CSS-JS%20Prettify)
* [Pretty JSON](https://packagecontrol.io/packages/Pretty%20JSON)
* [Bootstrap 3 Snippets](https://packagecontrol.io/packages/Bootstrap%203%20Snippets)
* RegReplace
* Sublime Text 3 Only
 * [Sidebar Enhancements](https://packagecontrol.io/packages/SideBarEnhancements)

[Back to TOC](#table-of-contents)

## Local Databases

### mySQL

### Postgresql

* [Postgres.app](http://postgresapp.com/)

[Back to TOC](#table-of-contents)

## Python Specific Environment

### Virtual Environment

```bash
pip install virtualenv
pip install virtualenvwrapper
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
* cookiecutter-flask (Comes with FontAwesome 4)
  * `pip install cookiecutter-flask`
  * `cookiecutter https://github.com/sloria/cookiecutter-flask.git`
  * [cookiecutter-flask homepage](https://github.com/sloria/cookiecutter-flask)

#### Django

* `pip install django`
* Sublime Plugins
  * [Djaneiro](https://packagecontrol.io/packages/Djaneiro)
* Django Plugins
  * [Django Bootstrap 3](https://github.com/dyve/django-bootstrap3)
  * [django-fontawesome](https://pypi.python.org/pypi/django-fontawesome)
* [Official First Django App Tutorial](https://docs.djangoproject.com/en/1.8/intro/tutorial01/)

[Back to TOC](#table-of-contents)

## Ruby Specific Environment

### Ruby Version Manager (RVM)

* You may need to `brew install gnupg gnupg2` first so the gpg key can be installed.
* To solve the errors from this: 
  * `sudo chown -R $(whoami) /usr/local/lib`
  * `brew link libgpg-error`
  * `brew link libassuan`
  * `brew link libgcrypt`
  * `brew link libksba`
  * `brew link libusb`
  * `brew link libusb-compat`
  * `brew link pth`
* `brew doctor` can be helpful as well.

* Install
  * `gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3`
  * `\curl -sSL https://get.rvm.io | bash -s stable`
  * `source /Users/{username}/.rvm/scripts/rvm` (replace {username})
  * `rvm install 2.2.4` (or latest stable release version on this page [Ruby](https://www.ruby-lang.org/en/))
  * `rvm use 2.2.4`
  * You may also want `ruby -v` or `which ruby`.
* Link to [RVM](https://rvm.io/) for niceness sake, but avoid reading their docs at all costs. They are **horrible**.

### Gems

* Postgresql = `gem install pg`
* [Cheatset](https://github.com/Kapeli/cheatset) = `gem install cheatset`

 Make cheat sheets for Dash.

* [Other Gems listed by Category](https://www.ruby-toolbox.com/categories)

### Ruby Web Frameworks

#### Rails

* `gem install rails`
* [Official Getting Started Guide](http://guides.rubyonrails.org/getting_started.html)

[Back to TOC](#table-of-contents)

## Other Helpful Tools

* [Dash](https://kapeli.com/dash)
* [Google Chrome](https://www.google.com/intl/en/chrome/browser/)
 * [1Password Extensions](https://agilebits.com/onepassword/extensions)
 * [Amazon Assitant for Chrome](https://chrome.google.com/webstore/detail/amazon-assistant-for-chro/pbjikboenpfhbbejgkoklgkhjpfogcam)
 * [Cookies](https://chrome.google.com/webstore/detail/cookies/iphcomljdfghbkdcfndaijbokpgddeno)
 * [OneTab](https://chrome.google.com/webstore/detail/onetab/chphlpgkkbolifaimnlloiipkdnihall)
 * [Pin It Button](https://chrome.google.com/webstore/detail/pin-it-button/gpdjojdkbbmdfjfahjcgigfpmkopogic)
 * [ColorZilla](https://chrome.google.com/webstore/detail/bhlhnicpbhignbdhedgjhgdocnmhomnp)
 * [Save to Pocket](https://chrome.google.com/webstore/detail/niloccemoadcdkdjlinkgdfekeahmflj)
 * [Shortcuts for Google](https://chrome.google.com/webstore/detail/baohinapilmkigilbbbcccncoljkdpnd)
* [Mozilla Firefox](https://www.mozilla.org/en-US/firefox/desktop/)
 * [1Password Extenions](https://agilebits.com/onepassword/extensions)
* [Slack](https://slack.com/)
* Download from App Store with Licenses
 * 1Password
 * Omnigraffle
* Toggl

[Back to TOC](#table-of-contents)
