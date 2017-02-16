[< Back to Nuggets](readme.md)

---

# Git reset

First off: **Have you already pushed your changes?**
If yes and you haven't pushed to your private fork, **stop right here!** Unless you really know it's ok to rewrite history.

## Normal `reset` 

Let's start with the regular `git reset` and go back one commit as an example:

```sh
git reset HEAD~1
# make your changes
git add ...
git commit -c ORIG_HEAD
```

What we did:
* `git reset` moves the `HEAD` pointer to a specified point
* `HEAD~1` specifies this point as the previous command to the current `HEAD` reference
* At this point, it looks like the previous commit never existed
* `git commit -c ORIG_HEAD` re-commits the "lost" commit


## `git reset --soft`
The `--soft` option takes one more step, than only moving the `HEAD` reference back by one. It also adds the changes which were made in the commit we just undid, to the staging area (`INDEX`). When you execute `git status` after the soft reset, you'll see green the changes that were made by the commit and red the changes made after you commited.


## `git reset --hard`
`--hard` takes even one more step. After moving the commit changes to the staging area like `--soft` does, it also undoes any changes to the working tree. So anything you did after the commit, will be lost.


## Bonus: Change latest commit message
If you only want to change the commit message of the latest commit, there's no need for a `reset` and you can simply use the `--amend` option.

```sh
git commit --amend
# or directly
git commit --amend -m "<new-message>"
```

## Beyond `reset`
If you want to go more aggressive and rewrite the history, check out [Advanced rebasing](advanced-rebasing.md).