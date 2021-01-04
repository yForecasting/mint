# Linux Mint
This is a brief introduction how to get started with Linux Mint for data science and academic research. 

To see your current version of Mint, use in the terminal:

> cat /etc/os-release

## Programming Tools
### Install R
Install R via the terminal:
> sudo apt update
> sudo apt-get install r-base

You can test R by simply: 
> R

> install.packages("ggplot2")

> q()

### Install Rstudio
get the name of the last Ubuntu/Debian Rstudio version at https://rstudio.com/products/rstudio/download/#download Do a right-click, copy file location. 
> wget https://download1.rstudio.org/desktop/bionic/amd64/rstudio-1.3.1093-amd64.deb

If needed to install gdebi:

> sudo apt install gdebi

Then install the deb-file:

> sudo gdebi rstudio-1.3.959-amd64.deb

The R-file here installs all basic needed packages. You can open and run it in Rstudio.
In case of errors, you can use:
> apt install r-cran-stringi 
And if this results in errors, then try: 
> sudo apt purge -y r-base r-base-core r-base-dev
> sudo apt install -y r-base r-base-core r-base-dev


! For Mint you will need following for installing devtools: 
> sudo apt install libxml2-dev

> sudo apt install libssl-dev

> sudo apt install libcurl4-openssl-dev

### Install pyCharm
For pyCharm, do not use the Software Manager, as this version is often outdated. Use the jetBrains website instead, and preferrably install via the tar. 

Go to your download location and then use the recommended installation location according to the filesystem hierarchy standard (FHS). --> is /opt. To install PyCharm into this directory, enter the following command:

> sudo tar xzf pycharm-*.tar.gz -C /opt/

Switch to the bin subdirectory with the terminal.
> cd /opt/pycharm-*/bin

Run pyCharm from this directory.

> sh pycharm.sh

After a graphical configuration setup, you get the standard IDE. 
If an error occured beacaus the Python interpreter could not be installed, then do:
*  Configure Python interpreter
*  Add interpreter
*  System interpreter
*  Select the latest Python version
*  OK

You'll notice none of the frequent packages are installed (try import numpy).
First install pip in the terminal:
> sudo apt update
> sudo apt install python3-pip python3-pip

Then install the package in the terminal:
> pip3 install numpy

You can now see the package installed in pyCharm
Go to File > Settings > Project > Python interpreter

To add a desktop shortcut:
*  Desktop > RM > New Launcher
*  Command > Browse > go to /opt/pycharm*/bin/pycharm.sh
*  Command: type sh before the path
*  Fill in Name, Comment, Picture as you like
*  Say Yes to add to Menu as well.


Installing additional packages can now also be done in the terminal in pyCharm.

For your information:
The alternative install of pyCharm via snap is no longer supported from Mint 20 onwards. Yes, there is a workaround and this gives away admin privileges to snap.

## Resource Management Tools
### Install Smartgit
SmartGit is a version control management software. 

> sudo apt-get install gdebi
> wget http://www.syntevo.com/static/smart/download/smartgit/smartgit-17_0_1.deb
> sudo gdebi smartgit-17_0_1.deb

You need to install git as well:
> sudo apt-get install git
> sudo add-apt-repository ppa:git-core/ppa 
> sudo apt update; apt install git

#### (OR Install Gitkraken)
Gitkraken is an alternative for smartgit. It can be installed via the software manager or via: 

> wget https://release.gitkraken.com/linux/gitkraken-amd64.tar.gz

> sudo tar -xvzf gitkraken-amd64.tar.g

#### (Repair broken packages)
Not all goes perfect the first time, so in case something brakes down:

> sudo apt update --fix-missing

> sudo apt install -f

## Datebase Tools
### Install DBeaver
DBeaver is a database explorer, which visualises all accessible tables via the database scheme. It also enables easy querying of different sources. Supports MySQL, MariaDB, SQLite, Oracle, DB2, SQL Server, Sybase, MS Access, Teradata, Firebird and Derby.

First update the linux:

> sudo apt update 

> sudo apt upgrade

DBeaver requires java:

To check the current version:

> java --version

To install Java:

