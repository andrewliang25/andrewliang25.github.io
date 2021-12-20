---
title: SEO(Search Engine Optimization) on Hexo NexT
date: 2020-07-14 18:40:06
tags:
---


## Google Search Console

Go to {% link Google Search Console https://search.google.com/search-console/welcome %} and add property.
{% asset_img search_console_new_property.png Enter blog URL under URL prefix %}

<!-- more -->

Then verify ownership by HTML tag.
{% asset_img verify_ownership.png Click "HTML tag" to see extended content %}

Copy the meta tag which contains verify code.
{% asset_img verify_ownership_HTML_tag.png Click "copy" %}

Paste the copied meta tag on the top of `head.swig`.
Which is under `<username>.github.io\themes\next\layout\_partials\head\`
After generating and deployment, you will verify it successfully.


## Submit Sitemap
Install Hexo plugin to generate sitemap.
```
npm install hexo-generator-sitemap --save
```
Then open `_config.yml` under `root\`, add the code beneath at the end:
```
# Sitemap
sitemap:
  path: sitemap.xml
```
After generating and deployment, check if it generated `sitemap.xml` successfully.

Then submit the sitemap to Google Search Console.
{% asset_img submit_sitemap.png Submit sitemap.xml to Google Search Console %}
Check the status of siremap. You should see "Success".


## Google Analytics
Register on {% link Google Analytics https://analytics.google.com/ %}.
{% asset_img welcome_google_analytics.png Welcome to Google Analytics %}

Enter account name (you can change it later).
{% asset_img google_analytics_account_setup.png Account setup %}

Choose "Web".
{% asset_img google_analytics_measure_website.png What do you want to measure? %}

Enter "Website Web" and "Website URL". **Select "https://".**
{% asset_img google_analytics_property_setup.png Property setup %}

Then you will get a unique tracking ID.
Put the ID in `username.github.io\themes\next\_config.yml`:
```
# Google Analytics
google_analytics:
  tracking_id: UA-XXXXXXXXX-X
  localhost_ignored: true
```

See if Google Analytics get any dataflow.

# Reference

> https://support.google.com/webmasters/answer/9429907
> https://github.com/hexojs/hexo-generator-sitemap
> https://support.google.com/analytics/answer/1008015?hl=en
