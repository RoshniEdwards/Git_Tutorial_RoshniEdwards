# Git Tutorial
**Roshni Edwards**


So let’s start by understanding what git is. **Git** is software used to track changes in a set of files. Programmers usually use it for coordinating collaborative work while creating source code during software development. This is very helpful because it allows several different contributors to make proposed changes to a file without having to necessarily change the original file. This tutorial will help you get started with Git and gain a better understanding of how it can help you! :D

*Prerequisites: Install Git and create a Github account*

**We will be covering the following concepts in this tutorial:**
1. Cloning a Repository
2. Checking a File's Status
3. Staging a File
4. Committing Changes to a File
5. Pushing Changes
6. Creating a Branch
7. Stashing
8. Merging

Say you have a program you want to collaborate on with one of your friends. You can use git to do this! Let's say that your friend has written a simple html program that created a very basic website, but you want to change the program so that the website is more interesting and engaging for people to look at. You can both collaborate on the website using git! 

We will start this tutorial by **cloning an existing repository** in git. Files are stored in a repository. A repository is similar to how you store files in a folder or directory on your computer.Cloning a repository allows you to have a full copy of the file and potentially make your own changes to it!  To do this, the command you need is **git clone**.
1. open your terminal(in my case gitbash)
2. You clone a repository by typing git clone and then the repository's github url. For example, if you want to clone your friend's git repository where they stored their code called website_1, you can do so like this:
```
$ git clone https://github.com/website_1/website_1
```
3. If you want to clone the repository into a directory named something other than website_1, you can specify the new directory name as an additional argument:

```
$ git clone https://github.com/website_1/website_1 mywebsite
```
Keep in mind that your local repository is made up of three "trees" maintained by git. the first one is your *Working Directory* which holds the actual files. the second one is the *Index* which acts as a staging area and finally the *HEAD* which points to the last commit you've made.

After cloning the file, you now have a copy of the file that you can edit and make changes to.

Each file in your working directory can be either tracked or untracked. Tracked files  are files that Git knows about. Untracked files are any files in your working directory that were not in your last snapshot and are not in your staging area.

Make sure the files you want to edit are tracked by **checking their status** using the **git status** command. It would look something like this if you ran git status right after a clone..

```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working tree clean
```

*This means that none of your tracked files are modified yet.*

Now, to edit the file open your file explorer and find the file location on your computer. When you find it, open it with your prefered editor, (I am using Visual Studio Code) and make the changes you want to add. After you have modified your file, you need to stage it before committing your changes.

To **stage your file**, you run the **git add** command. This is used to start tracking new files, to stage files, etc. Below, we are staging our mywebsite file and running git status.

```
$ git add mywebsite.md
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README
    modified:   mywebsite.md
```
*Remember, if you modify a file after you run git add, then you need to run git add again to stage the latest version of the file before committing again*

Now that you have modified your file and staged it, you are ready to **commit your changes**. To do this you simply type **git commit**.

```
$ git commit
```
Once you do this, your editor of choice will open and give you a message that looks something like this..
```
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# On branch master
# Your branch is up-to-date with 'origin/master'.
#
# Changes to be committed:
#	new file:   README
#	modified:   mywebsite.md
#
~
~
~
".git/COMMIT_EDITMSG" 9L, 283C
```
You can either delete the default commit message and type your own, or just leave it as is.
You can also insert your commit message inline by adding a -m and then your message to your commit command. For example, if we added a title to the website we can say:
```
$ git commit -m "add Title"
[master 463dc4f] add Title
 2 files changed, 2 insertions(+)
 create mode 100644 README
```
Now the file is committed to the HEAD, but not in your remote repository yet.

To send the changes you made to your remote repository, we need to **push changes** and to do this, execute **git push origin master** and change "master" to whatever branch you want to push your changes to.
```
$ git push origin master
```
Now your changes are pushed to the master branch!

In Git, a **branch** is a pointer to one specific commit. You can use new branches for development and merge them back to the master branch upon completion. The master branch is the branch where you first created your repository.

To create a new branch use the **git branch** command.
 For example to create a branch named "future" use...
```
$ git branch future
```
To switch to the branch you just created, you run the **git checkout** command...
```
$ git checkout future
```
To switch back to master...
```
$ git checkout master
```
*This points the HEAD pointer back to the master branch, and reverts the files in your working directory back to the snapshot that master points to.*
\
And to create a new branch and switch to it at the same time, you can run the git checkout command with the -b switch:
```
$ git checkout -b future_2
Switched to a new branch "future_2"
```


and to delete the branch again...
```
$ git branch -d future_2
```
And remember, a branch is not available to others unless you push the branch to your remote repository...
```
$ git push origin <branch>
```
And now your branch can be seen by the other collaborators on your file.


**git stash** temporarily shelves (or stashes) changes you've made to your working copy so you can work on something else, and then come back and re-apply them later on.

The command to stash your changes is **git stash**:
```
$ git stash
Saved working directory and index state WIP on master; d7435644 Feat: configure graphql endpoint
```
*This stores/"stashes" the uncommitted changes and overlooks untracked and ignored files.*

You can reapply stashed changes with the commands **git stash apply** and **git stash pop**. git stash apply reapplies the changes while git stash pop removes the changes from the stash and reapplies them to the working copy.
```
$ git stash pop future
```
or
```
$ git stash apply future
```

**git stash clear** empties the stash list by deleting all stashes.
**git stash drop <stash_id>** deletes a certain stash from the stash list.

And to **update and merge a branch** you would use the **git pull** and **git merge** commands.

to update your local repository to the newest commit...
```
$ git pull
```
to merge another branch into your active branch(master) use git merge. So if we wanted to merge our branch future_2 back into future we can use:
```
$ git merge future
```
Git attempts to auto-merge changes, but this is not always possible and results in conflicts. You need to merge those conflicts by editing the files shown to you by git. After changing, you need to mark them as merged...
```
$ git add future_2
```
before merging changes, you can also preview them by using
```
$ git diff <source_branch> <target_branch>
```
or in our case with future_2 merging with future...
```
$ git diff future_2 future
```
I hope this tutorial helped you understand git a little more!
Here's a [link to more Git information](https://git-scm.com/book/en/v2) if you need it!
			


![Image](https://miro.medium.com/max/800/1*70aOJ1osE9C8cVZUkmH95g.png)