#Instructions for Students#




###Recovering from Mistakes###
We all make goofs from time to time, but version control was designed to help us out when we goofed by remembering the history and giving us access to it.

####Well, those changes didn't work (Super Undo)####

####I started working in the wrong branch!####
#####The setup#####
Make a new branch **adding_images**

`git branch adding_images`

Make some changes, like adding `![image](https://cloud.githubusercontent.com/assets/6819944/3662415/5564f386-11ca-11e4-9bd2-bb47126a825d.png)` to the cheesecake recipe, showing off how delicious the end result is.

#####The problem#####
`git branch` reveals that we are still in our old branch making this change. 
This is not good, as we are mixing together features.  

Thankfully, since we didn't commit, the resolution is pretty easy.  We'll use the **stash**, which acts like a stack of changes:
```
git stash
git checkout adding_images
git stash list  	//optional, but we can see what was stashed
git stash apply		//applies the most recently stashed changes
```

**Alternative fix**
In some cases, I've noticed newer versions of git are smart enough to do this for you if you simply switch branches:

`git checkout adding_images`

Try this first, and if git complains about uncommitted changes, go with the above solution.

#####To avoid this#####
Make sure you checkout the branch after you make it:
```
git branch new_branch
git checkout new_branch
```

####I _committed_ in the wrong branch!####
#####The setup#####
as [before](#user-content-i-started-working-in-the-wrong-branch), but now execute

`git commit -m "Added image of cheesecake"` 

after making the change(s).

#####The problem#####
`git log --decorate` shows us the problem in detail, with a commit in the wrong wrong branch.  Make a note of the first 5-10 letters/numbers in the sha hash, we'll need them in a bit.

Since we haven't pushed yet, no one else need know of our mistake.  We'll simply copy the misplaced commit to the correct branch using the *cherry-pick* command and then delete the old commit. 

```
git checkout adding_images
git cherry-pick [hash]
//if there are merge conflicts, you'll need to run git merge or git mergetool and then git cherry-pick --continue
git checkout old_branch
git reset --hard HEAD~1 	//erases the last commit by resetting to the 2nd to last commit
git checkout adding_images
//back to work (on the right branch)
```

If you had the misfortune of committing multiple (e.g. 3) commits to the wrong branch, you'll do something similar:
```
git checkout adding_images
git cherry-pick [hash]~3..[hash]

//again, if there are merge conflicts, you'll need to run git merge or git mergetool and then git cherry-pick --continue
git checkout old_branch
git reset --hard HEAD~4 	//erases the last 3 commits by resetting to the 4th to last commit
git checkout adding_images
//back to work (on the right branch)
```


#####To avoid this#####
Make sure you checkout the branch after you make it:
```
git branch new_branch
git checkout new_branch
```