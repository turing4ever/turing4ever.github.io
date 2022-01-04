---
title: Turn the clock back with git 
key: 20190504
tags: 
published: false
---

Writing code sometimes is like hiking on a trail, especially at a point where you really wish you could go back but could't. 
It's a blessing that `git` allows you to do what's impossible in the physical world if you can use it properly. 


_Scene 1_

You just edited a bunch of files in a directory but you haven't committed anything yet. Unfortunately you realize that what you 
have written in the last 15 minutes was completely brain fart. Instead of burning all your manual scripts, you do this: 
```bash
git reset --hard
```     

_Scene 2_

Like in Scene 1, your brain farted, but you have committed locally! `git reset --hard` can't save you this time. 
In order to discard your last commit, you do this: 
```bash
git revert bb248d23
``` 
in which `bb248d23` is the commit id of your last commit. This command will make another commit to undo what you have edit 
in your last commit. 


_Scene 3_

You smoked something and you took one step further than Scene 2. You **pushed** to remote! Can you still regret and go back?
Yes, you do this to discard the last commit in a remote branch:
```bash
git push origin +bb333333^:remote_branch_name
``` 
in which `bb333333` is the commit id of last commit in `remote_branch_name`, caused by your foolish `push`. The command here 
forces the remote branch to the parent of `bb333333`. 

With forgiveness from `git`, you can save yourself some headache by using tricks above. You still need to discipline 
yourself to use `commit` and `push` strategically so that in your panic moment, `git` can turn the clock back for you.
