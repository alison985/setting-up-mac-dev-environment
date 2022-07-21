
> Created as a copy of the 21.04 document on 2022-07-16
```bash
>> lsb_reelase -a
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 22.04 LTS
Release:	22.04
Codename:	jammy
>> python3 --version
Python 3.10.4
```

## Notes and Assumptions
* When ordering a computer you do NOT want vPro in your Wifi chip. From what I read it has a remote machine takeover. Was designed for corporations to have access to employee laptops.
* As a whole this document lists steps to do in order. Or at least an order that should work. That said, mix and match and YMMV.
* This set of assumptions are based on installing Ubuntu 22.04 LTS(July 7, 2022). By default: 
    * Some level of Wi-fi works
    * Firefox is installed
    * External Monitor plug-in works
    * Connecting a printer works
    * LibreOffice is installed
* You want a computer mirroring Alison's setup. Mix-and-match as desired. Use at your own risk as the GNU GPLv2 license says.
* You will need a USB key (portable USB) that is at least 4 GB large. This will allow you to make an Ubuntu bootable USB so you can install the OS on your new machine. PLEASE BE AWARE you have to _DELETE_ everything on it in order to do this*... pick a USB key to use accordingly.
* These instructions will get out of date relatively quickly.

## Remember
`Shift+Cnl+C` or `+V` to copy and paste into terminal.

