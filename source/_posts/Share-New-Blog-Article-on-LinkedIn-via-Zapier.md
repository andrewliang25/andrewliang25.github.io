---
title: Share New Blog Article on LinkedIn via Zapier
date: 2021-12-25 21:01:30
tags:
---


## Add RSS in your site

Install hexo generator feed:
```
npm install hexo-generator-feed --save
```

Put the plugin in `_config.yml`:
```yaml
feed:
  enable: true
  type: atom
  path: atom.xml
  limit: 20
  hub:
  content:
  content_limit: 140
  content_limit_delim: ' '
  order_by: -date
  icon: icon.png
  autodiscovery: true
  template:
```

<!-- more -->

Verify if `atom.xml` is generated to your repositary:
{% asset_img Check-atom.xml.png Check atom.xml %}

## Create and configure workflow on Zapier

First, register on Zapier.

Select `RSS by Zapier` and `LinkedIn`.
Choose the recommended workflow: blog posts on linkedin.
{% asset_img Create-workflow.png Create Workflow %}

Add RSS URL of your blog to `Feed URL`.
{% asset_img Add-RSS-URL.png Add RSS URL %}

Zapier will crawl the three latest articles in RSS.
If it looks all right, continue.
{% asset_img Test-trigger Test Trigger %}

Select `Create Share Update` and connect to your LinkedIn account.
{% asset_img Create-Share-Update-in-LinkedIn.png Create Share Update in LinkedIn %}
{% asset_img Grant-Access-to-Zapier.png Grant Access to Zapier %}
{% asset_img LinkedIn-Account-Connected.png LinkedIn Account Connected %}

Configure post format.
{% asset_img Set-up-Actions.png Set up Actions %}

Test the Zap and check it on your LinkedIn.
{% asset_img Send-Test-Post-via-Zap.png Send Test Post via Zap %}
{% asset_img Test-Post-on-LinkedIn.png Test Post on LinkedIn %}

Rename the Zap and turn it on.
{% asset_img Turn-on-Zap.png Turn on Zap %}

From now on, Zapier will share every new article from your blog automatically.

# Reference

> https://github.com/hexojs/hexo-generator-feed
> https://zapier.com/apps/linkedin/integrations/rss/152/grow-your-audience-by-sharing-your-new-blog-posts-on-linkedin
> https://www.tricycle-europe.com/how-to-automate-sharing-to-linkedin/