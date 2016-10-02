Post-Install Ubuntu Gnome 16.04
===============================

After you install brand new Ubuntu Gnome 16.04 (OK 2016/10/02), the first thing you need to do is to update repositories and make sure you have the latest updates installed.

```shell
sudo apt-get update && sudo apt-get upgrade
```

PPAs
----

```shell
sudo add-apt-repository -y ppa:videolan/stable-daily &&
sudo add-apt-repository -y ppa:otto-kesselgulasch/gimp &&
sudo add-apt-repository -y ppa:webupd8team/java &&
sudo apt-get update
```

Basic tools
-----------

* `vlc`: media player
* `gimp`: photo/image editor
* `bleachbit`: cleaning utility
* `oracle-java8-installer`: official Java installer
* `xpad`: post-it
* `htop`: linux process viewer
* `imagemagick`: image editing

```
sudo apt-get install vlc gimp bleachbit oracle-java8-installer xpad htop imagemagick
```

### Common codec

* `ubuntu-restricted-extras`: play popular file formats like mp3, avi, flash videos etc.

```
sudo apt-get install ubuntu-restricted-extras
```

### With direct download

* `google-chrome`: google's browser
```
goto https://www.google.fr/chrome/browser/desktop/
download last version
double click on .deb file downloaded
```

* `sublime-text-3`: ide
```
goto https://www.sublimetext.com/3
download last version
double click on .deb file downloaded
```

* `enpass`: secured passwords manager
```
goto https://www.enpass.io/
download last version
cd /path_to/download_directory
chmod +x EnpassInstaller
sudo apt-get install libxss1 lsof
./EnpassInstaller
```

* `birdie`: twitter client
```
goto http://birdieapp.github.io/
download last version
double click on .deb file downloaded
```

Dev tools
---------

* `vim`
* `curl`, `tree`
* `git`, `gitk`: git
* `make`, `build-essential`
* `filezilla`: FTP

```
sudo apt-get install vim curl tree git gitk make build-essential filezilla
```

Lamp tools
----------

* `apache2`
* `mysql` and `mysql-workbench`: mysql
* `php 7`

https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu-16-04

```
sudo apt-get install apache2
sudo apache2ctl configtest
```

if a warning emerge (like ``), add to

```
sudo nano /etc/apache2/apache2.conf
add to bottom of the file:
ServerName localhost
save it and redo sudo apache2ctl configtest
then test http://localhost/ or http://127.0.0.1/
```
```
sudo apt-get install mysql-server
sudo mysql_secure_installation
responses : no no yes yes yes yes
service mysql status
sudo apt-get install mysql-workbench
```

```
sudo apt-get install php libapache2-mod-php php-mcrypt php-mysql
sudo apt-get install php7.0-cli php7.0-curl
```

* `phpmyadmin`: mysql admin

```
sudo apt-get install phpmyadmin apache2-utils
```

https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-on-ubuntu-12-04

### Security

http://www.leshirondellesdunet.com/pare-feu-ufw

### Terminal / Shell

