
## Repo Creator's Opinions

* When ordering a computer you do NOT want vPro in your Wifi chip. From what I read it has a remote machine takeover. Was designed for corporations to have access to employee laptops.
* De-google, de-apple, de-monopolize yourself.
* :The more you know: about computers the better off you will be. 
* Notes App and To Do app should be in the same app.
* Ubuntu with Gnome GUI is very equivalent to a Windows or Mac computer at this point(Oct 2021). The graphics are just not as sleek and you have more control and freedom. 

## Current Assumptions
1. This set of assumptions are based on installing Ubuntu 21.04, Oct 2021. By default: 
    * Some level of Wi-fi works
    * Firefox is installed
    * External Monitor plug-in works
    * Connecting a printer works
    * LibreOffice is installed
1. You want a computer mirroring Alison's setup. Mix-and-match as desired. Use at your own risk as the GNU GPLv2 license says.
1. You will need a USB key (portable USB) that is at least 4 GB large. This will allow you to make an Ubuntu bootable USB so you can install the OS on your new machine. PLEASE BE AWARE you have to _DELETE_ everything on it in order to do this*... pick a USB key to use accordingly.
1. These instructions will get out of date from Oct. 2021 relatively quickly.

## Default Install

1. [Framework community forum on Ubuntu Linux install on Framework laptop](https://community.frame.work/t/ubuntu-21-04-on-the-framework-laptop/2722)
    - Install Ubuntu 21.04 (only distribution that works right now (Oct 2021). 
        - Version 20 doesn't have default Wifi)
        - Make sure you're installing this specific Ubuntu version. I had to hunt on the Ubuntu website to find this particular version. 
    - Install updated Wifi Drivers 
    - Enable Deep Sleep
1. Run all updates in Ubuntu Software.
1. In terminal, run `sudo apt update`.
1. Install vim (or equivalent).
1. Disk level encryption.

## Install Minimum Programs

1. In terminal
    - Add _apt user. https://askubuntu.com/q/771936 
    - Install Zoom. See https://support.zoom.us/hc/en-us/articles/204206269-Installing-or-updating-Zoom-on-Linux#h_adcc0b66-b2f4-468b-bc7a-12c182f354b7
1. Docker Desktop
1. Slack
1. Install [Privacy Badger Extension](https://addons.mozilla.org/en-US/firefox/addon/privacy-badger17/) to Firefox

## Adjust Default Configurations

1. Change dot files to personal defaults
    - `.bash_profile` on Mac = `.profile` on Linux Ubuntu
1. Copy to or create new SSH keys for commputer
1. "Favorite" Apps in your dock so they stay in the dock
    * Terminal
    * Firefox (should be by default)
    * Files (should be by default)
    * Slack
    * Zoom
    * Calculator
    * Note-taking App
1. Tweak setting on how long to wait before sleeping (1 minute is too short)
1. Browser bookmark creations and/or import
1. Login to Firefox if desired. Provides portability for browser data between machines

## Generally Recommended Apps to Install on Linux
These are available to install via Ubuntu Software.

1. Audacity (audio)
1. VLC (video)
1. Inkscape (vector art)
1. Calibre (e-book library management)

## Takes Time but worth doing

1. Setup addiitonal permissions groups
1. Setup a guest account

## Apps Alison Tried And didn't like

* Notes App (default install)
* Taskbook (installed myself)


## TODO

1. Install video proprietary things (link pending)
1. Figure out best Screenshots with ease of Mac keyboard shortcuts. Default Screenshot app is too time consuming.
1. Figure out best Note Taking Program
    * (Joplin Markdown and Preview mode task lists as of Oct 2021 are "buggy" for my personal workflow)
    * View [latest note-taking recommendations on Slant](https://www.slant.co/topics/6303/~note-taking-apps-for-linux)
        * Trying [QOwnNotes](https://www.qownnotes.org/getting-started/demo.html)
        * [QOwnNotes Firefox Web Companion](https://addons.mozilla.org/en-US/firefox/addon/qownnotes-web-companion/)
        * [QOwnNotes Make Spellcheck Work](https://www.qownnotes.org/editor/spellchecking.html)
1. Figure out best Password sharing/random creation/saving
    * [ PENDING - Can't figure out how not to have vault put online ] In Ubuntu Software, install 1Password.
1. Figure out if I can have a shortcut to put computer to sleep like my mac hot corner.
1. Ensure connection with Gitlab
1. Think through NextCloud


## Issues Run Into So Far
1. On opening Slack, sometimes it will prompt you to force quit or wait. I recommend logging out of any unused Slacks in the app (you can always use them in the browser as relevant) and clicking Wait. 
1. Zoom usage has something not ice going on. For instance, it can make not even copy and paste work



* Yes, if you're really geeky/knowledgeable/willing to take risks this is not an absolute.
