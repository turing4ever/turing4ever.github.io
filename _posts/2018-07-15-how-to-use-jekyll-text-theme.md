---
title: How to use jekyll-text-theme
key: 20180715
tags: jekyll howto
---

The instructions on the home page of jekyll-text-theme doesn't actually
work well for hosting a blog on github. Because ideally you would like 
to build your site both locally and on github with the same settings. 
The challenge is that github only supports a few default themes. If you 
want to use other themes, you only have one choice: pick one theme that is hosted
as a public github repo and use `remote-theme:USRNAME/REPONAME` instead of `theme:THEMENAME`.

Here is what I have added in my _config.yml: 
`remote_theme: kitian616/jekyll-text-theme`
It works perfectly on both github and my local Mac. Yes~!

