---
title: Install Hexo and Deploy to GitHub
date: 2020-06-03 15:08:55
tags:
---


**Note: All instructions below are based on Windows.**

## Environment
* {% link Node.js https://nodejs.org/en/ %}
* {% link Git https://git-scm.com/ %}
* {% link Notepad++ https://notepad-plus-plus.org/ %}( or any editor you prefer)

<!-- more -->

## Install Hexo and Initailization
Install with the command below.
```
npm install -g hexo-cli
```

After installing Hexo, let's initialize it.
```
hexo init                               //Initialize Hexo in current folder
npm install                             //Install Hexo in current folder
npm install hexo-deployer-git --save    //Install hexo-deployer-git
```
Or create new folder with initialization.
```
hexo init <folder>                      //Create new folder <folder> and initialize Hexo in it
cd <folder>                             //Change directory into <folder>
npm install                             //Install Hexo in current folder
npm install hexo-deployer-git --save    //Install hexo-deployer-git
```

## Blog Config
Enter the Hexo folder you just set up.
And open "_config.yml" by right click -> Edit with Notepad++ (or your own text editor).
Modify line 6 ~ line 18. Change URL to your own github page `https://<username>.github.to/`
{% asset_img modify_config.png %}

## Deploy to GitHub
At the bottom of "_config.yml", modify the file as below.
Change repo into your own repo link `https://github.com/<username>/<username>.github.io.git`
{% asset_img config_deploy.png %}

Enter the command below in terminal.
Make sure the path is blog folder.
```
hexo clean          //Clean the cache file (db.json) and generated files (public)
hexo generate       //Generate static files
hexo deploy         //Deploy your website
```
Now enter `https://<username>.github.io/` in browser to see how your blog looks like!


# Reference

> https://hexo.io/docs/index.html
> https://hexo.io/docs/commands.html
> https://hexo.io/docs/one-command-deployment.html
