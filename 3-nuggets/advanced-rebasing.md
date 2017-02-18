[< Back to Nuggets](readme.md)

---

# Advanced rebasing

Beyond re-applying your commit on another base, `rebase` offers an interactive mode, allowing you to edit each commit as it is re-applied and effectively rewriting the git history however you want. This includes:

* Squash multiple commits into a single one
* Move commits inside the history
* Split commits into multiple
* Edit commits
* ...and more!

So hold your breath, we'll do all of these in one rebase!


#### Setup

I have prepared a fresh git repository with a single file `readme.md` and then created the following 6 commits in chronological order:

1. Squash A
2. Squash B
3. Squash C
4. Move to top
5. Split
6. Rename me


#### Battle plan

What we're going to do:

* Squash the first 3 commits into one single commit with the message "Squashed".
* Move the "Move to top" commit, so it seems like it was the first commit.
* Split the commit "Split" into two commits "Split A" and "Split B"
* Fix the commit message from "Rename me" to "Renamed"


The resulting commits order should be:


1. Move to top
2. Squashed
3. Split A
4. Split B
5. Renamed


#### Let's go

[![asciicast](https://asciinema.org/a/e0frfdhgq25s3joztmk6pzmix.png)](https://asciinema.org/a/e0frfdhgq25s3joztmk6pzmix)

#### Notes

Rebasing is a powerful tool! Notice how the commit hashes are different, after we've completed the rebase. That's because we have rewritten history. So unless those 6 commits have been made exclusively offline, the only way to push our rebase is by `git push --force`. Be careful here!

* Only rebase your own branches
* If you really have to rebase a branch where multiple people have worked on, talk with each other first!
* You can always abort a rebase by typing `git rebase --abort`

Some maintainers will require you to squash your work into a single commit, in order to improve the repository history. [Github now even offers squashing functionality](https://github.com/blog/2141-squash-your-commits) directly on the merge button. Now you know how to do this.
