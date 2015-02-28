Post-Install Ubuntu Gnome 14.10
===============================

After you install brand new Ubuntu Gnome 14.10, the first thing you need to do is to update repositories and make sure you have the latest updates installed.

```
sudo apt-get update && sudo apt-get upgrade
```

Install the "ubuntu-restricted-extras" package. This will enable your Ubuntu to play popular file formats like mp3, avi, flash videos etc.

```
sudo apt-get install ubuntu-restricted-extras
```

PPAs
----

```
sudo add-apt-repository -y ppa:videolan/stable-daily
sudo add-apt-repository -y ppa:otto-kesselgulasch/gimp
sudo add-apt-repository -y ppa:webupd8team/java
```


* Sublime-text 3
* Mozilla

```
sudo add-apt-repository ppa:webupd8team/sublime-text-3 && sudo add-apt-repository ppa:ubuntu-mozilla-security/ppa
```

### Install

#### Dev environment

WIP http://gorails.com/setup/ubuntu

* Apache 2
* PHP 5
* MySql
* Filezilla
* Composer
* Redmine
* SonarQube
* php-console
* personnal projects with VHost
* apache2 config
* git config
* dot-files
* dev personnal directorys
* virtual boxes
* sublime-text 3 with package control
* chrome with some extensions

```
sudo apt-get install apache2 php5 mysql-server libapache2-mod-php5 php5-mysql
```

* Filezilla (yeah, sometimes...)

```
sudo apt-get install filezilla filezilla-common
```

* Git

If you don't already have a Github account, make sure to register. Then

```
sudo apt-get install git

git config --global color.ui true
git config --global user.name "{YOUR_NAME}"
git config --global user.email "{YOUR_@_MAIL.com}"
ssh-keygen -t rsa -C "{YOUR_@_MAIL.com}"

```

The next step is to take the newly generated SSH key and add it to your Github account. You want to copy and paste the output of the following command and paste it [here](https://github.com/settings/ssh).

```
cat ~/.ssh/id_rsa.pub
```

Once you've done this, you can check and see if it worked:

```
ssh -T git@github.com
```

You should get a message like this:

```
Hi {YOUR_GITHUB_NAME}! You've successfully authenticated, but GitHub does not provide shell access.
```

* Node.js

```
sudo add-apt-repository ppa:chris-lea/node.js
sudo apt-get update
sudo apt-get install nodejs
```

#### Usefull app

```
sudo apt-get install gimp vlc
```

#### Update installed stack

```
rails -v
ruby -v
sudo gem update
sudo composer self-update
```

#### Laptop config

Jupiter is No More, TLP Looks Like a Good Alternative

```
sudo add-apt-repository ppa:linrunner/tlp
sudo apt-get update
sudo apt-get install tlp tlp-rdw
```

Configz
-------

### Adding current user to www-data group

```
sudo adduser $LOGNAME www-data
```

### Add some empty files to models

```
cd /home/[YOUR_NAME]/Modèles

touch "new_file_CSS.css" && touch "new_file_HTML.html" && touch "new_file_JS.js" && touch "new_file_Markdown.md" && touch "new_file_PHP.php"
```
