# git-team-pratice

## How to push a new local branch to a remote Git repository

1. Create a new branch.
```
git checkout -b remote-branch-01
```

2. Edit or add some file, for example create a new file 'remote-branch-01.txt'

3. Push your branch to the remote repository.
```
git push -u origin remote-branch-01
```

## How to checkout a remote branch into new local branch 

Assume there is a new remote branch `origin/Feature2020` was created by others, and it is not in your local git repo.

First, fetch the remote branches, and now you will able to see the `origin/Feature2020` shown in your remote-branch list
```
git fetch origin
```

Next, you checkout to a local branch and work on it
```
git checkout -b Feature2020 origin/Feature2020
```

## How to rebase

### Work On A New Branch

Create a new dev branch and checkout to that branch

```
git checkout -b feature-001
```

### Commit Regulary

Add some commits

```
echo "hello" > feature-001-01.txt
git add .
git commit -m "Add feature-001-01.txt"

echo "world" > feature-001-02.txt
git add .
git commit -m "Add feature-001-02.txt"

echo "!!!" > feature-001-03.txt
git add .
git commit -m "Add feature-001-03.txt"
```

### Fetch Before Squashing

When you're ready to merge your features back into the master branch, run git fetch. 
```
git fetch
```

### Squash Commits Into One

```
git rebase -i origin/master
```

This will open an interactive rebase tool, which shows all the commits you've made on your branch. You'll then `squash` all your changes into one commit.

To do this, replace pick with s for all but the top commit. s is shorthand for squash - imagine all the changes you've made being `squashed` up into the top commit.

**Squashing** three commits into one by replace the `pick` to `s` from second to thrid commits are squashed into the first commit.

```
# original
pick bf27dcd Add feature-001-01.txt
pick cc23dcb Add feature-001-02.txt
pick ef30abc Add feature-001-03.txt
...
```

```
# Squashing second to thrid commits into the first commit
pick bf27dcd Add feature-001-01.txt
s cc23dcb Add feature-001-02.txt
s ef30abc Add feature-001-03.txt
...
```

Press `Esc` and then enter `:wq` to save and exit the VIM interactive rebase tool

When you close this window you'll see all your existing commits, which you can edit down into a simpler, more concise commit message.

Replacing existing commits with a new commit message.

Exit the rebase tool and you're ready to merge.

### Merge Your Changes

Checkout the master branch

```
git checkout master
```

Merge INTO master

```
git merge feature-001
```

Push your local master branch to remote 

```
git push origin master
```

### Cleanup

Delete remote feature branch (the colon is important!)

```
git push origin :feature-001
```

Delete local branch

```
git branch -d feature-001
```

### Reference

- [https://jameschambers.co/writing/git-team-workflow-cheatsheet/](https://jameschambers.co/writing/git-team-workflow-cheatsheet/)

