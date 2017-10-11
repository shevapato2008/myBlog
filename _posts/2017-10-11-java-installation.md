---
layout: post
title: Java Installation on Ubuntu 16.04
meta: This post helps install Java under Linux environment.
comments: true
mathjax: true
---

There are basically two standard types of installation: JRE (Java Runtime Environment) and JDK (Java Development Kit).
+ JRE enables the ability to create Java applications for different types of deployments using minimal core tools.
+ JDK is a fully loaded development kit that has everything that JRE has plus additional resources to create/secure applications and applets.

<br>

## Check the current version of Java installed.
---
Make sure that the server is fully updated.
```shell
$ sudo apt updated
```
Check what version of Java is currently installed or if it is not installed.
```shell
$ java -version
```

<br><br>

## Method 1: Install Java Open JRE or JDK
---
Choose the type of Java installation you want.
```shell
$ sudo apt install default-jdk
$ sudo apt install default-jre
```
Or alternatively, install Java with Open JRE 7 and JDK 7. (Obsolete)
```shell
$ sudo apt install openjdk-7-jre
$ sudo apt install openjdk-7-jdk
```
However, openjdk-7-* would not work any more.
![openjdk-7-jre error message]({{site.baseurl}}/assets/images/2017-10-11/1.png)
![openjdk-7-jdk error message]({{site.baseurl}}/assets/images/2017-10-11/2.png)

<br><br>

## Method 2: Install Java using PPA Repository (Recommended)
---
Another alternative Java installation is with Oracle JRE and JDK. However, we would need to install additional repositories for a proper installation.
```shell
$ sudo apt-get install software-properties-common
$ sudo add-apt-repository ppa:webupd8team/java
```
Then you will need to fully update the system.
```shell
$ sudo apt-get update
```
You can install several versions of Java by using the following commands.
```shell
$ sudo apt-get install oracle-java7-installer
$ sudo apt-get install oracle-java8-installer
$ sudo apt-get install oracle-java9-installer
```
Java 8 and 9 would basically work fine. But [Oracle JDK7 itself is no longer hosted in the PPA because that's not allowed by the new Java license](http://www.webupd8.org/2012/01/install-oracle-java-jdk-7-in-ubuntu-via.html). You will have to find alternative sources to download the corresponding installation package. You might find the following mirrors usable: [Source1](http://ftp.osuosl.org/pub/funtoo/distfiles/oracle-java/ "Mirror hosted by Oregon State University"), [Source2](http://www.360sdn.com/ide-develop-tool/2016/0919/9262.html "360sdn Mirror"). jdk-7u80-linux-x64.tar.gz is the installation file needed for a Ubuntu 16.04 64bit machine.

After manually downloading the JDK tar.gz archive, you can place it under `/var/cache/oracle-jdk7-installer` and install it using the previous command.
```shell
$ sudo cp /Downloads/jdk-7u80-linux-x64.tar.gz /var/cache/oracle-jdk7-installer
$ cd /var/cache/oracle-jdk7-installer
$ tar -xvzf jdk-7u80-linux-x64.tar.gz
$ sudo apt-get install oracle-java7-installer
```
**Note**: Explanation on file extraction command `tar -xvzf *.tar.gz`<br>
+ **`f`**: this must be the last flag of the command, and the tar <span style="font-weight: bold;">f</span>ile must be immediately after. It tells tar the name and path of the compressed file.
+ **`z`**: tells tar to decompress the archive using g<span style="font-weight: bold;">z</span>ip.
+ **`x`**: tar can collect files or e<span style="font-weight: bold;">x</span>tract them. `x` does the latter.
+ **`v`**: makes tar talk a lot. <span style="font-weight: bold;">V</span>erbose output shows you all the files being extracted.

Check Java version.
```shell
$ java -version
```
![java version]({{site.baseurl}}/assets/images/2017-10-11/3.png)

This means Java 9 is currently the default version.

<br><br>

## Java Version Configuration
---
Check your alternatives with the following command.
```shell
$ sudo update-alternatives --config java
```
![java alternatives]({{site.baseurl}}/assets/images/2017-10-11/4.png)

As shown above, java 9 has been switched to java 7.

<br><br>

## Setting Java Environment Variables
---
Since many programs nowadays need a JAVA_HOME environment variable to work properly, we will need to find the appropriate path to make these changes. With the following command, you can view all java installs and their paths.

**Method 1: Manual Setup**
```shell
$ sudo update-alternatives --config java
```
To edit the environment file, you can open `/etc/environment` using any text editor like `nano` or `gedit`.
```shell
$ sudo nano /etc/environment
$ sudo gedit /etc/environment
```
Add the following line:
```
export JAVA_HOME="/usr/lib/jvm/java-9-oracle"
```
The java path could be different. Then use `source` to load the variables, by running the following command.
```shell
$ source /etc/environment
```
The check the variable.
```shell
echo $JAVA_HOME
```
**Note**:<br>
Usually most linux systems source /etc/environment by default. If your sytem does not do that add the following line to `~/.bashrc`.

**Method 2: Automatic Setup**

To automatically set up the Java 7 environment variables, you can install the following package:
```shell
$ sudo apt-get install oracle-java7-set-default
```
If you've already installed `oracle-java8-set-default` or `oracle-java9-set-default`, they will be automatically removed when installing oracle-java7-set-default (and the environment variables will be set for Oracle Java 7 instead).

That’s it. You have successfully installed Java JDK on your Ubuntu 16.04. You can now install JAVA based software such as Tomcat, GitBucket, GlassFish 4 and many more.

<br><br>

## Removing Oracle Java
---
If you don't want to use Oracle Java (JDK) 7 anymore on your Ubuntu / Linux Mint computer and want to go back to OpenJDK, all you have to do is remove the Oracle JDK7 Installer and the previous Java (OpenJDK, etc.) version will be used:
```shell
$ sudo apt-get remove oracle-java7-installer
```

<br><br>

## Reference
---
+ [Install Oracle Java 7 in Ubuntu or Linux Mint via PPA Repository](http://www.webupd8.org/2012/01/install-oracle-java-jdk-7-in-ubuntu-via.html)
+ [Install Java (JRE Or JDK) On Ubuntu 16.04](https://www.atlantic.net/community/howto/install-java-jre-jdk-on-ubuntu-16-04/)
+ [How to Install Java on Ubuntu 16.04](https://www.rosehosting.com/blog/how-to-install-java-on-ubuntu-16-04/)

**More on Trouble Shooting**<br>
+ [AskUbuntu] [How to set JAVA_HOME for Java?](https://askubuntu.com/questions/175514/how-to-set-java-home-for-java)
+ [AskUbuntu] [What command do I need to unzip/extract a .tar.gz file?](https://askubuntu.com/questions/25347/what-command-do-i-need-to-unzip-extract-a-tar-gz-file)
