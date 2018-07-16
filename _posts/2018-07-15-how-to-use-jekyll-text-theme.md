---
title: How to use jekyll-text-theme
key: 20180715
tags: jekyll howto
---
Documentations on the jekyll-text-theme [official site](https://tianqi.name/jekyll-TeXt-theme/docs/en/quick-start)
outline three ways of running a site on github with jekyll-text-theme:  
 1. Copy & paste the source code into your own repo.
 2. Fork and reuse the source code of the theme. 
 3. Install the theme as a gem. 

 I think all of them work. However, if you want to keep idential environments on both github and your local machine, keep the theme up to date without much efforts, 
you've got some challenges.  

 For example, if you copy & paste the theme code, how do you update the theme when it gets a new version?  
 Installing the theme as a gem is great, but Github is not your personal server. You can't install gems there.   
 In fact, Github only supports a few default themes when you use `theme:THEMENAME`. If you want to use other themes, you only have one choice: picking one theme that is hosted as a public github repo and use `remote-theme:USRNAME/REPONAME` instead of `theme:THEMENAME`.


So, here is what I have added in my `_config.yml`:   
```YAML
     remote_theme: kitian616/jekyll-text-theme  
```
It works perfectly on both Github and my Mac.  

