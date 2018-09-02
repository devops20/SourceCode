# gitflow

https://www.atlassian.com/git/tutorials/comparing-workflows

https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow

https://git-scm.com/book/en/v2/Git-Branching-Branching-Workflows



https://www.toptal.com/git/git-workflows-for-pros-a-good-git-guide


rebase:

https://benmarshall.me/git-rebase/

Git Rebasing Examples

The example below combines git rebase with git merge to maintain a linear project history. This is a quick and easy way to ensure that your merges will be fast-forwarded.

# Start a new feature
git checkout -b new-feature master
# Edit files
git commit -a -m "Start developing a feature"

In the middle of our feature, we realize there’s a security hole in our project:

	
# Create a hotfix branch based off of master
git checkout -b hotfix master
# Edit files
git commit -a -m "Fix security hole"
# Merge back into master
git checkout master
git merge hotfix
git branch -d hotfix

After merging the hotfix into master, we have a forked project history. Instead of a plain git merge, we’ll integrate the feature branch with a rebase to maintain a linear history:

git checkout new-feature
git rebase master

This moves new-feature to the tip of master, which lets us do a standard fast-forward merge from master:

git checkout master
git merge new-feature



##########################
git reset --soft hard mixed

https://stackoverflow.com/questions/3528245/whats-the-difference-between-git-reset-mixed-soft-and-hard

When you modify a file in your repository, the change is initially unstaged. In order to commit it, you must stage it—that is, add it to the index—using git add. When you make a commit, the changes that are committed are those that have been added to the index.

git reset changes, at minimum, where the current branch (HEAD) is pointing. The difference between --mixed and --soft is whether or not your index is also modified. So, if we're on branch master with this series of commits:

- A - B - C (master)

HEADpoints to C and the index matches C.

When we run git reset --soft B, master (and thus HEAD) now points to B, but the index still has the changes from C; git status will show them as staged. So if we run git commit at this point, we'll get a new commit with the same changes as C.

Okay, so starting from here again:

- A - B - C (master)

Now let's do git reset --mixed B. (Note: --mixed is the default option). Once again, master and HEAD point to B, but this time the index is also modified to match B. If we run git commit at this point, nothing will happen since the index matches HEAD. We still have the changes in the working directory, but since they're not in the index, git status shows them as unstaged. To commit them, you would git add and then commit as usual.

And finally, --hard is the same as --mixed (it changes your HEAD and index), except that --hard also modifies your working directory. If we're at C and run git reset --hard B, then the changes added in C, as well as any uncommitted changes you have, will be removed, and the files in your working copy will match commit B. Since you can permanently lose changes this way, you should always run git status before doing a hard reset to make sure your working directory is clean or that you're okay with losing your uncommitted changes.

 
