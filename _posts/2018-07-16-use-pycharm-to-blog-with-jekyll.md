---
title: Use Pycharm to blog with jekyll
key: 20180716
tags: 
published: false
---

Wouldn't it be great if you can stay in your favorite IDE even when you
are writing your blog?


Pycharm is a promising solution with its integration of git, awesome
editor, syntax highlighting and markdown plugin. But there's only one
problem that gets in the way: unlike your flask or django apps, there's
no builtin runner for jekyll.
You can run your local site by `bundler exec jekyll serve` from command
line but do you really want to switch back to terminal every time when
finishing your draft in Pycharm?

You can add a Bash runner and customerize it to serve your local site.
Here is what I did:
1. Edit Configurations
2. Add a Bash runner from the defaults.
3. Change or add following parameters.

| Settings: | Values|
| -------- | -------------- |
| Script: | _config.yml |
| Interpreter Path:| /usr/local/bin/bundler |
| Interpreter Options:| exec jekyll serve |
| Program Argument: | -I |
| Working Directory:| PATH_TO_ROOT_OF_YOUR_REPO |


Now it runs like a charm. Enjoy!
