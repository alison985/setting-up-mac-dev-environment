
> Created as a copy of the 21.04 document on 2022-07-16.

```bash
>> lsb_release -a
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

# INSTALL

## Default Install
I integrated lots of info from lots of thread, however the [Official Frame.work Ubuntu 22.04 Install Guide](https://guides.frame.work/Guide/Ubuntu+22.04+LTS+Installation+on+the+Framework+Laptop/109?lang=en) is available.

<!--
[Original 21.04 Install guide thread](https://community.frame.work/t/ubuntu-21-04-on-the-framework-laptop/2722) [Framework Guide for Installing 22.04](https://guides.frame.work/Guide/Ubuntu+22.04+LTS+Installation+on+the+Framework+Laptop/109?lang=en)
    * Includes microphone add
    * wifi update
-->
1. Install stuff in Terminal that you'll need later.
    ```bash
    sudo apt-get update
    sudo apt upgrade -y
    sudo apt-get install vim
    sudo apt-get python3-gpg            #needed for Dropbox file signature verification and otherwise handy
    sudo apt install gnome-tweaks       #to get 2 finger right click to work.
    sudo apt install gdebi              #GUI for package installation. recommended by Zoom install page.
    mkdir ~/Sites                       #directory to clone repos to so that you don't have problems with Dropbox sync
    sudo vim /etc/modprobe.d/alsa-base.conf     #enable headset mic input
    [scroll to end of file]
    i
    enter
    options snd-hda-intel model=dell-headset-multi
    esc
    :qw
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
1. Improve power usage on sleep/suspend.
    ```bash
    # On some SSDs (e.g. SN750 with older firmware), there is a workaround to improve suspend battery life
    #   How to change grub options in general https://linuxhint.com/change-grub-options/
    #   why change from deep sleep like used in 21.04 https://community.frame.work/t/linux-battery-life-tuning/6665#suspend-power-usage-2 AND default enabled in 22.04
    #   from frame.work instructions: sudo sed -i 's/^GRUB_CMDLINE_LINUX_DEFAULT.*/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash nvme.noacpi=1/g' /etc/default/grub

    sudo cp /etc/default/grub /etc/default/grub.bak     #make backup of file before changing it
    sudo vim /etc/default/grub
    [scroll to end of tile]
    i
    enter
    GRUB_CMDLINE_LINUX_DEFAULT="quiet splash nvme.noacpi=1"
    esc
    :qw
    ```
1. confirm change
    ```bash
    cat /sys/power/mem_sleep
    ## note this isn't updating for me from the `[s2idle] deep` response even after reboot

    # Then refresh the GRUB configuration
    sudo update-grub

    # And reboot
    sudo reboot
    ```
