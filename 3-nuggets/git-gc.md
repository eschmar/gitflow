[< Back to Nuggets](readme.md)

---

# Reduce local Git folder size

When working with a git repository for a long time, the `.git` folder can become quite bloated. Here is how to clean up with the commands [git reflog](https://git-scm.com/docs/git-reflog) and [git gc](https://git-scm.com/docs/git-gc).

```sh
# Check `.git` folder size
du -sh .git

# Prune older reflog entries
git reflog expire --all --expire=now

# Cleanup unnecessary files and optimize the local repository
git gc --prune=now --aggressive

# Recheck folder size. Should be lower now.
du -sh .git
```
