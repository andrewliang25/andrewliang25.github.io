---
title: Hexo - Custom Theme
tags:
---

## Chose your theme
Go to {% link Hexo Theme https://hexo.io/themes/ %} and pick a theme you like.
**Note: In this article, I use {% link NexT https://github.com/theme-next/hexo-theme-next %} theme as example.**
## Fork theme repository
Click into theme repository and fork it.
{% asset_img nextRepoFork.png Fork NexT theme repository %}
**⚠ Be aware of comercial usage due to Copyrights ⚠**
Now you have your own repo which is clone from the theme.
<!-- more -->

## Git Submodule


```
λ git submodule add <https://github.com/your/forked/theme/repo>
```

## Theme configuration

## Commit and push changes

## Checkout submodules in workflow




# Known Issues

### Blank layout

* Check if submodules checkout successfully

### Template Render Error while generating

* Update Hexo to latest version

> Reference
> https://help.github.com/en/github/getting-started-with-github/fork-a-repo
> https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/syncing-a-fork
> https://git-scm.com/book/en/v2/Git-Tools-Submodules
