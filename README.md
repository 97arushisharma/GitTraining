# GitTraining
A simple git training repository where we document various git commands.

[https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners](https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners)

## Entering our Identity

The first thing you should do when you install Git is to set your user name and e-mail address. This is important because
every Git commit uses this information, and it’s immutably baked into the commits you pass around:

>     $ git config --global user.name "John Doe"
>     $ git config --global user.email johndoe@example.com
  
Again, you need to do this only once if you pass the --global option, because then Git will always use that information for
anything you do on that system.
If you want to override this with a different name or e-mail address for specific projects, you can run the command without
the --global option when you’re in that project.

## Checking the Settings

If you want to check your settings, you can use the git config --list command to list all the settings Git can find at that
point:

>     $ git config --list
>
>     user.name=Arushi Sharma
>     user.email=arushisharma@gmail.com
>     color.status=auto
>     color.branch=auto
>     color.interactive=auto
>     color.diff=auto
>     ...

>     $ git config user.name
  
>     Arushi Sharma
  
## Getting Started

To push a new project to github follow the following steps:

>     $ cd <project_directory>
>     $ git init
>     $ git add <file_name> OR .

(.) dot adds all the files present in that directory to the commit.

>     $ git commit -m "Commit Message"

The commit message should ideally be less than 8 words. To write an extended description use:

>     $ git commit -m

Add the commit message to the file that opens.

Now create a repository on github. Now creat a SSH key for remote ssh to the repo from your machine. For this look if the rsa key already exist:

>     $ cat ~/.ssh/id_rsa.pub

If the file does not exist create a rsa key using the following steps:

>     $ ssh-keygen -t rsa
Press enter until it generates a key. Now copy the content of the public key(id_rsa.pub) and add them to your github settings under SSH key:

```
https://github.com/settings/keys
```
Now add the remote repo to your local repo:

>     $ git remote add origin git@github.com:XYZ/project.git
>     $ git remote -v

Now push your commits to the master branch:

>     $ git pull --rebase origin master
>     $ git push origin master

## Cloning a Repository

You can clone a repository with <git clone [url]> command. For example, if you want to clone the Ruby Git library called
Grit, you can do so like this:

>     $ git clone git://github.com/97arushisharma/GitTraining.git

This creates a directory named GitTraining, initializes a .git directory inside it, pulls down all the data for that 
repository, and checks out a working copy of the latest version. If you go into the new GitTraining directory, you’ll see
the project files in there, ready to be worked on or used. If you want to clone the repository into a directory named 
something other than GitTraining, you can specify that as the next command-line option:

>     $ git clone git://github.com/97arushisharma/GitTraining.git git-training
  
## Create a new Branch and Push into it

>     $ git init
>     $ git add .
>     $ git commit -m "Librarian control to Admin"
>     $ git pull
>     $ git checkout -b librarian_removal
>     $ git push origin librarian_removal
>     $ git branch -a
>     $ git checkout master
>     $ git pull https://github.com/97arushisharma/Gem-Library.git librarian_removal
>     $ git push origin master
  
## To make changes to a cloned project and push them directly.

>     $ git branch
>     $ git add/rm <file_name>
>     $ git commit -m "Message Here"
  
### to fetch all the latest changes from the master branch

>     $ git fetch -v --all
  
### Write our changes on top of the fetched changes

>     $ git rebase
>     $ git push origin <branch_name>
  
## Cherry Pick a commit from branch1 to branch2(Instead of Merging)

>     $ git checkout <branch1>
>     $ git log --oneline
  This will show all the commits that have been performed on branch1.
Select the hash for the commit that you wish to cherry-pick and apply over branch2.
>     $ git checkout <branch2>
>     $ git cherry-pick <commit-hash>
  Apply the commit hash for all the commits that you need in the chronological order(earliest first)
Incase of any merge conflicts resolve them and then use the following commands:
>     $ git add <file-name>
>     $ git cherry-pick --continue
This will apply the cherry-picked commit on top of the HEAD of the branch2.
To see the files that have been changed use:
>     $ git diff --name-status <branch2>..<branch1>
Now to squash any commits use:
>     $ git rebase -i
  Edit the `pick` to `s` or `f` for all commits except the first. `s` and `f` flag squash/ fixes the commit to the commit preceding it.

Advanced used case: Suppose you have made two tools named “apple” and “orange”
```
<cid> Add feature for apple
<cid> Paint apple red
<cid> Eat apple
<cid> Eat orange
<cid> Throw orange
```
So, we will edit them as:
```
p Add feature for apple
f Paint apple red
f Eat apple
p Eat orange
f Throw orange
```
You can even reorder commits in `git rebase -i`.

To edit the commit message:
>     $ git commit --amend
>     $ git push origin <branch2>
  
>     $ git cherry -v branch2 branch1
   This will show the list of all the commits in branch2 that were made after the split from branch1.
  
### Then create a single commit for all commits

>     $ git rebase -i <Commit-Hash>
  
The `Commit-Hash` will be the hash for the commit ovre which all the commits have to be squashed. Edit the 'pick' into 's' for all the commits except the first one to squash them into a single commit.

### To checkout a particular commit from current branch into a new branch

>     $ git branch <branch-name> <commit-hash>

## How to show a particular commit including the changes

### This will show all the recent commits in the chronological order

>     $ git log
>     $ git log --decorated

### Pick the commit hash of the commit that you wish to see and use it in the below command

>     $ git show <commit-hash>
  
### To show the differences in the uncommited code and the master(origin)

>     $ git diff
To show differences in the staged changes
>     $ git diff --staged

### To see the git commit graph

>     $ git log --all --oneline --graph
