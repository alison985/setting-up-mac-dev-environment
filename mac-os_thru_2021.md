

# How To Setup a Mac Development Environment (from scratch)
Should be considered out-of-date but still relevant overall.
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
* [Docker](#docker)
* [Other Helpful Tools](#other-helpful-tools)
* [Out of Date](#out-of-date-2021)

## Assumptions

* Mac OS X 10.10.4+
* Dropbox
* Sublime Text 3
* You're logged in as an administrative user of the computer.
* You want Python 2.7.x (2.7 is end of life, upgrade to 3!)
* You have a VPN already

## Basic Configuration
* [Github for Mac](https://mac.github.com/)  [ [Source](http://hackercodex.com/guide/mac-osx-mavericks-10.9-configuration/) ]
* Unhide Library Folder
    * Open Finder.
    * Press `shift-command-H` and then `command-J`, which will bring up a window that configures Finder view options.
    * Check the “Show Library Folder” and close the window.
* Bash Profile Setup
  * `vim ~/.bash_profile`

```bashsi
# Finder: show hidden files
defaults write com.apple.finder AppleShowAllFiles TRUE

# Always use colour output for ls.
[[ "$OSTYPE" =~ ^darwin ]] && alias ls='command ls -G' || alias ls='command ls --color';

######ALIASES###############
alias sublime='open -a "Sublime Text 2"'
alias reload='source ~/.bash_profile'
alias edit_profile='vim ~/.bash_profile'

######EXPORT#############
export EDITOR=sublime

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

export WORKON_HOME=~/Envs
export PROJECT_HOME=~/Envs
export VIRTUALENVWRAPPER_PYTHON=/usr/local/bin/python
export VIRTUALENVWRAPPER_VIRTULENV=/usr/local/bin/virtualenv
source /usr/local/bin/virtualenvwrapper.sh
```
    * `source ~/.bash_profile`

* Get the XCode pieces you need
    * `xcode-select --install`
    * Will prompt for full version of Xcode or just command line tools

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
import urllib.request,os,hashlib; h = 'df21e130d211cfc94d9b0905775a7c0f' + '1e3d39e33b79698005270310898eea76'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```

### Default Sublime Packages
* [Markdown Preview](https://packagecontrol.io/packages/Markdown%20Preview)
* [Color Highlighter](https://packagecontrol.io/packages/Color%20Highlighter)
* [PostgreSQL Syntax Highlighting](https://packagecontrol.io/packages/PostgreSQL%20Syntax%20Highlighting)
* [Bracket Highlighter](https://packagecontrol.io/packages/BracketHighlighter)
* Bootstrap 4 Snippets
* Gitgutter
    - In Preference > Settings > user file add
```
{
	"auto_complete_triggers":
	[
		{
			"characters": "b4",
			"selector": "text.html"
		}
	],
	"font_size": 15,
	"ignored_packages":
	[
		"Vintage"
	]
}
```

Sublime Text 3 Only
* [Sidebar Enhancements](https://packagecontrol.io/packages/SideBarEnhancements)

[Back to TOC](#table-of-contents)

## Local Databases

### mySQL

```bash
mysql -v
brew install mysql
mysql -v
mysql -uroot

# mysql-5.7.19.sierra.bottle.tar.gz as of this writing

#We've installed your MySQL database without a root password. To secure it run:
#    mysql_secure_installation

#MySQL is configured to only allow connections from localhost by default

#To connect run:
#    mysql -uroot

#To have launchd start mysql now and restart at login:
#  brew services start mysql
#Or, if you don't want/need a background service you can just run:
#  mysql.server start
```

### Postgresql

* [Postgres.app](http://postgresapp.com/)

[Back to TOC](#table-of-contents)

## Python Specific Environment

### Virtual Environment

Asssumes the variables for virtualenv listed in the ~/.bash_profile above. Uses virtualenvwrapper to - you guessed it - wrap virtualenv.

```bash
pip install virtualenv
pip install --ignore-installed six #handles six upgrade error
pip install virtualenvwrapper
export WORKON_HOME=~/Envs
source /usr/local/bin/virtualenvwrapper.sh
```
* Close Terminal and Re-open Terminal.
* `cd` to your directory
* `mkvirtualenv venv`
* `workon venv`

### Sublime Python Packages
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

## Docker

* Download stable package from [https://docs.docker.com/docker-for-mac/install/](https://docs.docker.com/docker-for-mac/install/) and install.

## Other Helpful Tools

* [Toggl](https://support.toggl.com/toggl-on-my-desktop/)
* [Mozilla Firefox](https://www.mozilla.org/en-US/firefox/desktop/)
    * Set Default Search to bing.com 
    * [1Password Extenions](https://agilebits.com/onepassword/extensions)
    * [EFF Plugin Home](https://www.eff.org/pages/tools) - HTTPS Everywhere, etc.
    * [Wayback Machine Extension](https://addons.mozilla.org/en-US/firefox/addon/wayback-machine_new/)
    * Find other [Firefox Addons](https://addons.mozilla.org/en-US/firefox/extensions/)
* [Slack](https://slack.com/)
* Download from App Store with Licenses
    * 1Password
    * Moom
    * Paste or [non-Mac Store](https://pasteapp.io/)
    * Navicat

[Back to TOC](#table-of-contents)

## Out-of-Date 2021
### Dev
* Start the Xcode download/updates first through the App Store. This takes awhile. (you can download only the part you need with the CLI command above.)

Sublime Packages - Optional/Don't Use in 2021
* RegReplace
* [HTML-CSS-JS Prettify](https://packagecontrol.io/packages/HTML-CSS-JS%20Prettify)
* [Pretty JSON](https://packagecontrol.io/packages/Pretty%20JSON)
* [Bootstrap 3 Snippets](https://packagecontrol.io/packages/Bootstrap%203%20Snippets)

* mergetool/difftool
    * [Kaleidoscope](http://www.kaleidoscopeapp.com/)
    * Other options: 
      * [Diff Tools on Mac OS X Blog Entry](http://www.git-tower.com/blog/diff-tools-mac/) 
      * [Meld](http://meldmerge.org/) through [MacPorts](https://www.macports.org/install.php)
 
## Ruby Specific Environment - Out-of-Date

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

Here are commands I've used in getting started on a rails project setup. Don't run unless you understand them.

* `gem install bundler`
* `bundle install`
* `gem install rails`
* [Official Getting Started Guide](http://guides.rubyonrails.org/getting_started.html)
* `bin/setup`
* `bundle exec rake db:create db:schema:load`

[Back to TOC](#table-of-contents)
 
### Other
 
* [Google Chrome](https://www.google.com/intl/en/chrome/browser/)
   * [1Password Extensions](https://agilebits.com/onepassword/extensions)
   * [Cookies](https://chrome.google.com/webstore/detail/cookies/iphcomljdfghbkdcfndaijbokpgddeno)
   * [HTTPS Everywhere](https://chrome.google.com/webstore/detail/https-everywhere/gcbommkclmclpchllfjekcdonpmejbdp)
   * [Privacy Badger](https://chrome.google.com/webstore/detail/privacy-badger/pkehgijcmpdhfbdbbnkijodmdjhbjlgp)
   * [Pin It Button](https://chrome.google.com/webstore/detail/pin-it-button/gpdjojdkbbmdfjfahjcgigfpmkopogic)
   * [ColorZilla](https://chrome.google.com/webstore/detail/bhlhnicpbhignbdhedgjhgdocnmhomnp)
   * [Save to Pocket](https://chrome.google.com/webstore/detail/niloccemoadcdkdjlinkgdfekeahmflj)
