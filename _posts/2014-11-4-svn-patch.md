---
layout: post
title: Create and apply a patch from svn diff
---

Sometimes I find that I have been working in trunk for what was going to be a very small change, and it has outgrown  that scope and belongs in its own branch.

The 2 options are [svn switch](http://svnbook.red-bean.com/en/1.7/svn.ref.svn.c.switch.html) or [svn diff](http://svnbook.red-bean.com/en/1.7/svn.ref.svn.c.diff.html) + [patch](http://linux.die.net/man/1/patch)

### svn switch

This allows you to point your working copy at a different remote 

{% highlight console %}
> pwd > trunk
> svn mkdir http://local.svn.com/project/branches/new_branch
> svn switch http://local.svn.com/project/branches/new_branch
> svn commit -m 'Commit from trunk that should have been in new_branch'
> svn switch http://local.svn.com/project/trunk
{% endhighlight %}

You can even switch only specific sub directories of your project. Which I suppose could be handy.

My biggest fear is that if I forget to switch back, it could get confusing, so I rarely use this method.
 
### svn diff and patch

I prefer to be as verbose as possible when moving code around, and so I like this method, although it's less elegant.

{% highlight console %}
> pwd > trunk
> svn diff file_with_changes_1 file_with_changes_2 > patchfile.diff
> svn mkdir http://local.svn.com/project/branches/new_branch
> cd ..
> svn checkout http://local.svn.com/project/branches/new_branch
> cd new_branch
> cp ../trunk/patchfile.diff .
> patch -p0 -i patchfile.diff
> svn commit -m 'Commit from trunk that should have been in new_branch'
{% endhighlight %}


-p0 ensures that the files you are applying to exist
-i just tells it to take the patchfile.diff as input
