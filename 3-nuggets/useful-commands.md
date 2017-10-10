[< Back to Nuggets](readme.md)

---

# Useful commands

Collection of commands, possibly usable in cli aliases:

```sh
# add only parts of your changes with the --patch option
git add --patch
git add -p

# check remote entries
git remote -v

# preview removal of untracked files and then remove them
git clean -n
git clean -f

# remove local branches after they have been deleted upstream
git branch -D <branch>
git remote prune origin

# merge branches and choose which branch to prioritize
git merge branch -X ours/theirs

# diff
git difftool development..feature/<name>

# remove all merged branches and prune your fork
git fetch origin && git fetch upstream && git branch --merged | grep -v -e "master" -e "development" | xargs git branch -D && git remote prune origin
```
