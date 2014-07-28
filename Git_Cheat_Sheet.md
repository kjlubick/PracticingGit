#Git Cheat Sheet#


###Branching Workflow###
Get updates from coworkers

`git pull` 

Make a new (local, private) branch and switch to it.
```
git branch new_branch
git checkout 

//or, in one command
git checkout -b new_branch
```

Stage some of your changes for a nice, neat commit 
```
git add file_one.txt
git add file_two.txt

//or, for a more interactive approach, to allow chunk-by-chunk seperation
git add -p

//then, commit them
git commit -m "Succint message about what happened"
```

Save all your changes (locally)
```
git commit -a -m "Some message here"
```




####Undo last commit, preserve changes####
`git reset --soft HEAD~1`

Technically, the `--soft` flag is on by default, but I can never remember if it is or not, so I always type it out.

**Common use cases:** You want to split up the last commit into multiple or forgot to add files

This completely erases the last commit you made, so do **not** use it if you have already pushed that commit.


####Permanently get rid of all changes since last commit####
`git reset --hard`

**Common use cases:** You don't like the changes you've made and want to start over from the last commit

####Temporarily get rid of all changes since last commit####
`git stash`

To undo:

`git stash apply`

**Common use cases:** You need to do something on a different branch, but can't automatically switch branches because of conflicts.