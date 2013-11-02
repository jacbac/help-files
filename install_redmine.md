Redmine
=======

[http://wiki.bitnami.com/Applications/BitNami_Redmine](http://wiki.bitnami.com/Applications/BitNami_Redmine)

Install
-------

### Prerequisites

Ubuntu 13.04
MySql
PHPMyAdmin

### Installing Redmine

Download BitNami Redmine Stacks [here]()


### Launch Redmine

> cd /home/dev/worktools/redmine-2.3.3-1

> ./ctlscript.sh start

Open in your browser

> http://localhost:8080/redmine/

### Config

#### How to change the default URL to the root?

WIP

On Linux and OS X, you have to change

```
installdir/apps/redmine/conf/httpd-app.conf
installdir/apps/redmine/conf/httpd-prefix.conf
```

files to modify the "/redmine" url to the root url.

You can find below a configuration example. Please take into account that your current redmine.conf file may be a little bit different. You should modify the "installdir/apps/redmine/config/httpd-app.conf" file according to the changes that you can see in bold (the line SetEnv RAILS_RELATIVE_URL_ROOT "/redmine" must be removed too):

```
<Directory "installdir/apps/redmine/htdocs/public">
    Options -MultiViews
    <IfVersion < 2.3 >
      Order allow,deny
      Allow from all
    </IfVersion>
    <IfVersion >= 2.3>
      Require all granted
    </IfVersion>  
</Directory>

PassengerPreStart http://127.0.0.1:8080/
```

You should modify the "installdir/apps/redmine/conf/httpd-prefix.conf" file according to the changes that you can see in bold:
DocumentRoot "installdir/apps/redmine/htdocs/public/"

Include installdir/apps/redmine/conf/httpd-app.conf

Then restart the Apache server

> sudo service apache2 restart
