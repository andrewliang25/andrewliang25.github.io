---
title: Hexo - Custom Theme
date: 2020-06-24 17:01:37
tags:
---


## Chose your theme
Go to {% link Hexo Theme https://hexo.io/themes/ %} and pick a theme you like.
**Note: This article, I use {% link NexT https://github.com/theme-next/hexo-theme-next %} theme as example.**

## Fork theme repository
Click into theme repository and fork it. 
{% asset_img nextRepoFork.png Fork NexT theme repository %}
**⚠ Be aware of Copyrights. No commercial use. ⚠**
Now you have your own repo which is clone from the theme.
<!-- more -->

## Git Submodule
```
git submodule add <https://github.com/your/forked/theme/repo> themes/<theme_name>
```
Clone the repository into `theme/<theme_name>` as submodule.
We can see `.gitsubmodule` file has been added.

## Theme configuration
Open `_config.yml` in root file and modify theme name.
{% asset_img configChangeTheme.png Change theme into NexT %}
Enter `themes/<theme_name>` folder, open `_config.yml`.
There is a lot of settings. Change and preview it with `hexo server`.

## Commit and push changes
After config the theme, we need to commit and push changes on remote.
Enter `theme/<theme_name>` on terminal. Enter command `git status`.
You will see the branch is detached.
Update HEAD using `git checkout`.
```
git checkout master
```
Since HEAD is on forked-theme-repo/master, commit and push your changes.
Also, don't forget to commit and push blog source.

## Checkout submodules in workflow
Since you have pushed blog source, CI has been triggered.
But the blog shows blank layout.
Because CI did not checkout submodules.
Add `Checkout submodules` before `Deploy hexo`.
```
- name: Checkout submodules
  uses: srt32/git-actions@v0.0.3
  with:
    args: git submodule update --init --recursive
```
Commit it and wait for CI done its job.

# Known Issues

## Blank layout
* Check if submodules checkout successfully
{% asset_img CheckoutSubmodules.png Log of CI Checkout submodules %}

## Template Render Error while generating
* Update Hexo to latest version
```
npm update
```

> Reference
> https://help.github.com/en/github/getting-started-with-github/fork-a-repo
> https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/syncing-a-fork
> https://git-scm.com/book/en/v2/Git-Tools-Submodules
