**This is a work in progress.**

![Gitflow](gitflow-small.png)

The goal of this repository is to have a shareable reference point for working with git, specifically using the gitflow branching model. Everything in this guide is heavily inspired and based on [nvie's original blog post](http://nvie.com/posts/a-successful-git-branching-model/). As he correctly realised, the easiest way to teaching git is using a "big picture" figure:

[Gitflow Life Cycle PDF Version](gitflow.pdf)

Is this guide for you? Gitflow works well in mid-sized teams with multple deployment environments. There are reasons for not using any dev branch at all (in flat organisations), but it requires continuous live deployment, which is not always possible (when working for a customer, rather than on a product).

## Information
This section is only important if you're evaluating this to share with your colleagues. If you were sent here, [jump right to `Getting started`](#1-getting-started).

## 0. Table of contents
1. [Getting Started](#1-getting-started)
    * Git basics
    * Checklist
2. [Gitflow](#2-gitflow)
    * Branch types
    * Pull Requests
    * Forking
    * Flow charts
3. [Cookbook](#3-cookbook)
    * Project setup
    * Hotfix
    * Feature/Bugfix
    * Release
    * Rebase
    * Advanced rebasing
    * Clean up
4. [Helpers](#4-helpers)
    * CLI alias
5. [Recommended tools](#5-recommended-tools)

## 1. Getting started
To really grasp the concepts behind git, it is critical to know the basic commands. That’s why this guide will be using the command line. If you want to streamline the process with a GUI later on (see recommended Tools) that’s fine, however command line is and should be the default.

Please take your time to go through each chapter in this guide and **ask your peers** in case something is unclear!

### Git basics
Because there’s already comprehensive documentation on Git basics available on the web and this guide focuses more on the workflow, I won’t cover them here. Instead, I provide links to resources I found best for starting with git. Please go through the following guides:

* [git - the simple guide](http://rogerdudler.github.io/git-guide/)
* [Got 15 minutes and want to learn Git?](https://try.github.io)

Now you should have a basic understanding on how to use git.

### Checklist
Make sure you understand the following commands and concepts before continuing:

* Git init/clone
* Git status
* Git Add
* Git reset
* Git commit 
* Git push
* Git pull
* Git branch 
* Git checkout 
* Git merge 
* Staging Area

Let's quickly check if you have set your name and email address:

```sh
git config -l
```

If you don't see your name and email address, you should set them now:

```sh
git config --global user.name "John Doe"
git config --global user.email "john.doe@acme.git"
```

## 2. Gitflow
One of the major strengths of Git is its flexibility, which is why there are many different established workflows out in the wild. In this guide, we're discussing the standard workflow for working with open source software (on Github), called Gitflow. It’s a branching model designed around project deployment.

### Branch Types
There are two permanent branches:

* **Master**. This is the first branch of every Git repository and should always represent the current state on the live server (production). 
* **Dev**. Originating from the master branch, this is the place where development happens. Consequently this branch should represent the current state on the development/staging server.

Everyone will communicate with the main branches through pull requests only. **No direct pushes to main branches should ever happen.**

#### Supporting branch types
While `master` and `dev` are permanent branches, Gitflow also introduces supporting temporary branches:

| Type | Description | Naming |
| ------------- |-------------| -----|
| Hotfix | If you encounter a severe bug in the production environment that prevents proper functioning, the hotfix branch is the way to go. It is the only temporary branch originating from master and should only contain small fixes. Merge this branch in both dev and master after completion. | hotfix/<name> |
| Feature | This is the most common branch type you will be using. Originating from dev, this branch contains one logically definite feature and will be merged back into dev. | feature/<name> |
| Bugfix | Exactly the same as the Feature type. This is just a distinction for better readability later in the history of the repository. | bugfix/<name> |
| Release | When you’re ready to deploy a new release from dev to master it may be a good idea to use a release branch. If you’re working alone, this branch isn’t necessary. However if other team members will continue working on the dev branch, it makes sense to freeze a current state for release and do any bug fixes on this branch. Merge this branch both into dev and master. | release/<name> |

All development happens on these branches. The shorter the lifespan of said branches, the easier it will be to merge them later with your pull requests. After a successful merge, the branch is normally deleted (thus temporary).

### Pull Requests
When we’re talking about merging one branch into another, a pull request is always involved. In later graphics, an arrow from one branch to another represents a pull request. In other words, this is our tool for getting code from one branch to another. After a successful pull request, the temporary branch is normally deleted.

Pull requests are a feature of Git itself, however the “vanilla” way of creating a pull request would be copying a diff of your branch to the one you want to merge into, and then sending this diff via Email to the repository maintainer. Fortunately, services like Github simplify this process significantly by providing a GUI.

// todo: how to actually make a pull request.

### Forking
A fork is a copy of a repository. Forking a repository allows you to freely experiment with changes without affecting the original project. This is widely used in open source: The code base is publicly available on for example Github, but you won’t be able to directly push changes into the repository, as you’re not the maintainer and therefor don’t have the privileges to do so. The maintainer has the responsibility to decide, which changes will flow into his repository and which won’t. In other words, he accepts or declines pull requests.

Now, to create your own pull request, you will need your own repository -> your own fork.

So additionally to the main project repository, every involved employee will have his own fork of the repository. Make sure that your peers have read access to your fork.

// todo: how to create your own fork.

### Flow charts
This chapter was intentionally held short, because the past made clear that it’s easiest to explain Git using flowcharts. The next chapter contains a cheat sheet, picturing the life cycle of a project repository in a flowchart.

In the subpages you’ll find the single steps explained in depth. It's a good idea to try the commands on a real repository when going through the chapters.

## 3. Cookbook
### Project setup
### Hotfix
### Feature/Bugfix
### Release
### Rebase
### Advanced rebasing
### Clean up
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

See [CLI Aliases](#cli-alias) for shortening these steps.

## 4. Helpers
### CLI alias

## 5. Recommended tools

## Todo
* [ ] Improve .png version
* [ ] Write proper todo list