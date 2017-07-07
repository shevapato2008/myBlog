---
layout: post
title: Jekyll Installation on Ubuntu 16.04
meta: Go over the commands for Jekyll 3.5 installation on Ubuntu 16.04.
comments: true
mathjax: false
---

This post goes over the commands for Jekyll 3.5 installation on Ubuntu 16.04.

[Jekyll][Jekyll] is a simple, blog-aware, static site generator for personal, project, or organization sites. Written in Ruby by Tom Preston-Werner, GitHub's co-founder, it is distributed under an open source license.

<br>

## Step 1 - Install Ruby & Jekyll
---

Update package list to ensure we get the latest information.
```shell
$ sudo apt-get update
```

Then install Ruby and its development libraries as well as [`make`][mk] and [`gcc`][gcc] so that Jekyll's libraries will compile once we install Jekyll.

```shell
$ sudo apt-get install ruby ruby-dev make gcc
```

Use Ruby's [`gem`][gem] package manager to install Jekyll as well as Bundler to manage Gem dependencies.

```shell
$ sudo gem install jekyll bundler
```
Note:
* [`make`][mk] package: a utility for directing compilation
* [`gcc`][gcc] package: GNU C compiler
* [`gem`][gem] package manager: [RubyGems][RubyGems] is a package manager for the Ruby programming language that provides a standard format for distributing Ruby programs and libraries (in a self-contained format called a "gem"), a tool designed to easily manage the installation of gems, and a server for distributing them.

<br>

## Step 2 - Check the Firewall
---

We'll begin by checking the firewall status to see if it’s enabled. If so, we’ll ensure traffic to our site is permitted so we will be able to view our development site in a web browser.

```shell
$ sudo ufw status
```

Use the following commands to turn on/off the firewall.

```shell
$ sudo ufw enable
$ sudo ufw disable
```

We’ll need to open port 4000, the default port for the Jekyll development server.

```shell
$ sudo ufw allow 4000
```

Double-check the status:

```shell
$ sudo ufw status
```

Now our firewall rules look like:
```
To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere
4000                       ALLOW       Anywhere
```

<br>

## Step 3 - Start the Jekyll Server
---

Clone the github repository to local machine. Go to the specific folder and start Jekyll server by running the following commands.

```shell
$ jekyll serve
```

<br>

## Reference
---

[Jekyll]: https://en.wikipedia.org/wiki/Jekyll_(software) "Jekyll in Wikipedia"
[RubyGems]: https://en.wikipedia.org/wiki/RubyGems "RubyGems in Wikipedia"
[mk]: https://packages.ubuntu.com/trusty/make "make package in Ubuntu"
[gcc]: https://packages.ubuntu.com/search?keywords=gcc "gcc package in Ubuntu"
[gem]: https://rubygems.org/ "rubyGems.org"

[How to Set Up a Jekyll Development Site on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-jekyll-development-site-on-ubuntu-16-04#conclusion)
