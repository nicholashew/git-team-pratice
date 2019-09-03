"# git-team-pratice" 

## How to rebase

```
######################################################
## CREATE A NEW BRANCH TO WORK ON
######################################################
# Create a new dev branch and checkout to that branch
git checkout -b feature-001

######################################################
## WRITE SOME CODE, COMMIT REGULARLY
######################################################
# Make two commits
echo "hello" > feature-001-01.txt
git add .
git commit -m "Add feature-001-01.txt"

echo "world" > feature-001-02.txt
git add .
git commit -m "Add feature-001-02.txt"

echo "!!!" > feature-001-03.txt
git add .
git commit -m "Add feature-001-03.txt"

######################################################
## FETCH WHEN YOU'RE DONE
######################################################
# When you're ready to merge your features back into the master branch, run git fetch. 
git fetch

######################################################
## SQUASH YOUR COMMITS AND GET READY TO MERGE
######################################################
# SQUASH YOUR COMMITS AND GET READY TO MERGE
git rebase -i master

# This will open an interactive rebase tool, which shows all the commits you've 
# made on your branch. You'll then "squash" all your changes into one commit.
# To do this, replace pick with s for all but the top commit. s is shorthand for  # squash - imagine all the changes you've made being "squashed" up into the top commit.

# "Squashing" three commits into one by replace the "pick" to "s" from second to thrid commits are squashed into the first commit.
# press "Esc" and the ":wq" to save and exit the VIM interactive rebase tool

# Replacing existing commits with a new commit message
# Exit the rebase tool and you're ready to merge.

######################################################
## MERGE YOUR CHANGES
######################################################
# Checkout the master branch
git checkout master

# Merge INTO master
git merge feature-001

# Push your local master branch to remote 
git push origin master

######################################################
## CLEANUP
######################################################
# Delete remote feature branch (the colon is important!)
git push origin :feature-001

# Delete local branch
git branch -d feature-001
```