[< Back to Nuggets](readme.md)

---

# Git log

Git log is the tool for understanding the history of your repository.

```sh
# Only show commits made on the current branch.
# If you have followed gitflow and use this command on dev,
# this will only show pull request merge commits. 
git log --first-parent

# Files changed in the last 5 commits
git log --name-status --pretty=oneline -n 5

# See the changes of a file, works even 
# if the file was deleted
git log -- <file path>

# List amount of commits per author
git shortlog -s -n
```
