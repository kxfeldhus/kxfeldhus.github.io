---
layout: post
title: Create and apply a patch from svn diff
---

Sometimes I find that I have been working in trunk for what was going to be a very small change, and it has outgrown  that scope and belongs in its own branch.

There are 2 options.

#### svn switch

This allows you to point your working copy at a different remote 


You can even switch only specific sub directories of your project. Which I suppose could be handy.

My biggest fear is that if I forget to switch back, it could get confusing, so I rarely use this method.
 
#### svn diff and patch

I prefer to be as verbose as possible when moving code around, and so I like this method, although it's less elegant.



-p0 ensures that the files you are applying to exist
-i just tells it to take the patchfile.diff as input