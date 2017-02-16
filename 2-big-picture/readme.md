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
# PR origin/hotfix/<name> -> upstream/dev

# create a new tag on master
git checkout master
git fetch upstream
git rebase upstream/master
git tag -a v1.0.1
git push upstream --tags
```


### Feature/Bugfix

Originates from | Will be merged into
--- | ---
`dev` | `dev`

Important points to remember:
* The most common branch types you will be using.
* Difference between feature and bugfix is only the wording for better readability.
* Never merge these branches directly into `master`!

```sh
git checkout dev
git pull

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

# go to stash and create the pull request from your fork
# PR origin/feature/<name> -> upstream/dev
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

# create the new branch with the version number (e.g. "v1.0.0") and directly push it 
git checkout -b release/<version>
git push -u origin release/<version>

#
# at this point, the release branch should be deployed to a staging environment and thoroughly tested!
#

# if necessary, make your bug fixes 
git add <file>
git commit -m "<message>"
... 
git push

# go to stash and create the pull requests
# PR upstream/release/<version> -> upstream/master
# PR upstream/master -> upstream/dev
```


### Rebase
// todo


### Clean up

Yes, clean up. This makes it not only easier for you, but also for your colleagues who may be reviewing your code or have to check something in your repository. This includes:

* Delete old branches
* Clean up local branch references

```sh
# delete a local branch
git branch -D feature/delete

# delete a remote branch
git push origin :feature/delete

# clean up local branch references git branch -a
git branch remote prune origin git branch -a
```

See [CLI Aliases](../3-nuggets/cli-aliases.md) for shortening these steps.

