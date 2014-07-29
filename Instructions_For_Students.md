#Instructions for Students#

The following serves as an introduction to the Feature Branch way of working with git and GitHub, along with some practice with merge conflicts and recovering from mistakes.

This lesson works best if you have a friend to do it with, to fully experience resolving merge conflicts.  After you find a friend, figure out who will be "User 1" and who will be "User 2", as you'll have separate instructions later.

###Getting started with these Excercises###
This lesson set assumes you already have a git installation.  [GitHub for Windows](https://windows.github.com/) or [GitHub for Mac](https://mac.github.com/) are good clients if you don't already have one.

Fork this repository (only once, if you have a partner) and then clone it.  Either hit the convenient "Clone in Desktop" button (if you installed a client recently, this may require you to restart your browser), or 
```
git clone https://github.com/[username]/PracticingGit.git
```
Be sure to give your friend [push access](https://help.github.com/articles/adding-collaborators-to-a-personal-repository)!

###My first feature, GUI-style###
Let's get a feel for our new GUI (unless you are a strict command-line person, then skip ahead to the next section).

First, let's make a branch off of master.  Note the new branch will always be off of whatever branch you are currently working on.  Use your name as the branch.
![gui1](https://cloud.githubusercontent.com/assets/6819944/3729155/cfc85a9a-16b7-11e4-83d4-f5a9aef6c8c6.PNG)
Second, open up the README.md file.  User 1, replace [training aid #1] with your name.  Likewise, User 2, replace [training aid #2] with your name.  We want to avoid conflicts for now, so make sure you don't edit anything else.  Be sure to save your file.
![gui2](https://cloud.githubusercontent.com/assets/6819944/3729160/e62ce8e6-16b7-11e4-9187-3e982aba9677.PNG)
You should see the client recognize the changes.  It should even stage them for you automatically by checking the box of all the files with edits (currently only one).
![gui3](https://cloud.githubusercontent.com/assets/6819944/3729165/f5523970-16b7-11e4-8099-54a9fd1593ca.PNG)
Type in a commit message, optionally a commit body and then press the commit button.
![gui4](https://cloud.githubusercontent.com/assets/6819944/3729168/ffc84d72-16b7-11e4-8d23-b78761e82c61.png)
Our branch, by default, is a private one, and we can see that our new commit is "unsynced", that is, our coworkers haven't gotten it yet.  Click the Publish button to make it public.
![gui5](https://cloud.githubusercontent.com/assets/6819944/3729169/07655746-16b8-11e4-86aa-bcde0a03bb79.png)
Now that our feature branch is public, let's merge it into master.  User 1, you'll go first, so we have no problems (for now).  User 2, hang on for a moment. Click the "manage" button to pull up a branch tool.
![gui6](https://cloud.githubusercontent.com/assets/6819944/3729170/12801aa8-16b8-11e4-8661-97b6430b1d68.PNG)
This tool is drag and drop.  Drag our feature branch to the first slot and "master" to the second branch.  We want to put our features *into* master, so we do it in this order.
![gui7](https://cloud.githubusercontent.com/assets/6819944/3729174/1be6d5b4-16b8-11e4-9da7-6c11da5d2ae4.png)
Then, hit merge.  This should happen automatically.  You can delete your feature branch, if you want.

Switch back to the master branch and you'll see your commit there, as well as the fact that you'll need to sync.  Hit the sync button.
![gui8](https://cloud.githubusercontent.com/assets/6819944/3729188/6b665b8c-16b8-11e4-8e8c-179be4fc4c46.PNG)

User 2, thank you for your patience.  Go ahead and hit your sync button to pull in User 1's change.  Then, repeat the same steps to merge it in.

And that's it, you have just made your first feature branch, your first feature and merged it in.  Pretty slick, right?

###Now for the command line###
For this excercise, we'll do a similar style of changes, but this time, we'll deal merge conflicts.  And, we'll try it from the command line.


Let's make a branch off of master.
```
git checkout master
git branch fav_recipe		
git checkout fav_recipe
```

Go ahead and, to the absolute bottom of the Best_Recipes.md and add the name of your favorite food.  Also, let's update the first line to say "the best six recipes" instead of "the best five recipes".  When you are done, save, and execute `git status` to verify git detected your changes.

We'll stage the changes and commit, like so:
```
git add Best_Recipes.md
git commit -m "Blueberry souffles are the best food ever"   //or a different message of your choosing
```

This time, instead of making our feature branch public, let's merge it in to master and then push it.  This is a typical workflow if the feature is completed.

```
git checkout master		//we switch to the "base branch" we want the feature to join
git merge fav_recipe
git push
```

Who ever is the second person to push (in your group) will introduce a merge conflict.  You'll probably see a message like "Updates were rejected because the tip of your current branch is behind." 

To resolve this, we need to get the pushed changes and merge them in:
```
git pull			//gives message like "Conflict (content): Merge conflict in Best_Recipes.md"

git mergetool		//opens up graphical merge tool (like Meld) to handle the conflicts
```

When you are done resolving the conflicts (i.e. listing both recipes and changing "the best six recipes" to "the best seven recipes"), save the file in Meld, exit meld and then end the merge with `git commit`

Now, you can push your resolution:
```
git push
```


The GitHub tool doesn't handle merge conflicts well, which is why I avoided it in the first demo.  If you see something like:
![image](https://cloud.githubusercontent.com/assets/6819944/3738388/4d878d56-1740-11e4-87a7-4fcabbab92bb.png)

and you try to sync, you'll probably see:

![image](https://cloud.githubusercontent.com/assets/6819944/3738400/67656d10-1740-11e4-8f68-e6558fad568a.png)

If you suspect there will be conflicts pushing or pulling, I recommend switching to the command line.

###Staging###
Now for some practice staging.  Run the following setup.  
```
git checkout origin/for_staging_practice -t
git branch staging_copy				//make a copy of this branch
git checkout staging_copy

git reset HEAD~1 			//this will DESTROY the previous commit (named "Commit Blob")
							//you would NEVER want to do this to a pushed commit
```
The last command basically undid the last commit, leaving us with a bunch of edits that we will pretend you just did.  To do the edits, you can use one of a few commands

```
git diff HEAD
//or
git status -v
//or, assuming you have it set up
git difftool HEAD
```
As you can see, 3 or 4 different things have happened, which means if we were to commit all the changes, it would be a bit messy.

First, let's stage the addition of Nutritional_Information.md and Top_tier_supply_list in to two separate commits, as they are distinct and deserve their own thought.
```
git add Nutritional_Information.md 			//tab completion is your friend
git status
``` 
Your terminal should look something like:
![image](https://cloud.githubusercontent.com/assets/6819944/3737341/1c08c678-1736-11e4-88c2-c88c4cf13fc4.png)
Note the staged change (Nutritional_Information.md), the not staged (Best_Recipes.md), and the untracked (Top_tier_supply_list.md).  These the three typical states an edit can be in.

```
git commit -m "Adding Nutrition stub"

git add Top_tier_supply_list.md
git commit -m "A supply list would be good"
```

Now we are left with the changes to the recipe, which fall into one of two categories: Adding serving size and Adding recipe variations (There may be more, what do you think?).  For practice, let's use the interactive staging command.  If you make a mistake while staging, `git reset` will unstage everything.

```
git add -p
```
![image](https://cloud.githubusercontent.com/assets/6819944/3737471/3957db6e-1737-11e4-8a33-b0e04f5e9118.png)
This shows us a *hunk* of edits and gives us half the alphabet to type to respond.  What does each mean?

* y - stage this hunk
* n - do not stage this hunk
* q - quit; do not stage this hunk or any of the remaining ones
* a - stage this hunk and all later hunks in the file
* d - do not stage this hunk or any of the later hunks in the file
* g - select a hunk to go to
* / - search for a hunk matching the given regex
* j - leave this hunk undecided, see next undecided hunk
* J - leave this hunk undecided, see next hunk
* k - leave this hunk undecided, see previous undecided hunk
* K - leave this hunk undecided, see previous hunk
* s - split the current hunk into smaller hunks
* e - manually edit the current hunk
* ? - print help

If you forget, type **?** and git will print the list.  Usually, you'll stick with **y**, **n**, or **q**.

When you are done with staging the first set, commit, using a descriptive message and then invoke `git add -p` to do another interactive staging process, or `git add .` to stage all changes.

For super efficency, you can stage everything and commit in one command:
```
git commit -am "Message"   		// the -a flag says "All changes", and -m specifies the message, so we merge them -am
```

###Log###
The gui has a nice way to view the recent history.  To get something like that, we use the log command:
```
git log
```

Wow, that's an extensive log.  By default, git uses the **less** tool to show the long change history, which means you can page up or page down by pressing **b** or **space** respectively.  Most important of the numerous commands less offers (e.g. searching), is to exit, which you do by typing *q*.

Normally, we don't want to see the entire history, so to show the last five commits:
```
git log HEAD~5..HEAD
```
This looks a little strange, but what what's going on is what I call "relative commits" (officially called "Extended revisions").  Normally, you have to specify the sha hash of a commit so git knows which one you mean.  Normally, these are pretty long `fd0c1f30927ea926ae27d7e1c0c6d52db95795c1` and it would be a pain to type them out in full.

Fortunately, there are shortcuts.  `HEAD` always refers to the previous commit, i.e. the one you are working off of right now.  The relative part of "relative commits" comes into play with `HEAD~1`, which is the parent of `HEAD`, which is usually two commits ago.  In the example, `HEAD~5` refers to five commits before `HEAD`.

The two dots (yes, two dots, despite a standard [ellipsis](http://en.wikipedia.org/wiki/Ellipsis) having three dots) specify a range, from `HEAD~5` to `HEAD`, which is a lot easier than listing `HEAD, HEAD~1, HEAD~2...`.  Why are 5 commits shown instead of 6 (which should be the case if you count carefully)?  It's just how `git log` works, returning commits between those two points.

Now, `HEAD` is useful and all, but what if you are referring to commits in a different branch?  Never fear, we can do relative positioning on sha hashes as well.
```
//don't actually type this.  See below:
git log 4671d25c04bccbf2f1a4257b8560b3181baffaa5~3..4671d25c04bccbf2f1a4257b8560b3181baffaa5		//Shows the three commits before the specified commit
```

Hashes are really long.  Thankfully, you only need to type as much of the hash as you need to be unique.  This is typically between 5 and 7 chars depending on the size of the repo.  Git will mumble something about "ambiguous arguments"  if you need more. 

```
git log 4671d~3..4671d		//Shows the three commits before the specified commit
```

We'll be using these tricks throughout the rest of the lesson to save space an

###Reset/Revert, tools for going back in time###
If you want to undo previous commits, there are two general ways to do this, a permanent* way and a temporary way.

We'll start with the temporary way.  I use this when I'm working on a new feature,  realize an older feature has broken, and want to see if my last few commits are responsible.

Let's try this from master, to revert the last 3 changes:
```
git checkout master
git revert HEAD~3..HEAD  //the first in the range is ignored, so this is only the last 3 commits
```

Git will make 3 new commits that are exact opposites of the last three commits - removing text you added and replacing deleted text.

You don't need to reset in order.  If you feel that the 2nd to last commit was really the culprit, you can just revert that with:
```
git revert HEAD~1 
```

Now, let's pretend the old feature was broken before I started work (i.e. my changes didn't break them) and I want to delete the revert commits and go back to what I was working on.  `git reset` has the power to delete commits, along with a few other things.

To delete the 3 reverts we introduced:
```
git reset --hard HEAD~3 //this puts the 4th to last commit as the new head
```

The most common use case I have for reset is actually to abandon all my changes I've made since the last commit.

Go ahead and edit some file, any file, pehaps deleting most of it.  Then, to undo that:
```
git reset --hard HEAD  //return to the last commit
```

One final caution about reset.  **NEVER** delete commits that have been pushed to the central repository, as this will screw up your coworker's history and make reincorporating changes difficult.

*Okay, technically reset is not permanent.  [git reflog](http://gitready.com/intermediate/2009/02/09/reflog-your-safety-net.html) can dig you out of trouble if you really need it, but it's best to be careful and pretend that deleting commits with reset can't be undone.

###Merging, a more thorough practice### 

####A basic merge####
We have two branches `quiche-1-merge` and `quiche-2-merge`.  They have some additions to our recipe collection, but the quiche recipes don't quite match.  Let's merge these two branches and resolve the conflicts.
```
git checkout origin/quiche-1-merge -t
git checkout origin/quiche-2-merge -t 		//get these branches if they don't already exist

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

Finally, let's merge the temporary branch `integrating-quiche` back into master, which should be an easy fast-forward merge.
```
git checkout master
git merge integrating-quiche
git branch -d integrating-quiche   //delete temporary branch
```

####Merging strategies####
In some cases, we can be smart about how we merge, using *merge strategies*.

For all the examples, we will assume we were the authors of quiche-merge-1 and are looking to merge in some changes posed by quiche-merge-2.

```
git checkout quiche-merge-1
git branch merge-strats			//this will be the temporary merge branch
git checkout merge-strats
```

Now, if quiche-merge-2 were an old dev branch and we want to basically ignore all changes in that branch, we can use the *ours* strategy. 

`git merge quiche-2-merge -s ours`

This type of merge will *never* have a conflict, but if you look at the end of the results, **all** changes from quiche-2-merge, including the extensive soup recipe, were lost.  The *ours* strategy is typically only useful if you want to keep the history of a branch, but ignore all consequences of said branch.

Let's undo the merge:
```
git reset --hard HEAD~1
```

A more useful merging pattern would have used the default merging strategy, but defaulted to using our version, if there was a conflict.

Thankfully, there is such an option.
```
git merge quiche-2-merge -X ours
```

Again, there will be no conflicts.  This is because any conflicts are resolved using our changes.

Notice in the results from the merge that all three recipes (quesadilla, soup and quiche) are there, with our quiche recipe overwriting the other one.

The subtle difference here is the -s and the -X switch.  the -s uses the *ours* strategy, where the -X uses the *ours* option associated with the default strategy (known as the *recursive* strategy).

Had we wanted to keep the other quiche recipe (i.e. from "their" branch), we simply would have done:

```
git merge quiche-2-merge -X theirs
```

Most of the time, you'll want to use the default recursive strategy with one of a few options like
```
git merge [branch] -X ignore-all-space   //differences in whitespace are ignored
git merge [branch] -X patience		//can produce better diffs for merging, especially if large changes have been made
```

####Patient Merging - a savior for large diffs####
I wasn't planning to do an entire lesson on the patient merge option, but then a real-life example happened as I was putting these lessons together.

We'll be merging patience-merge-2 into patience-merge-1.  As before, let's make a special merge branch, just in case things go wrong (and they might).
```
git checkout origin/patience-merge-1 -t
git checkout origin/patience-merge-2 -t 		//get these branches if they don't already exist


git checkout patience-merge-1
git checkout -b patience-merge  //shorthand for making a new branch and switching to it
```

Merge in patience-merge-2, and then pull up mergetool
```
git merge patience-merge-2
git mergetool
```

![patience_bad](https://cloud.githubusercontent.com/assets/6819944/3729379/cc37ae9e-16bc-11e4-9eb4-f6c983f32cc1.PNG)
Ouch!  That diff is terrible!  Git seems to have gotten confused on exactly what changed and what didn't.  Lines 9-17 seem identical in both the left and the right versions, but that's not what the diff says.

To be clear, this isn't a problem with Meld, but with the algorithm git used to compare the two branches.  Meld simply displays what git outputs.

Quit Meld and when git asks if the merge was successful, say no.  Then, abort the merge with:
```
git merge --abort
```

Now, we'll tell git to be a bit more careful merging this time.
```
git merge patience-merge-2 -X patience
git mergetool
```

![patience_good](https://cloud.githubusercontent.com/assets/6819944/3729384/d8e00e8e-16bc-11e4-9084-c46a08cb864c.PNG)

There, that's a much clearer diff, showing us exactly what we need to know.  The version on the left is obviously more fleshed out, so we can take those changes.

Wrap up the merge by committing.  We're not quite done yet, as we have to merge our temporary merge branch into the "main" branch, which was patience-merge-1.
```
git checkout patience-merge-1
git merge patient-merge		//this merge should be automatic

git branch -d patient-merge //delete temp branch
```




For a lesson on recovering from mistakes, see [this set of excercises](/Recovering_from_mistakes.md).