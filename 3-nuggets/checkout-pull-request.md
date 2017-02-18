[< Back to Nuggets](readme.md)

---

# Checkout Pull Requests

When a colleague is requesting help or you want to test a pull request yourself, you can easily fetch the branch from his or her fork and (depending on your priveleges) contribute directly.

```sh
# checkout branch of a fork
# http://stackoverflow.com/a/5884825/4401817
git remote add coworker git://path/to/coworkers/repo.git
git fetch coworker
git checkout --track coworker/foo

# pull updates from your coworker
git checkout foo
git pull
```

However, as a general rule, a fork is supposed to be your own playground. Avoid using this too much and for example rather make use of the pull request review features of Github, requesting changes from your colleague. At the very least, talk with each other first. In the worst case you can push the branch to your own fork, decline the original pull request and create a new one, originating from your fork.
