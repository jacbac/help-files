References
----------

* [DevEnv on Mac](http://codepen.io/rafhun/blog/setting-up-a-devenv-on-a-mac)
* [Install Book](http://sourabhbajaj.com/mac-setup/)
* [Mac Dev Setup](https://github.com/nicolashery/mac-dev-setup)
* [OS X Yosemite with AMP and Homebrew](https://medium.com/@raureif/os-x-yosemite-how-to-set-up-apache-mysql-and-php-with-homebrew-4bc236d7d9fa)

Dev tools
---------

### Xcode

Install Xcode from the AppStore, then:
```
xcode-select --install
```

### Homebrew

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### iTerm2 with zsh:

```
brew tap Caskroom/cask
brew install Caskroom/cask/iterm2
```

And finally zsh and OhMyZSH to getting additional functionality

```
brew install zsh zsh-completions
curl -L https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh | sh
```

edit the .zshrc by opening the file in a text editor:
```
ZSH_THEME="agnoster"

DEFAULT_USER="{YOUR_USER}"

plugins=(git colored-man colorize brew osx symfony2 dircycle common-aliases npm nyan)
```

### Sublime-Text

Open sublime-text in terminal with alias `subl`:
```
ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/subl
```

### Various

Install last version with homebrew:

```
brew install curl
brew install wget
brew install git
```

### Pear

Necesarry for PHPCS install.

Check if you have it: pear version. If not, move into and get pear.phar:

```
cd /usr/local
[sudo] curl -O  http://pear.php.net/go-pear.phar
```

Install it:

```
sudo php -d detect_unicode=0 go-pear.phar
```

Click yes a couple of times during the install

Add PEAR to your PATH:

```
vim ~/.zshrc
export PATH="/Users/toog/pear/bin:$PATH"
source ~/.zshrc
```

Verify with `pear version`

### Packages managers

* [composer](https://getcomposer.org/):
```
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/bin/composer
vim ~/.zshrc
and add to .zshrc
alias composer="php /usr/bin/composer/composer.phar"
```

* [nodejs](https://nodejs.org/):
```
brew install node
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

### Adding current user to _www group

```
http://prasanthj86.blogspot.fr/2011/11/mac-os-x-adding-user-groups-and.html
```

### MAMP

Apache 2.4 and PHP 5.5 are packaged with Mac OS X 10.10. We prefer to keep them. We install MySQL with brew and secure the MySQL installation:

```
brew install mysql
mysql_secure_installation
```

Set a root password, delete test account, etc.

#### PHP

In `/etc/apache2/httpd.conf`, uncomment lines to load the php library:
```
LoadModule php5_module libexec/apache2/libphp5.so
```

Prevent the apache notice "Could not reliably determine the server's fully qualified domain name" and redefine in `/etc/apache2/httpd.conf`:

ServerName localhost

```
sudo cp /etc/php.ini.default /etc/php.ini
sudo vim /etc/php.ini
set
    date.timezone = Europe/Paris

```

### PHPMyAdmin

To make working with MySQL databases a little easier we install phpmyadmin for the server through Homebrew. Start the installation by running

```
brew tap homebrew/php
brew install phpmyadmin
```

You get some instructions once the installation has finished. Follow these by adding the necessary configuration to the httpd.conf. Do not forget to restart Apache after changing the configuration: sudo apachectl restart.

Then open in Sublime-text the file indicated at the end of the installation (subl /usr/local/etc/phpmyadmin.config.inc.php) and add your own blowfish secret. You can generate a blowfish secret [here](http://www.question-defense.com/tools/phpmyadmin-blowfish-secret-generator).

By the way, you can uncomment lines:

```
$cfg['MaxRows'] = 50;
```

To make phpmyadmin work we need to fix the `2002 MySQL socket error` by running these two commands:

```
sudo mkdir /var/mysql
sudo ln -s /tmp/mysql.sock /var/mysql/mysql.sock
```

### XDebug

[See here](https://www.computersnyou.com/3416/setup-xdebug-macosx-10-10-yosemite/)

### Tree

```
brew install tree
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

### Generate an SSH key

[With some helps from Github](https://help.github.com/articles/generating-ssh-keys/)

OS X & App Configurations
-------------------------

### The Dock

To get the dock better organized some spacing can help. One can add empty dock elements that act as spacers through the command line by running this command:
```
defaults write com.apple.dock persistent-apps -array-add '{tile-data={}; tile-type="spacer-tile";}'
```

as many times as you want spacers. Then to make them appear restart the dock by running:
```
killall Dock
```

### Finder

Set some common options for the finder:

Show dotfiles in Finder by default:
```
defaults write com.apple.finder AppleShowAllFiles TRUE
```

Show status bar in Finder by default:
```
defaults write com.apple.finder ShowStatusBar -bool true
```

Use column view in all Finder windows by default:
```
defaults write com.apple.finder FXPreferredViewStyle Clmv
```

Avoid creation of .DS_Store files on network volumes:
```
defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool true
```

Allow text selection in Preview/Quick Look
```
defaults write com.apple.finder QLEnableTextSelection -bool true
```

### Safari

Enable the Develop menu and the Web Inspector:

```
defaults write com.apple.Safari IncludeDevelopMenu -bool true
defaults write com.apple.Safari WebKitDeveloperExtrasEnabledPreferenceKey -bool true
defaults write com.apple.Safari "com.apple.Safari.ContentPageGroupIdentifier.WebKit2DeveloperExtrasEnabled" -bool true
```

Add a context menu item for showing the Web Inspector in web views:
```
defaults write NSGlobalDomain WebKitDeveloperExtras -bool true
```

Update packages
---------------

* composer: `composer self-update`
* npm: `npm install npm -g`
* ruby: `gem update` or `sudo gem update --system`
* homebrew: `brew update`
* homebrew installed packages: `brew upgrade`
$ pear: `pear upgrade pear`
$ pear installed packages: `pear upgrade`