> sudo add-apt-repository ppa:linuxuprising/java

> sudo apt install oracle-java12-installer

Install DBeaver now:

> sudo apt update && sudo apt install dbeaver-ce

Test DBeaver:

> sudo apt install mariadb-server

> sudo mysql -u root -p
> CREATE DATABASE dbeaver;
> GRANT ALL PRIVILEGES ON dbeaver.* TO 'dbeaveruser'@'localhost' IDENTIFIED BY 'dbeaverpss';
> FLUSH PRIVILEGES;
> exit;

## Help with System issues
### Ethernet card
To see all cards:

> lshw -C network

To see if your card is up:
> inxi -Fxxxz

You'll see the logical name e.g. eno1. To activate your card:

> sudo ifconfig eno1 up

or as a selection:

> lspci -nn|grep Ethernet

To restart network manager:
> sudo service network-manager restart
or 
> sudo systemctl restart NetworkManager.service
or 
> sudo nmcli networking off
> sudo nmcli networking on
or
> sudo ifdown -a && sudo ifup -a
or graphically with 
> nmtui

#### Put driver together with kernel
Download the driver from https://downloadcenter.intel.com/download/15817, currently 3.2.4.2 (as shown in lshw -C above)
> make install in the src folder
> rmmod e1000e
> modprobe e1000e
> and to make the new driver survive a reboot update-initramfs -u

### Belgium eID

Copy link from website https://eid.belgium.be/en/linux-eid-software-installation

Then execute:
> wget https://eid.belgium.be/sites/default/files/software/eid-archive_2020.2_all_2.deb

Then check the PGP key and install

### Remote access
To install TeamViewer on a 64 bit system:

> wget https://download.teamviewer.com/download/linux/teamviewer_amd64.deb
> sudo dpkg -i teamviewer_amd64.deb

If you have errors, try first:
> sudo apt-get install -f

To run:
> teamviewer

## Community

https://community.linuxmint.com/software


## Fast terminal commands

### Search files

> find <dir> -iname <file*>

> locate -i <filename*>
> sudo updatedb

### Update
You can set updates to install automatically in the update manager, but if you are solving a problem, these commands can help to start with:
> sudo apt update 
> sudo apt upgrade

## Productivity Tools
### Create pop-up message with a timer in terminal 
> sleep 15m; zenity --question --text "Time to go!"; echo $?

### GIT in terminal
> sudo apt-get install git

### f.lux
Latest version: https://github.com/xflux-gui/fluxgui
Install instructions:

> sudo apt-get install python3-pexpect python3-distutils gir1.2-appindicator3-0.1 gir1.2-gtk-3.0
Download fluxgui, install system wide
> cd /tmp
> git clone "https://github.com/xflux-gui/fluxgui.git"
> cd fluxgui
> ./download-xflux.py
> sudo ./setup.py install --record installed.txt

Run flux
> fluxgui

### yEd Graph Editor
Download on https://www.yworks.com/products/yed/download#download

Change permissions of the .sh file before installing it:
> chmod +x yEd-3.17.2_64-bit_setup.sh
> ./yEd-3.17.2_64-bit_setup.sh


### AutoKey GTK


#### Google Translate
Install NodeJS:
> curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
> sudo apt-get install -y nodejs

Install Yarn
> curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
> echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
> sudo apt-get update
> sudo apt-get install yarn

Install DeepL Translator CLI
> yarn global add deepl-translator-cli
> deepl --version
oi

> deepl translate -t 'DE' 'How do you do?'

> echo 'How do you do?' | deepl translate -t 'DE'

> deepl detect 'Wie geht es Ihnen?'

> deepl -h
> deepl translate -h
> deepl detect -h




### Printer
When CUPS is giving problems:
> sudo systemctl stop cups-browsed
> sudo systemctl disable cups-browsed
Download driver from https://www.dell.com/support/home/en-us/drivers/driversdetails?driverid=074w2&oscode=1204a&productcode=dell-e525w-printer 
> unzip Printer_E525w_Driver_Dell_A00_Linux.zip
> sudo apt install ./dell-color-mfp-e525w_1.0-28_all.deb



