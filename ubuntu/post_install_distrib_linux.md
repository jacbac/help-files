Post-Install Ubuntu Gnome 14.10
===============================

After you install brand new Ubuntu Gnome 14.10, the first thing you need to do is to update repositories and make sure you have the latest updates installed.

```
sudo apt-get update && sudo apt-get upgrade
```

PPAs
----

```shell
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
* `sublime-text-installer`: sublime-text 3
* `oracle-java8-installer`: official Java installer
* `xpad`: post-it

```
sudo apt-get install vlc gimp bleachbit oracle-java8-installer xpad htop
```

### Common codec

* `ubuntu-restricted-extras`: play popular file formats like mp3, avi, flash videos etc.

```
sudo apt-get install ubuntu-restricted-extras
```

### With direct download

* `google-chrome`: google's browser
```
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb && sudo dpkg -i google-chrome-stable_current_amd64.deb && rm -f google-chrome-stable_current_amd64.deb
```

* `enpass`: secured passwords manager
```
cd /path_to/download_directory
chmod +x EnpassInstaller
sudo apt-get install libxss1
./EnpassInstaller
```

* `birdie`: twitter client
```
[Download from official site](http://www.birdieapp.eu/)
```

Dev tools
---------

* `vim`
* `tree`
* `git`
* `apache2`
* `php5`
* `phpmyadmin`: mysql admin
* `php5-cli`, `php5-curl`, `php-pear` (for pecl installations), `php5-intl`, `php5-mcrypt`, `php5-mysql`, `php5-imagick`, `php5-dev` (needed by xdebug)
* `make`, `build-essential`
* `filezilla`: FTP
* `mysql-workbench`: mysql admin

```
sudo apt-get install vim curl tree git apache2 mysql-server php5 libapache2-mod-php5 phpmyadmin php5-cli php5-curl php-pear php5-intl php5-mcrypt php5-mysql php5-imagick php5-dev make build-essential ilezilla mysql-workbench
```

* `zsh` with `oh-my-zsh`:
```
sudo apt-get install zsh
chsh -s /bin/zsh
wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O - | sh
then update .zshrc with `dot-files` config exemple
reboot if needed
```

* `composer`:
```
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
```

* `phpcs` (PHP Code Sniffer):
```
sudo pear install PHP_CodeSniffer
```

* `phpcs` Symfony2 Coding Standard:
```
pear config-show | grep php_dir
cd /path/to/pear/PHP/CodeSniffer/Standards
git clone git://github.com/escapestudios/Symfony2-coding-standard.git Symfony2
phpcs --config-set default_standard Symfony2
```

* `phpcs-fixer` (PHP CS Fixer):
```
wget http://get.sensiolabs.org/php-cs-fixer.phar -O php-cs-fixer
sudo chmod a+x php-cs-fixer
sudo mv php-cs-fixer /usr/local/bin/php-cs-fixer
```

* `phpmd` (PHP Mess Detector), `phpdp` (PHP Depend):
```
sudo pear channel-discover 'pear.phpmd.org' && sudo pear channel-discover 'pear.pdepend.org'
sudo pear install --alldeps 'phpmd/PHP_PMD'
```

* `nodejs`:
```
curl -sL https://deb.nodesource.com/setup | sudo bash -
sudo apt-get install -y nodejs
```

* `xdebug`:
```
sudo pecl install xdebug
sudo vim /etc/php5/apache2/php.ini
set
    zend_extension="/usr/lib/php5/20121212/xdebug.so"
sudo service apache2 restart
```

* `phpunit`:
```
wget https://phar.phpunit.de/phpunit.phar
chmod +x phpunit.phar
sudo mv phpunit.phar /usr/local/bin/phpunit
phpunit --version
    PHPUnit x.y.z by Sebastian Bergmann and contributors.
```

* `rails` with `ruby`: [Look at this setup](https://gorails.com/setup/ubuntu/14.10)


Config
------

### Vim

* `Vundle`:
```
git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim
then update .vimrc with `dot-files` config exemple
```

* `YouCompleteMe`:
```
sudo apt-get install build-essential cmake python-dev
cd ~/.vim/bundle/YouCompleteMe
./install.sh --clang-completer
```

### Git

```
update .gitconfig with `dot-files` config exemple
```

### Sublime-Text 3

* [Install Package control](https://packagecontrol.io/installation)
* [Plugin Side​Bar​Enhancements](https://packagecontrol.io/packages/SideBarEnhancements)
* [Plugin Alignment](https://packagecontrol.io/packages/Alignment)
* [Plugin Doc​Blockr](https://packagecontrol.io/packages/DocBlockr)
* [Plugin Git​Gutter](https://packagecontrol.io/packages/GitGutter)
* [Plugin Phpcs](https://packagecontrol.io/packages/Phpcs)
* [Plugin Markdown Preview](https://packagecontrol.io/packages/Markdown%20Preview)
* [Syntax Highlighting LESS](https://packagecontrol.io/packages/LESS)
* [Syntax Highlighting Behat](https://packagecontrol.io/packages/Behat)
* [Syntax Highlighting Markdown](https://packagecontrol.io/packages/Markdown%20Extended)
* [Theme Monokai Extended](https://packagecontrol.io/packages/Monokai%20Extended)

```
update User Preferences.sublime-settings with `dot-files` config exemple
update User phpcs.sublime-settings with `dot-files` config exemple
```

### MySQL

```
sudo mysql_secure_installation
```

### Adding current user to www-data group

```
sudo adduser $LOGNAME www-data
```

### PHP

```
sudo vim /etc/php5/apache2/php.ini
set
    date.timezone = Europe/Paris

```

### Apache2 mods

```
sudo a2enmod rewrite headers deflate expires setenvif
sudo service apache2 restart
```

### Auto-mount ntfs partitions

[Serious Askubuntu answer](http://askubuntu.com/questions/46588/how-to-automount-ntfs-partitions)

### Generate an SSH key

[With some helps from Github](https://help.github.com/articles/generating-ssh-keys/)

Clean-up
--------

```
sudo apt-get -f install && sudo apt-get autoremove && sudo apt-get -y autoclean && sudo apt-get -y clean
```


Update installed stack
----------------------

* packages: `sudo apt-get update`
* composer: `sudo composer self-update`
* php-cs-fixer: `sudo php-cs-fixer self-update`
* pear: `sudo pear channel-update pear.php.net && sudo pear upgrade-all`
* ruby: `sudo gem update`


Other
-----

* Update if needed `/etc/hosts` and add personnal projects VHost in `/etc/apache2/sites-available`...
