Post-Install Ubuntu Gnome 14.10
===============================

After you install brand new Ubuntu Gnome 14.10, the first thing you need to do is to update repositories and make sure you have the latest updates installed.

```
sudo apt-get update && sudo apt-get upgrade
```

PPAs
----

```
sudo add-apt-repository -y ppa:videolan/stable-daily
sudo add-apt-repository -y ppa:otto-kesselgulasch/gimp
sudo add-apt-repository -y ppa:webupd8team/java
sudo add-apt-repository -y ppa:webupd8team/sublime-text-3
sudo add-apt-repository -y ppa:webupd8team/y-ppa-manager

sudo apt-get update
```

Basic tools
-----------

* `vlc`: media player
* `gimp`: photo/image editor
* `bleachbit`: cleaning utility
* `ubuntu-restricted-extras`: play popular file formats like mp3, avi, flash videos etc.
* `sublime-text-installer`
* `oracle-java8-installer`: official Java installer
* `xpad`: post-it

```
sudo apt-get install vlc gimp bleachbit ubuntu-restricted-extras oracle-java8-installer xpad htop
```

### With direct download

* `google-chrome`: google's browser
* `enpass`: secured passwords manager

```
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb && sudo dpkg -i google-chrome-stable_current_amd64.deb && rm -f google-chrome-stable_current_amd64.deb
```

```
cd <download_directory>
chmod +x EnpassInstaller
sudo apt-get install libxss1
./EnpassInstaller
```

Dev tools
---------

* `vim`
* `tree`
* `git`
* `apache2`
* `mysql-workbench`
* `php5`
* `phpmyadmin`
* `filezilla`
* `php5-cli`: 
* `php5-curl`:
* `php-pear`: for pecl installations
* `php5-intl`:
* `php5-mcrypt`:
* `php5-mysql`:
* `php5-imagick`

```
sudo apt-get install vim curl tree git apache2 mysql-server php5 libapache2-mod-php5 phpmyadmin php5-cli php5-curl php-pear php5-intl php5-mcrypt php5-mysql php5-imagick filezilla mysql-workbench
```

* `zsh`:
```
sudo apt-get install zsh 
chsh -s /bin/zsh
wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O - | sh
```

* `composer`: 
```
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer
```

* `nodejs`: 
```
curl -sL https://deb.nodesource.com/setup | sudo bash -
sudo apt-get install -y nodejs
```

* `xdebug`: 
```
pecl install xdebug
zend_extension="/usr/local/php/modules/xdebug.so"
```

Clean-up
--------

```
sudo apt-get -f install && sudo apt-get autoremove && sudo apt-get -y autoclean && sudo apt-get -y clean
```

Config
------

### Git

```
git config --global color.ui true
git config --global user.name "{YOUR_NAME}"
git config --global user.email "{YOUR_@_MAIL.com}"
```

### MySQL

```
sudo mysql_secure_installation
```

### Adding current user to www-data group

```
sudo adduser $LOGNAME www-data
```

Update installed stack
----------------------

```
sudo gem update
sudo composer self-update
```

Help and resources
------------------

[Ubuntu setup](http://gorails.com/setup/ubuntu)

Other
-----

* personnal projects with VHost
* apache2 config
* git config
* dot-files
* virtual boxes
* chrome with some extensions
