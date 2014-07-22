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

#####To avoid this#####
Make sure you checkout the branch after you make it:
```
git branch new_branch
git checkout new_branch
```