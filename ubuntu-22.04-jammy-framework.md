
> Created as a copy of the 21.04 document on 2022-07-16
```bash
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 22.04 LTS
Release:	22.04
Codename:	jammy
```

## Notes and Assumptions
* When ordering a computer you do NOT want vPro in your Wifi chip. From what I read it has a remote machine takeover. Was designed for corporations to have access to employee laptops.
*  This set of assumptions are based on installing Ubuntu 22.04 LTS(July 7, 2022). By default: 
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
1. 
```bash
sudo apt-get update
sudo apt-get install vim
sudo apt-get python3-gpg            #needed for Dropbox file signature verification and otherwise handy
sudo apt install gnome-tweaks       #to get 2 finger right click to work.
sudo apt install gdebi              #GUI for package installation. recommended by Zoom install page.
```

1. Run all updates in Ubuntu Software.
1. Run all updates in Software Updater.
1. Login to Firefox account. Confirm Firefox Extensions. This adds bookmarks and passwords too.


## Install allllllll the programs
1. Install Zoom [Zoom's Instructions](https://support.zoom.us/hc/en-us/articles/204206269-Installing-or-updating-Zoom-on-Linux)
1. Install Dropbox [Downloads page](https://www.dropbox.com/install)
    * Pause Syncing
    * Select folders for selective sync.
1. Install Webex (yes there are people who still use this) [where to download .deb package](https://www.webex.com/downloads.html)


## Install from Ubuntu Software:
    * Audacity (audio)
    * Calibre (ebook library)
    * dBeaver (DB client)
    * Flameshot (screenshots. currently testing out)
    * GIMP (non-vector art, but easier). Note "digital signatures" in this app means signed certificate signatures. To add an image signature you have to add a new layer based on opening a file. Then you have to scale the image signature layer by clicking on the layer name and scaling that layer specifically.
    * Inkscape (vector art)
    * postman (API call making and testing)
    * qownnotes (notes)
    * Slack
    * VLC (video)


## Install from Snap
1. Microsoft Teams. There are reports that Microsoft Teams doesn't work unless installed through Snap. So, do this.
```bash
#install Microsoft Teams without error by using snap
#https://techviewleo.com/install-and-use-microsoft-teams-on-ubuntu/
sudo apt install snap                       #confirm installed
sudo systemctl enable --now snapd.socket    #enable snap
sudo ln -s /var/lib/snapd/snap /snap        #make sym link
sudo snap install teams-for-linux           #install Microsoft Teams
```

## Configuration
1. Favorite Apps to your dock/sidebar. You want a minimum of: Terminal, Settings, Firefox, Files, Slack, Zoom, Calculator, LibreOffice, Note-taking app. Others to consider: screenshot, Thunderbird or email client, Software Updater














## Not yet done
1. Toggl Timer. Otherise [Linux instructions with flatpak](https://support.toggl.com/en/articles/2410832-toggl-track-desktop-app-for-linux).
    1. [install flatpak](https://flatpak.org/setup/Ubuntu)
    2. [toggl on flatpak](https://flathub.org/apps/details/com.toggl.TogglDesktop) - this may also be possible through a new app(that I think was added by flatpak) called Software
1. Change dot files to personal defaults
    - `.bash_profile` on Mac = `.profile` on Linux Ubuntu. See README.md in this repo.
1. [Enable Deep Sleep](https://community.frame.work/t/ubuntu-21-04-on-the-framework-laptop/2722/7) ^Restart

### Install via Terminal
1. [Github Desktop for Linux](https://github.com/shiftkey/desktop/)
    1. Ensure connection with Gitlab. 
        * Does need key to gitlab created.
        * Must pull repo through Terminal CLI from Gitlab and _then_ you can use it in Github for Desktop. Github for Desktop, on Linux at least, no longer offers a GUI interface for connecting to non-Github or local repo sources.
1. [Docker for Ubuntu](https://docs.docker.com/engine/install/ubuntu/) and follow the [post-install linux instructions](https://docs.docker.com/engine/install/linux-postinstall/)
1. Mozilla VPN. [instructions](https://support.mozilla.org/en-US/kb/how-install-mozilla-vpn-linux-computer)
```bash
sudo add-apt-repository ppa:mozillacorp/mozillavpn
sudo apt-get update
sudo apt-get install mozillavpn
mozillavpn # turn on
```
Login via web browser to Firefox account.


## Settings
1. Tweak setting on how long to wait before sleeping (1 minute is too short)
    * Settings > Power > Power Saving > Automatic Suspend.
    * On Battery Power 15 minutes.
    * On Plugged In 30 minutes.



## Things To Make It Really Work That You find along the way
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
    * For my own reference: [short ubuntu tts page](http://www.solomonson.com/posts/2010-07-24-ubuntu-linux-text-speech/), [Festival Official Project Page](https://www.cstr.ed.ac.uk/projects/festival/). 


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