* [`zsh` with `oh-my-zsh`](http://ohmyz.sh/):
```
sudo apt-get install zsh
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
then update .zshrc with `dot-files` config example
reboot if needed
```

### Packages managers

* [composer](https://getcomposer.org/):
```
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
```

* [nodejs](https://nodejs.org/):
```
# Note the new setup script name for Node.js v0.12
sudo apt-get update
sudo apt-get install -y nodejs npm
```

### Scaffolding Tools

* [Yeoman](http://yeoman.io/) (global):
```
$ [sudo] npm install -g yo
```

### Task Runners / System Builders

* [gulp](http://gulpjs.com/) (global):
```
$ [sudo] npm install -g gulp
```

* [brunch](http://brunch.io/) (global):
```
$ [sudo] npm install -g brunch
```

* [grunt](http://gruntjs.com/) (global):
```
$ [sudo] npm install -g grunt-cli
```

### CSS Extension Languages

* [LESS](http://lesscss.org/)
```
$ [sudo] npm install -g less
```

* [SASS](http://sass-lang.com/)
```
$ [sudo] npm install -g node-sass
```

### Debugging Tools

* `xdebug`:
```
sudo apt-get install php-xdebug
http://www.dieuwe.com/blog/xdebug-ubuntu-1604-php7
```

### Testing Tools / Linter

* `phpunit`:
```
wget https://phar.phpunit.de/phpunit.phar
chmod +x phpunit.phar
sudo mv phpunit.phar /usr/local/bin/phpunit
phpunit --version
    PHPUnit x.y.z by Sebastian Bergmann and contributors.
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

### QA & Monitoring tools

* `phpmetrics`:
```
composer global require 'halleck45/phpmetrics'
```

Then make the command `phpmetrics` accessible:

```
Simply add this directory to your PATH in your ~/.bash_profile (or ~/.bashrc or ~/.zshrc) like this:

export PATH=~/.composer/vendor/bin:$PATH
```

And analyse with:

```
phpmetrics --report-html=myreport.html /path/of/your/sources
```

### Others Languages & Frameworks

* `ruby` with `rails`: [Look at this setup](https://gorails.com/setup/ubuntu/14.10)


Config
------

### Vim

* `Vundle`:
```
git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim
then update ~/.vimrc with `dot-files` config example
vim +PluginInstall +qall
```

* `YouCompleteMe`:
```
sudo apt-get install build-essential cmake python-dev
cd ~/.vim/bundle/YouCompleteMe
./install.sh --clang-completer
```

### Git

```
update .gitconfig with `dot-files` config example
```

### Sublime-Text 3

* [Install Package control](https://packagecontrol.io/installation)
* [Plugin Side​Bar​Enhancements](https://packagecontrol.io/packages/SideBarEnhancements)
* [Plugin Alignment](https://packagecontrol.io/packages/Alignment)
* [Plugin Doc​Blockr](https://packagecontrol.io/packages/DocBlockr)
* [Plugin Git​Gutter](https://packagecontrol.io/packages/GitGutter)
* [Plugin PHPNamespace](https://packagecontrol.io/packages/PhpNamespace)
* [Plugin Phpcs](https://packagecontrol.io/packages/Phpcs)
* [Plugin SublimeLinter-php](https://packagecontrol.io/packages/SublimeLinter-php)
* [Plugin SublimeLinter-jshint](https://packagecontrol.io/packages/SublimeLinter-jshint). Prerequisite: `npm install -g jshint`
* [Plugin SublimeLinter-csslint](https://packagecontrol.io/packages/SublimeLinter-csslint). Prerequisite: `npm install -g csslint`
* [Plugin SublimeLinter-json](https://packagecontrol.io/packages/SublimeLinter-json)
* [Plugin Markdown Preview](https://packagecontrol.io/packages/Markdown%20Preview)
* [Plugin Color Highlighter](https://packagecontrol.io/packages/Color%20Highlighter)
* [Syntax Highlighting LESS](https://packagecontrol.io/packages/LESS)
* [Syntax Highlighting SASS](https://packagecontrol.io/packages/Sass)
* [Syntax Highlighting Behat](https://packagecontrol.io/packages/Behat)
* [Syntax Highlighting Twig](https://packagecontrol.io/packages/Twig)
* [Syntax Highlighting Markdown](https://packagecontrol.io/packages/Markdown%20Extended)
* [Theme Monokai Extended](https://packagecontrol.io/packages/Monokai%20Extended)
* [FR Dictionnaries](http://blog.smarchal.com/correcteur-orthographique-francais-sublime-text/)

```
update User Preferences.sublime-settings with `dot-files` config example
update User phpcs.sublime-settings with `dot-files` config example
update sublime-text close/save tabs buttons with new pngs. See `help-files/sublime` example
update gutter themes: open Command Palette, choose `SublimeLinter: Choose Gutter Theme`, select `Circle`.
update mark style: open Command Palette, choose `Sublime Linter: Choose Mark Style`, select `Outline`.
```

### Adding current user to www-data group

```
sudo adduser $LOGNAME www-data
```

### PHP

```
sudo vim /etc/php7/apache2/php.ini
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
* npm: `sudo npm install npm -g`
* phpunit: `sudo phpunit --self-update`
* php-cs-fixer: `sudo php-cs-fixer self-update`
* pear: `sudo pear channel-update pear.php.net && sudo pear upgrade-all`
* ruby: `sudo gem update`
* gem: `sudo gem update --system`

Other
-----

* Update if needed `/etc/hosts` and add personnal projects VHost in `/etc/apache2/sites-available`...
