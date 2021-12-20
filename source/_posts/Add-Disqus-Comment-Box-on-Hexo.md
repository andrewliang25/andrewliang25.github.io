---
title: Add Disqus Comment Box on Hexo
date: 2021-09-24 14:35:00
tags:
---


## Prologue

Disqus is a global comment system that improves discussion on websites and connects conversations across the web.

## Create Site

Create an account and log into {% link Disqus https://disqus.com/ %}. Once logged in, click the `GET STARTED` button on the homepage.
{% asset_img DisqusGetStarted.png GET STARTED %}

<!-- more -->

Then select `I want to install Disqus on my site` option and you will see the `Create a new site` interface.
{% asset_img installDisqusOnMySite.png install Disqus on my site %}

Enter your `Website Name`, which will serve as your Disqus shortname, or you can customize it. And select a Category from the drop-down menu. Then click `Create Site` button.
{% asset_img DisqusCreateNewSite.png Create New Site %}

Suscribe `Basic` plan
{% asset_img DisqusBasicPlan.png Suscribe Basic %}

Choose `I don't see my platform listed, install manually with Universal Code`, ignore the installation.
{% asset_img DisqusInstallation.png Disqus Installation %}

configure Disqus for your site, and click `Complete Setup` button.
{% asset_img DisqusModerationSettings.png Setup Moderation %}

## Enable Disqus

Set the value `enable` to `true`, add the obtained Disqus shortname (`my-custom-blog-shortname`), and edit other configurations in `disqus` section in the `theme config file` as following:
{% asset_img configYmlDisqus.png themes\next\_config.yml %}

Then you have comment box on your post like me below!


# Reference

> https://theme-next.js.org/docs/third-party-services/comments