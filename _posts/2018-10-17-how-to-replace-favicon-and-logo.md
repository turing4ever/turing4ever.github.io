---
title: How to replace favicon and logo
key: 20181017
tags: 
---
If you are using jekyll-text-theme and hosting your blog on github, how do you customize the `favicon` and `logo` on the blog?
Here are some instructions:
https://tianqi.name/jekyll-TeXt-theme/docs/zh/logo-and-favicon

If you simply follow the instructions, it will almost work. Almost! 

If you are hosting it on github.com with remote-theme, you shouldn't
update `_includes/head.html`. Assuming that you haven't changed any filenames for the icons, 
you only need to copy those files generated from **RealFaviconGenerator** to *assets* folder. 
Then you are all done. If you also updated `_includes/head.html`, you will actually mess up the page. 
So, skip it. 

   
