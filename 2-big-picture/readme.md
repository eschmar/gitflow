## 2. The Big Picture

The previous chapter was intentionally held short, because by experience it’s easiest to explain Git using flowcharts. This chapter introduces the "big picture", a flowchart picturing the life cycle of a project repository in Gitflow. Each of the steps will be explained in their own subchapter.

* [Project Setup](#project-setup)
* [Hotfix](#hotfix)
* [Feature/Bugfix](#featurebugfix)
* [Release](#release)
* [Rebase](#rebase)
* [Clean Up](#clean-up)

### Project Setup

#### Project Files

Project setup will be done once and ideally is a standardised process, maybe even using a boilerplate project as a base. So let's have a look at what belongs into a repository before the actual work on the project beings:

* **readme.md**: Describe your project.
* **.gitignore**: Use a service like [gitignore.io](http://gitignore.io) and adjust to your needs, such that no unnecessary land in your repository.
* **.gitattributes**: Define how to treat which files and set up [Git Large File Storage](https://git-lfs.github.com/).
* **.editorconfig**: Tabs or spaces? Either way, standardise hits among your team with the [editorconfig file](http://editorconfig.org/).
* **Build files**: Build configuration files depending on the services you are using.

This list is of course not complete and not mandatory. Make sure you find a sensible standard for your team and improve it along the way. 


#### Project Configuration

Initially, your repository will only contain a `master` branch. Create a `dev` branch originating from `master` and set it as the default branch. This makes sure that the `dev` branch is the default target branch in pull requests.

Next step is protecting both the `master` and `dev` branch from being pushed to directly. As stated earlier, all your changes should go through a proper branch and pull request. This makes sure that no direct pushes happen accidentally and that no `push --force` is possible.

Et voilà. Your repository is ready to be forked. The following sections assume that you are working on your own fork and two remotes configured:

* `origin`: Your own fork.
* `upstream`: The main repository.

How to add `upstream` to your remotes:

```sh
git remote add upstream <repository>
```

### Hotfix

Originates from | Will be merged into
--- | ---
`master` | `master` and `dev`

Important points to remember:
* This is the only temporary branch originating from `master`.
* Should only be used for severe bugfixes that prevent production from running properly.
* Create a new tag with a minor version bump ("v1.0.0" -> "v1.0.1") after merging.

```sh
# make sure your master branch is up to date
git checkout master
git fetch upstream
git rebase upstream/master

# create the new hotfix branch
git checkout -b hotfix/<name>

# make your changes
git add <file>
git commit -m "<message>"
...

# push the changes to your fork
git push -u origin hotfix/<name>

# create a pull request
# Pull Request: origin/hotfix/<name> -> upstream/dev

# create a new tag on master
git checkout master
git fetch upstream
git rebase upstream/master
git tag -a v1.0.1
git push upstream --tags

# Delete the hotfix branch.
```


### Feature/Bugfix

Originates from | Will be merged into
--- | ---
`dev` | `dev`

Important points to remember:
* The most common branch types you will be using.
* Difference between feature and bugfix is only the wording for better readability.
* **Never** merge these branches directly into `master`!

```sh
git checkout dev
git pull
git fetch upstream
git rebase upstream/dev

# create the new branch
git checkout -b feature/<name>

# make your changes
git add <file>
git commit -m "<message>"
...

# push the changes to your fork
git push -u origin feature/<name>

#
# It's good practice to rebase your feature or bugfix branch before
# creating pull requests. See chapter "Rebase".
#

# Pull Request: origin/feature/<name> -> upstream/dev
# Delete the feature/bugfix branch.
```


### Release

Originates from | Will be merged into
--- | ---
`dev` | First `master` then `dev`

Important points to remember:
* Is used when the development on the `dev` branch continues, but the features for an imminent new release have been frozen.
* From this point, only bugfixes should be merged onto the `release` branch.
* Bugfixes on `release` may be merged back into `dev` as well.
* Create a new tag with a version bump upon release.

```sh
git checkout dev
git pull
git fetch upstream
git rebase upstream/dev

# create the new branch with the version number (e.g. "v1.0.0")
# and directly push it to the main repository
git checkout -b release/<version>
git push -u upstream release/<version>

#
# at this point, the release branch should be deployed to a staging environment and thoroughly tested!
#

# if necessary, make your bug fixes 
git add <file>
git commit -m "<message>"
... 
git push

# Pull Request: upstream/release/<version> -> upstream/master
# Pull Request: upstream/master -> upstream/dev

# Delete the release branch.
```


### Rebase

Before we start: This is one of the trickiest steps in the beginning. Please take your time and don't be shy - **ask your peers** in case something is unclear!

Before merging your feature- or bugfix branch back into `upstream/dev`, it's good practise to rebase your branch. Other team members may have already merged their work back into `dev` and we want to avoid merge conflicts. The basic idea of a rebase is:

* Revert your branch to the original state when you created it from `dev`.
* Update to the current state of `dev`.
* Re-apply your commits one by one on top of the updated `dev` branch.

And all of this fully automatically - with the magic of git. So in the end it will seem, as if you started working from the latest state of the `dev` branch.

Does this sound too good to be true? Yes it is. Along the way, git merge conflicts may arise - and that's what causes the most problems for beginners.

Let's tackle this with an example, assuming you're on the master branch:

```sh
# Create a test file
printf "a\nb\nc\nd" > test.md
git add test.md
git commit -m "Add test file"

# Let's assume we have two colleagues A and B
git checkout -b conflict/a

# 1. Edit the letter 'd' into 'e' and commit
# 2. Edit the letter 'a' into 'f' and commit

git checkout master 
git checkout -b conflict/b

# 1. Edit the letter 'd' into 'x' and commit
git checkout master

# Now A is done with his work and merges first back into master
git merge conflict/a

# When B tries to merge back, there should be a merge conflict,
# since the letter 'd' was changed into 'e' and git doesn't know
# if it should keep 'e' or the new 'x':
git merge conflict/b

#
# Auto-merging test.md
# CONFLICT (content): Merge conflict in test.md
# Automatic merge failed; fix conflicts and then commit the result.
#
# This is what we want to avoid! Let's take a step back. The person
# merging the changes, is probably the maintainer of the repository.
# It may not be obvious what you were trying to change and it would
# require a lot of time to figure this out. So most likely he will
# just deny the changes. That's why the creator of the change
# should rebase.
#
git merge --abort

git checkout conflict/b
git rebase master

# Now first the commits from `conflict/a` will be applied and
# a merge conflict arises when the commits from `conflicts/b`
# are re applied. The difference is, that now the creator is
# dealing with the merge conflict, instead of the maintainer.
git mergetool
git rebase --continue

# When solving the merge conflict, backup files ending in *.orig
# may have been created. Let's remove that file with a clean:
git clean -f

# Retry to merge `conflict/b`
git checkout master
git merge conflict/b

# Nice!
```

#### `git mergetool`
In the example above, we've used the command `git mergetool`. This will open your defined tool to handle merge conflicts. There are various tools out there - choose the one that best fits you. Look out for three-way merging functionality.


### Clean up

Yes, clean up. This makes it not only easier for you, but also for your colleagues who may be reviewing your code or have to check something in your repository. This includes:

* Delete old branches
* Clean up local branch references

```sh
# delete a local branch
git branch -D feature/delete

# delete a remote branch
git push origin :feature/delete

# clean up local branch references
git branch -a
git branch remote prune origin
git branch -a
```


---

Next up: [Nuggets](../3-nuggets)