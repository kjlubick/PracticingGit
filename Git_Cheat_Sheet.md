#Git Cheat Sheet#


###Branching Workflow###





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