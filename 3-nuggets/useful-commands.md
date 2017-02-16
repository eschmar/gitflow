## [Back to Nuggets](readme.md)

---

# Useful commands

Collection of useful commands:

```sh
# add only parts of your changes with the --patch option
git add --patch
git add -p

# files changed in the last 5 commits
git log --name-status --pretty=oneline -n 5

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

# see the changes of a file, works even 
# if the file was deleted
git log -- <file path>

# checkout branch of a fork
# http://stackoverflow.com/a/5884825/4401817
git remote add coworker git://path/to/coworkers/repo.git
git fetch coworker
git checkout --track coworker/foo

git checkout foo
git pull

# diff
git difftool development..feature/<name>

# list amount of commits per author
git shortlog -s -n
```
