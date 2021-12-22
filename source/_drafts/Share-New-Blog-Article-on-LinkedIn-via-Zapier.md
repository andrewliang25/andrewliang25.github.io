---
title: Share New Blog Article on LinkedIn via Zapier
tags:
---

## Add RSS in your site

Install hexo generator feed:
```
npm install hexo-generator-feed --save
```

Put the plugin in `_config.yml`:
```
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
{% asset_img %}

Test if it connects successfully.
{% asset_img %}

Configure post format.
{% asset_img %}

Check test post on your LinkedIn.
{% asset_img %}

Rename the Zap and turn it on.
{% asset_img %}


# Reference

> https://github.com/hexojs/hexo-generator-feed
> https://zapier.com/apps/linkedin/integrations/rss/152/grow-your-audience-by-sharing-your-new-blog-posts-on-linkedin
> https://www.tricycle-europe.com/how-to-automate-sharing-to-linkedin/