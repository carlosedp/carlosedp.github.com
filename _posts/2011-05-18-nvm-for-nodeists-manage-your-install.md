---
layout: post
title: NVM for Nodeists. Managing your Node.js install
---

Based on [Giles Fabio's post](http://gillesfabio.com/blog/2011/03/01/rvm-for-pythonistas-virtualenv-for-rubyists/), if you are in the new Node.js train, here is a guide on building a lean Node.js development environment.

# Installation

First, install git in your environment. Since I'm on a Mac, I use the fantastic [homebrew](http://mxcl.github.com/homebrew/) package manager. It's just a `brew install git` away.

Download nvm (Node Version Manager):
    git clone git://github.com/creationix/nvm.git ~/.nvm

... and source it in your $HOME/.bashrc:
    . ~/.nvm/nvm.sh

Reload your session or source `. ~/.nvm/nvm.sh`.

# Managing multiple interpreters

NVM keeps all Node.js interpreters in it's own dir ($HOME/.nvm).

First sync nvm so it can 'check' all Node.js versions:
    nvm sync

To download, compile and install Node.js version 0.4.6 for example, run:
    nvm install v0.4.6

or to install the latest version, run:
    nvm install latest

Then, when finished installing, use the installed version:
    nvm use v0.4.6

To check all installed and available versions, run:
    nvm ls

And then, set the version as default (so there is no need to 'nvm use' it everytime)
    nvm alias default v0.4.6

# Managing project dependencies

NVM installs NPM, Node Package Manager, used to install Node.js modules.

NPM was recently updated to version 1.0. In this new version, it installs the package deps in a `node_modules` dir in the same project where you ran it.

To manage dependencies, create a `package.json` for your project:

{% highlight javascript %}
    {
      "name": "Project Name",
      "description": "Project Description.",
      "version": "0.0.1",
      "homepage": "http://#",
      "author": "You",
      "private": true,
      "dependencies": {
        "express": "2.x",
        "connect": ">= 1.4",
        "log4js": ">= 0.2.5"
      },
      "engines": { "node": ">= 0.4.6" }
    }
{% endhighlight %}

and to install the modules, use:
    npm install .

in the project dir.

To install a module globally, use the command:
    npm install module -g

and it will be available anywhere.


# Conclusion

It seems a little too much work to have a nice environment but this is trivial to avoid package conflicts and version problems between different projects.

