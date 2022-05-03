## Repo Creator's Opinions

* When ordering a computer you do NOT want vPro in your Wifi chip. From what I read it has a remote machine takeover. Was designed for corporations to have access to employee laptops.
* De-google, de-apple, de-monopolize yourself.
* :The more you know: about computers the better off you will be. 
* --Notes App and To Do app should be in the same app.--
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

As of 2022-05-03.
```bash
lsb_release -a
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 21.10
Release:	21.10
Codename:	impish
```

## Remember
`Shift+Cnl+C` or `+V` to copy and paste into terminal.

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
    * Calculator
    * Your note-taking app of choice
1. Tweak setting on how long to wait before sleeping (1 minute is too short)
1. Browser bookmark creations and/or import
1. Login to Firefox if desired. Provides portability for browser data between machines

## Things To Make It Really Work That You find along the way
* Video codecs. There's an apt option for ubuntu-restricted-extras. However, for me, in this laptop and configuration, `sudo apt-get install -y ffmpeg` worked for me. Make sure to restart your browser.
* Audacity needs a file change to give it a permission. It prompts you with instructions in a modal on start-up. The Blue microphone worked after doing this. I also had to put the sample rate at 192kb in audacity to avoid error messages.
* See also anything in the [current summary of install steps from the frame.work 21.04 install thread](https://community.frame.work/t/ubuntu-21-04-on-the-framework-laptop/2722).

## Generally Recommended Apps to Install on Linux

### Install via Ubuntu Software.
1. Audacity (audio)
1. VLC (video)
1. Inkscape (vector art)
1. Calibre (e-book library management)
1. GIMP (non-vector art, but easier). Note "digital signatures" in this app means signed certificate signatures. To add an image signature you have to add a new layer based on opening a file. Then you have to scale the image signature layer by clicking on the layer name and scaling that layer specifically.
1. Toggl Timer. Otherise [Linux instructions with flatpak](https://support.toggl.com/en/articles/2410832-toggl-track-desktop-app-for-linux).

### Install via Terminal
1. [Github Desktop for Linux](https://github.com/shiftkey/desktop/)
1. [Docker for Ubuntu](https://docs.docker.com/engine/install/ubuntu/) and follow the [post-install linux instructions](https://docs.docker.com/engine/install/linux-postinstall/)
1. Vim if not already installed.
1. Mozilla VPN. [instructions](https://support.mozilla.org/en-US/kb/how-install-mozilla-vpn-linux-computer)
```bash
sudo add-apt-repository ppa:mozillacorp/mozillavpn
sudo apt-get update
sudo apt-get install mozillavpn
mozillavpn # turn on
```
Login via web browser to Firefox account.

### Possible installs
1. Zoom - note if Zoom is running it's about the only thing you can use at the time. Good install as a back-up for times you can get a second device online.
1. Ensure connection with Gitlab. 
    * Does need key to gitlab created.
    * Must pull repo through Terminal CLI from Gitlab and _then_ you can use it in Github for Desktop. Github for Desktop, on Linux at least, no longer offers a GUI interface for connecting to non-Github or local repo sources.
1. Evolution for email Client via Ubuntu software.
1. Text-to-speech, especially for ePub. 
    * Install voice synthesizer and a nice voice. From [askubuntu.com answer](https://askubuntu.com/a/908889)
    ```bash
    sudo apt-get install festival
    sudo apt-get install festvox-us-slt-hts
    festival -i
    festival> (voice_cmu_us_slt_arctic_hts) 
    festival> (SayText "Don't hate me, I'm just doing my job!")
    ```
    * Set the nice voice as default voice in `/etc/festival.scm` using [these instructions](https://ubuntuforums.org/showthread.php?t=751169). My file ends up with:
    ```bash
    (Parameter.set 'Audio_Command "aplay -q -c 1 -t raw -f s16 -r $SR $FILE")
    (Parameter.set 'Audio_Method 'Audio_Command)
    (set! voice_default 'voice_cmu_us_slt_arctic_hts)
    (set! hts_duration_stretch 0.1)
    (Parameter.set 'Duration_Stretch 2.5)
    ```
    * [Install Flatpak](https://flatpak.org/setup/Ubuntu) so you can install Foliate via Flatpak [not via snap](https://github.com/johnfactotum/foliate/wiki#how-to-use-text-to-speech).
    * Restart
    * [Install Foliate via flatpak](https://flathub.org/apps/details/com.github.johnfactotum.Foliate). Foliate is an ePUB viewer that lets you add annotations and more control over which voice to do TTS reading in.
    ```bash
    flatpak install flathub com.github.johnfactotum.Foliate
    ```  
    * For my own reference: [short ubuntu tts page](http://www.solomonson.com/posts/2010-07-24-ubuntu-linux-text-speech/), [Festival Official Project Page](https://www.cstr.ed.ac.uk/projects/festival/). 

## Takes Time but worth doing

1. Setup addiitonal permissions groups
1. Setup a guest account

## TODO

1. Figure out best Screenshots with ease of Mac keyboard shortcuts. Default Screenshot app is too time consuming. Fast research pass hasn't found a good answer.
1. Figure out best Note Taking Program
    * (Joplin Markdown and Preview mode task lists as of Oct 2021 are "buggy" for my personal workflow)
    * View [latest note-taking recommendations on Slant](https://www.slant.co/topics/6303/~note-taking-apps-for-linux)
        * Trying [QOwnNotes](https://www.qownnotes.org/getting-started/demo.html)
            * RECOMMEND AGAINST the related [QOwnNotes Firefox Web Companion](https://addons.mozilla.org/en-US/firefox/addon/qownnotes-web-companion/) Breaks copy/paste from Firefox. Makes a new note for each copy/paste instead of including in current note. I didn't figure out a way to do image inclusion with it. 
            * [QOwnNotes Make Spellcheck Work](https://www.qownnotes.org/editor/spellchecking.html)
1. Figure out best Password sharing/random creation/saving
    * [ PENDING - Can't figure out how not to have 1Password vault put online ] In Ubuntu Software, install 1Password.
    * Currently using built-in Firefox feature. will transfer across devices but un/pw fields only without notes.
1. Figure out if I can have a shortcut to put computer to sleep like my mac hot corner.


## Apps Alison Tried And decided against

* Notes App (default install)
* Taskbook (installed myself)
* NextCloud. Based on r/nextcloud it seems like a lot of work(overhead) to run yourself for my particular needs right now.

## Issues Run Into So Far
1. On opening Slack (and other programs), sometimes it will prompt you to force quit or wait. I recommend logging out of any unused Slacks in the app (you can always use them in the browser as relevant) and clicking Wait. 
1. Zoom usage has something not nice going on. For instance, it can make not even copy and paste work. Framework community posts about optimizations may help. I have resorted to using my old Mac laptop for Zoom usage because it's just too painful.



* Yes, if you're really geeky/knowledgeable/willing to take risks this is not an absolute.