1. Deep sleep seems to be enabled already for 22.04. Confirm that `cat /sys/power/mem_sleep` returns `[s2idle] deep` or see [Enable Deep Sleep](https://community.frame.work/t/ubuntu-21-04-on-the-framework-laptop/2722/8)
1. Install Sublime Text 

```JSON
// Settings in here override those in "Default/Preferences.sublime-settings",
// and are overridden in turn by syntax-specific settings.
{
	"translate_tabs_to_spaces": true, 
    "highlight_modified_tabs": true, 
    "bold_folder_labels": true, 
    "show_encoding": true, 
    "binary_file_patterns": ["*.epub"],
    "folder_exclude_patterns": [".svn", ".git", ".hg", "CVS"],

}
```


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
* dBeaver and/or BeeKeeper Studio (DB client)
* GIMP (non-vector art, but easier). Note "digital signatures" in this app means signed certificate signatures. To add an image signature you have to add a new layer based on opening a file. Then you have to scale the image signature layer by clicking on the layer name and scaling that layer specifically.
* Inkscape (vector art)
* postman (API call making and testing)
* ?? qownnotes (notes) / Joplin
* Slack
    * Login to Slack
* VLC (video)
* Brasero (burn cd, dvd)


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
1. [VSCodium - the privacy-aware Visual Studio Code](https://github.com/VSCodium/vscodium). Text-based coding IDE. Binary releases of VS Code without MS branding/telemetry/licensing 
1. Extension Manager


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
1. Install the Github Desktop app. 
    * In the app, login to Github.
    * Clone repos from Gitlab with your Gitlab personal access token in Terminal.


## Install for Development Environment

1. Python
Note, `python` does not work in the Terminal. That's because there's no alias from python3 to python. If `python` does work then `.bashrc` has to refer to /usr/bin/python instead of what's below. Yes, the lack of this alias then creates a mis-match between virtualenv(wrapper) and the VSCodium python interpreter setting. That said, I have yet to try VSCodium to run Python, so maybe it can't detect the /python3(non-alias) version? Python 3.10.4 is the result in the Terminal and and Python 3.10.6 is mentioned in the VSCodium dialogue to select a python interpreter, which strengthens this theory.
 
:shrug: You will have virtualenv and virtualenvwrapper for MyCroft and python scripting without Docker containers.

    ```bash
    python3 --version
        > Python 3.10.4
    sudo apt-get install python3-pip build-essential # python-dev was here but no longer has an installation candidate

    # Both `pip --version` and `pip3 --version` work and are the same result.

    sudo pip install --upgrade pip              # --upgrade pip3 won't work
    sudo pip install --upgrade virtualenv 
    sudo pip install --upgrade virtualenvwrapper

    # Setup virtualenvwrapper
    # Reference, but not enough https://virtualenvwrapper.readthedocs.io/en/latest/
    cd ~/
    export WORKON_HOME=~/Envs
    mkdir -p $WORKON_HOME
    sudo vim .bashrc
    [scroll to bottom] 
    i
    #virtualenvwrapper config
    export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
    export WORKON_HOME=~/Envs
    source /usr/local/bin/virtualenvwrapper.sh
    [ESC]
    :w
    :q
    ```

    #  5. Run: workon
    #  6. A list of environments, empty, is printed.
    #  7. Run: mkvirtualenv temp
    #  8. Run: workon
    #  9. This time, the "temp" environment is included.
    # 10. Run: workon temp
    # 11. The virtual environment is activated. Maybe you want to install pandas.
    ```
1. Open VSCodium(privacy version of Visual Studio Code) that was installed above. 
    * Color Theme: Monokai Dimmed
    * Language support: 
        * Search `@builtin` will have the following installed: HTML, JavaScript, JSON, Markdown, Python, Shell Script, SQL, and YAML Language Basics
        * Search with `@sort:rating` or `@sort:installs` to find the following
            * Don't install SQLTools - it's not great. Use a dedicated SQL client.
            * YAML from Redhat
            * Better Jinja from samuelcolvin
            * an icon package (Material Icon Theme by PKief with 107k+ downloads)
            * Rainbow CSV
        * Consider in future: Bookmarks, XML, Python Extension Pack, Bootstrap 4 and/or Bootstrap 5 & Font Awesome Snippets, Debugger for Firefox, Highlight Matching Tag, Paste JSON as Code, MySQL, Github Respositories, AWS Toolkit, Docker, Snowflake Driver for SQLTools, SQLTools PostgreSQL/Redshift Driver, SQL(BigQuery), sqlfluff, one of the dbt ones, Color Picker or Color Highlight or something else, a TODO one

    * Select your python interpreter (Recommended: /usr/bin/python Python 3.10.6 64-bit)

1. [Docker for Ubuntu](https://docs.docker.com/engine/install/ubuntu/) and follow the [post-install linux instructions](https://docs.docker.com/engine/install/linux-postinstall/)

1. Postgres [Source](http://tecadmin.net/install-postgresql-server-on-ubuntu/) (CHECK THESE to ensure they are up-to-date)
    ```bash
    sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'
    wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | sudo apt-key add -
    sudo apt-get update
    sudo apt-get install postgresql
    sudo su - postgres
    psql
    ```

    OPTIONAL STEPS (good for finding port that postgres is running on. Default is 5432.
    Postgres:
    ```postgresql
    \conninfo
    \q
    ```

    Command line:
    ```bash
    su MAINUSERNAME
    (password)
    ```

    Create user for postgres and system. Something like this.
    ```bash
    createuser [username]
    sudo apt install postgresql-contrib
    sudo -i -u postgres
    su - [admin username]
    cd [directory to save postgres db]
    sudo adduser [username]
    sudo -u [username] psql
    ```

1. Navicat 
    After downloaded, `cd` to directory in terminal and `./navicat16-premium-en.AppImage`.

1. Install some servers. [Source](https://realpython.com/blog/python/kickstarting-flask-on-ubuntu-setup-and-deployment/)
    ```bash
    sudo apt-get install git nginx gunicorn
1. In .bashrc, [change HISTFILESIZE=2000 to 20000]    ```


## Configuration
1. If you haven't for awhile, this is a good time to restart.
1. Favorite Apps to your dock/sidebar. You want a minimum of: Terminal, System Monitor, Settings, Firefox, Files, Slack, Zoom, Calculator, LibreOffice, Note-taking app(Joplin). Others to consider: screenshot, Thunderbird or email client, "Software"(instead of Ubuntu Software)
1. Change dot files to personal defaults
    * DO WITH CAUTION, these are out of date and probably are missing things from above. `.bash_profile` on Mac = `.profile` on Linux Ubuntu. See [Mac OS](mac-os_thru_2021.md) in this repo.
1. Log into Zoom and Microsoft Teams (and Webex) to make sure your mic and video are permissioned and working.
1. Log into Pocket and Pinterest from your browser.
1. Setup relevant email accounts in Thunderbird or other smail client.
1. Plug-in printer to get it recognized and print test page.
1. Install GNOME Extensions. I'm experimenting with the following.
    * [OpenWeather](https://extensions.gnome.org/extension/750/openweather/)
    * [Vitals](https://extensions.gnome.org/extension/1460/vitals/)
    * [Clipboard Indicator](https://extensions.gnome.org/extension/779/clipboard-indicator/)
    * [Screenshot Tool](https://extensions.gnome.org/extension/1112/screenshot-tool/)




### Configure via Terminal
1. `sudo apt-get install chrome-gnome-shell` to be able to [add gnome extensions](https://wiki.gnome.org/action/show/Projects/GnomeShellIntegration/Installation?action=show&redirect=Projects%2FGnomeShellIntegrationForChrome%2FInstallation#Ubuntu_Linux) from the browser (later linux versions gnome-browser-connector)
1. `gnome-tweaks` will open some configuration settings. 
    * General > "Suspend when laptop lid is closed" to on
    * Startup Applications >
        * Dropbox (should be there already)
        * Mozilla VPN (consider)
    * Top Bar > 
        * Flip Weekday to on
    * Window Titlebars > 
        * Under Titlebar Buttons change Placement to Left. (Make it easier to switch between Mac and Linux.)
        * Under Titlebar Actions change Double-Click to "Toggle Maximize Vertically". (Might be the Xoom answer.)


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
1. Disk level encryption
1. Copy to or create new SSH keys for commputer

## Chosen against
1. Flameshot - way too easy to accidently upload to public web

## TODO
1. Screenshots
1. Note-taking (Joplin ATM)
1. Passwords
1. Shortcut to put computer to sleep

* Yes, if you're really geeky/knowledgeable/willing to take risks this is not an absolute.
