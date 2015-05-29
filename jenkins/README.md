Jenkins
=======

* [Jenkins install by Pascal Martin (FR, 2011)](http://blog.pascal-martin.fr/post/integration-continue-jenkins-installation-configuration.html) and [second part](http://blog.pascal-martin.fr/post/integration-continue-jenkins-projet-php.html)
* [Install Jenkins on Ubuntu (EN, 2015)](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu)
* [Jenkins and PHP (EN)](https://wiki.jenkins-ci.org/display/JENKINS/Jenkins+and+PHP)
* [Gnome 3 Jenkins Indicator](https://github.com/philipphoffmann/gnome3-jenkins-indicator)
* [Continuous integration with Jenkins (EN, 2012)](http://www.sitepoint.com/continuous-integration-with-jenkins-1/) and [second part (EN, 2012)](http://www.sitepoint.com/continuous-integration-with-jenkins-2/)
* [Automate PSR-compliance through Jenkins](http://www.sitepoint.com/automate-psr-compliance-through-jenkins/)
* [Installing and securing Jenkins (EN, 2014)](http://www.sitepoint.com/installing-securing-jenkins/)

Install
-------

```shell
wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
sudo apt-get install jenkins
```

Setup a virtual host
--------------------

This configuration will setup Apache2 to proxy port 80 to 8080 so that you can keep Jenkins on 8080.

Create a file called `jenkins.conf` in `/etc/apache2/sites-available`

```
(sudo apt-get install apache2)
sudo a2enmod proxy
sudo a2enmod proxy_http
sudo service apache2 restart
```

```
<VirtualHost *:80>
    ServerName jenkins
    ServerAlias jenkins.dns.loc

    ProxyRequests Off
    <Proxy *>
        Order deny,allow

        # apache 2.2 permissions
        #Allow from all

        # apache 2.4 permissions
        Require all granted
    </Proxy>
    ProxyPreserveHost on
    ProxyPass / http://localhost:8080/ nocanon

    AllowEncodedSlashes NoDecode
</VirtualHost>
```

Finally:

```
sudo a2ensite jenkins
sudo service apache2 reload
```


Config
------

Before adding some plugins, install phing first:

```
pear channel-discover pear.phing.info
$> pear install [--alldeps] phing/phing

wget http://jenkins:8080/jnlpJars/jenkins-cli.jar
```

Then install plugins (and restart):

```
java -jar jenkins-cli.jar -s http://jenkins:8080/ install-plugin greenballs
java -jar jenkins-cli.jar -s http://jenkins:8080/ install-plugin build-keeper-plugin
java -jar jenkins-cli.jar -s http://jenkins:8080/ install-plugin htmlpublisher
java -jar jenkins-cli.jar -s http://jenkins:8080/ install-plugin checkstyle
java -jar jenkins-cli.jar -s http://jenkins:8080/ install-plugin cloverphp
java -jar jenkins-cli.jar -s http://jenkins:8080/ install-plugin dry
java -jar jenkins-cli.jar -s http://jenkins:8080/ install-plugin violations
java -jar jenkins-cli.jar -s http://jenkins:8080/ install-plugin phing
java -jar jenkins-cli.jar -s http://jenkins:8080/ install-plugin git

java -jar jenkins-cli.jar -s http://jenkins:8080 safe-restart
```

Other could be usefull plugins:

```
java -jar jenkins-cli.jar -s http://jenkins:8080/ install-plugin audit-trail
java -jar jenkins-cli.jar -s http://jenkins:8080/ install-plugin email-ext
java -jar jenkins-cli.jar -s http://jenkins:8080/ install-plugin instant-messaging
java -jar jenkins-cli.jar -s http://jenkins:8080/ install-plugin jdepend
java -jar jenkins-cli.jar -s http://jenkins:8080/ install-plugin plot
java -jar jenkins-cli.jar -s http://jenkins:8080/ install-plugin pmd
java -jar jenkins-cli.jar -s http://jenkins:8080/ install-plugin tasks
java -jar jenkins-cli.jar -s http://jenkins:8080/ install-plugin postbuild-task
java -jar jenkins-cli.jar -s http://jenkins:8080/ install-plugin build-keeper-plugin
java -jar jenkins-cli.jar -s http://jenkins:8080/ install-plugin performance
java -jar jenkins-cli.jar -s http://jenkins:8080/ install-plugin monitoring

java -jar jenkins-cli.jar -s http://jenkins:8080 safe-restart
```