## Default Install
1. [Original 21.04 Install guide thread](https://community.frame.work/t/ubuntu-21-04-on-the-framework-laptop/2722) [Framework Guide for Installing 22.04](https://guides.frame.work/Guide/Ubuntu+22.04+LTS+Installation+on+the+Framework+Laptop/109?lang=en)
    * Includes microphone add
    * wifi update
1. Install stuff you'll need later.
    ```bash
    sudo apt-get update
    sudo apt-get install vim
    sudo apt-get python3-gpg            #needed for Dropbox file signature verification and otherwise handy
    sudo apt install gnome-tweaks       #to get 2 finger right click to work.
    sudo apt install gdebi              #GUI for package installation. recommended by Zoom install page.
    mkdir ~/Sites                       #directory to clone repos to so that you don't have problems with Dropbox sync
    ```
1. Run all updates in Ubuntu Software.
1. Run all updates in Software Updater.
1. Probably a good place to restart if you haven't recently.
1. Plug-in external monitor.
1. Login to Firefox account. Confirm Firefox Extensions. This adds bookmarks and passwords too.
1. Mozilla VPN. [instructions](https://support.mozilla.org/en-US/kb/how-install-mozilla-vpn-linux-computer)
    ```bash
    sudo add-apt-repository ppa:mozillacorp/mozillavpn
    sudo apt-get update
    sudo apt-get install mozillavpn
    ```
    Open the MozillaVPN app. Login via web browser to Firefox account.
1. Deep sleep seems to be enabled already for 22.04. Confirm that `cat /sys/power/mem_sleep` returns `[s2idle] deep` or see [Enable Deep Sleep](https://community.frame.work/t/ubuntu-21-04-on-the-framework-laptop/2722/8)


## Install as One-offs
1. Install Zoom [Zoom's Instructions](https://support.zoom.us/hc/en-us/articles/204206269-Installing-or-updating-Zoom-on-Linux)
    * Login to Zoom.
1. Install Dropbox [Downloads page](https://www.dropbox.com/install)
    * Login to Dropbox.
    * Pause Syncing
    * Select folders for selective sync. Do a set, then another set, then another set so that you have the files you most need available first.
1. Install Webex (yes there are people who still use this) [where to download .deb package](https://www.webex.com/downloads.html)


## Install from Ubuntu Software
* Audacity (audio)
* Calibre (ebook library) (copy your existing library into place from a backup first)
* dBeaver (DB client)
* Flameshot (screenshots. currently testing out)
* GIMP (non-vector art, but easier). Note "digital signatures" in this app means signed certificate signatures. To add an image signature you have to add a new layer based on opening a file. Then you have to scale the image signature layer by clicking on the layer name and scaling that layer specifically.
* Inkscape (vector art)
* postman (API call making and testing)
* qownnotes (notes)
* Slack
    * Login to Slack
* VLC (video)


## Install from Snap ("Software" app)
1. Microsoft Teams. There are reports that Microsoft Teams doesn't work unless installed through Snap. So, do this.
    ```bash
    #install Microsoft Teams without error by using snap
    #https://techviewleo.com/install-and-use-microsoft-teams-on-ubuntu/
    sudo apt install snap                       #confirm installed
    sudo systemctl enable --now snapd.socket    #enable snap
    sudo ln -s /var/lib/snapd/snap /snap        #make sym link
    sudo snap install teams-for-linux           #install Microsoft Teams
    ```
1. Visual Studio Code. Make sure you get the one that is called "code" and says by "Visual Studio Code [green checkmark]


## Install from Flatpak
1. Install Toggl Timer. [Linux instructions with flatpak](https://support.toggl.com/en/articles/2410832-toggl-track-desktop-app-for-linux).
    * [install flatpak](https://flatpak.org/setup/Ubuntu)
    ```bash
    sudo apt install flatpak
    sudo apt install gnome-software-plugin-flatpak
    flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
    ```
    * Restart.
    * Open "Software" app. Search for toggl and install "Toggl Track".
1. Install Github Desktop. 
    * Login to Github.
    * Clone repos from Gitlab with your personal access token.


## Configuration
1. If you haven't for awhile, this is a good time to restart.
1. Favorite Apps to your dock/sidebar. You want a minimum of: Terminal, Settings, Firefox, Files, Slack, Zoom, Calculator, LibreOffice, Note-taking app. Others to consider: screenshot, Thunderbird or email client, Software Updater
1. Change dot files to personal defaults
    * `.bash_profile` on Mac = `.profile` on Linux Ubuntu. See README.md in this repo.
1. Log into Zoom and Teams to make sure your mic and video are working.
1. Open Visual Studio Code (I'm trying it out). 
    * Color Theme: Monokai Dimmed
    * Language support: 
        * Python, HTML CSS, Javascript, YAML, Jinja, 
        * Other language support (testing): Color Highlight, TODO Highlights, Rainbow CSV, SQLTools, VSCode Great Icons
        * Consider in future: Bookmarks, XML, Python Extension Pack, Bootstrap 4, Debugger for Firefox, Highlight Matching Tag, Paste JSON as Code, MySQL, Github Respositories, AWS Toolkit, Docker, Snowflake Driver for SQLTools, SQLTools PostgreSQL/Redshift Driver, SQL(BigQuery), sqlfluff, one of the dbt ones
    * Select your python interpreter
1. Log into Pocket and Pinterest from your browser.
1. Setup relevant email accounts in Thunderbird or other smail client.
1. Python dev environment. Yes, yes, install an environment manager first.
    ```bash
    sudo apt install python3-pip`
    sudo pip3 install pandas
    ``` 


### Install via Terminal
1. [Docker for Ubuntu](https://docs.docker.com/engine/install/ubuntu/) and follow the [post-install linux instructions](https://docs.docker.com/engine/install/linux-postinstall/)


## Settings
1. Tweak setting on how long to wait before sleeping (1 minute is too short)
    * Settings > Power > Power Saving > Automatic Suspend.
    * On Battery Power 15 minutes.
    * On Plugged In 30 minutes.



<!-- ## Things To Make It Really Work That You find along the way
* Video codecs. There's an apt option for ubuntu-restricted-extras. However, for me, in this laptop and configuration, `sudo apt-get install -y ffmpeg` worked for me. Make sure to restart your browser.
    * For playing DVDs. [Reference](https://websiteforstudents.com/how-to-play-dvd-in-ubuntu-linux/)
      ```bash
      #maybe sudo add-apt-repository multiverse
      sudo apt install libdvd-pkg
      #it's okay that some of them don't install
      sudo apt install libdvdread7
      sudo apt install libdvdread8
      sudo apt install libdvdread4
      sudo apt install libdvdnav4
      #these are the ones that are proprietary from what I can tell
      sudo apt install gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly
      sudo apt install ubuntu-restricted-extras
      ```
* Audacity needs a file change to give it a permission. It prompts you with instructions in a modal on start-up. The Blue microphone worked after doing this. I also had to put the sample rate at 192kb in audacity to avoid error messages.
* See also anything in the [current summary of install steps from the frame.work 21.04 install thread](https://community.frame.work/t/ubuntu-21-04-on-the-framework-laptop/2722).

 
### Possible installs
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
    * For my own reference: [short ubuntu tts page](http://www.solomonson.com/posts/2010-07-24-ubuntu-linux-text-speech/), [Festival Official Project Page](https://www.cstr.ed.ac.uk/projects/festival/).  -->


## Takes Time but worth doing
1. Setup addiitonal permissions groups
1. Setup a guest account
1. Disk level encryption.
1. Copy to or create new SSH keys for commputer


## TODO
1. Screenshots
1. Note-taking
1. Passwords
1. Shortcut to put computer to sleep

* Yes, if you're really geeky/knowledgeable/willing to take risks this is not an absolute.
