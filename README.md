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

## Resource Management Tools
### Install Smartgit
SmartGit is a version control management software. 

> sudo apt-get install gdebi
> wget http://www.syntevo.com/static/smart/download/smartgit/smartgit-17_0_1.deb
> sudo gdebi smartgit-17_0_1.deb

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


