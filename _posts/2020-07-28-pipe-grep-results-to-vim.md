---
title: Pipe grep results into vim 
key: 20200728
tags: 
---

Sometimes you really need to copy the `grep` results into vim for further editing. And yes, you wish it could be done in one line. 
Here is a quick trick: pipe the grep results into vim. 

```console
grep PATTERN * | vim -
```
The trailing `-` tells `vim` to accept input from `STDIN`. Done!
