#Instructions for Students#


###Getting started with these Excercises###
- fork/clone

----GUI
- make branch
- make changes to contributor file (avoiding merge conflict) 
- stage
- commit 
- sync

----Command line
- make branch
- make changes (add favorite recipe to bottom of recipes, making conflict)
- stage
- commit
- push
- resolve conflicts


###Staging###
(have them checkout a branch, git reset --soft HEAD~1)


###Log###
-introduce ranges here
-quitting out of less

###Reset/Revert###
-use revert to temporarily rollback changes for debugging
-use rest

###Merging###
We have two branches `quiche-1-merge` and `quiche-2-merge`.  They have some additions to our recipe collection, but the quiche recipes don't quite match.  Let's merge these two branches and resolve the conflicts.
```
git checkout master
git branch integrating-quiche
git checkout integrating-quiche
```
First, since we anticipate a grusome merge, let's make a branch `integrating-quiche` to work on.  If we screw up, we can delete the branch and try again.

```
git merge quiche-1-merge 
```

The syntax here says "merge quiche-1-merge onto the current branch".  This merge should be done automatically, as it was derived from master and has no overlapping changes.

```
git merge quiche-2-merge 
```

Here we have some manual issues to resolve.  GitHub for Windows or GitHub for Mac can't handle these, so you have to resolve them on the command line.

 Open the merge tool to handle this (I recommend [Meld](http://meldmerge.org/)), or resolve them manually using your text editor.
```
git mergetool
```

If you are using Meld, remember that the center editor is what will be the merge results, the outside editors are temporary.  Save (Ctrl+S) when you are done resolving all the conflicts, and then exit Meld.  Git will automatically detect when you exit and move on.

When you are done with the mergetool, you'll see something like:
![image](https://cloud.githubusercontent.com/assets/6819944/3714391/26cb0e32-15a5-11e4-96f1-374f913f91db.png)

If you are happy with the results of the merge, `git commit` will conclude the merge process.  If you want to undo the merging, `git merge --abort` will rollback to before you merged in quiche-2-merge. 

For a lesson on recovering from mistakes, see [this set of excercises](/Recovering_from_mistakes.md).