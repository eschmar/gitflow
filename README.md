**This is a work in progress.**

The goal of this repository is to have a shareable reference point for working with git, specifically using the gitflow branching model. Everything in this guide is heavily inspired and based on [nvie's original blog post](http://nvie.com/posts/a-successful-git-branching-model/). As he correctly realised, the easiest way to teaching git is using a "big picture" figure:

<a href="https://github.com/eschmar/gitflow/blob/master/gitflow.pdf">
    <img width="580" src="https://github.com/eschmar/gitflow/raw/master/pdf-link.png" alt="Gitflow Life Cycle PDF Version">
</a>

Is this guide for you? Gitflow works well in mid-sized teams with multple deployment environments. There are reasons for not using any dev branch at all (in flat organisations), but it requires continuous live deployment, which is not always possible (when working for a customer, rather than on a product).

Since there is already comprehensive documentation on Git basics available on the internet, they won't be covered here. Instead, I assume that you are already somewhat familiar with git and refer you to other resources otherwise:

* [git - the simple guide](http://rogerdudler.github.io/git-guide/)
* [Got 15 minutes and want to learn Git?](https://try.github.io)

Please take your time to go through each chapter in this guide and **ask your peers** in case something is unclear!

## 0. Table of contents
1. [Getting Started](#1-getting-started)
    * Branch types
    * Pull Requests
    * Forking
2. [The Big Picture](#2-the-big-picture)
    * Project setup
    * Hotfix
    * Feature/Bugfix
    * Release
    * Rebase
    * Advanced rebasing
    * Clean up
3. [Nuggets](#3-nuggets)
    * CLI alias
4. [Recommended tools](#4-recommended-tools)

---

## 1. Getting Started

//todo: Hereafter we describe the tools involved to make gitflow work.

### Branch Types

Gitflow differentiates between permanent and supporting branch types, where permanent branches usually represent a certain project state. The obvious example is the `master` branch, whose state should always be equal to the live environment.

#### Permanent branch types

There are two permanent branches:

* **Master**. This is the first branch of every Git repository and should always represent the current state on the live server (production). 
* **Dev**. Originating from the master branch, this is the place where development happens. Consequently this branch should represent the current state on a testing server.

Everyone will communicate with the main branches through pull requests only. **No direct pushes to main branches should ever happen.**

#### Supporting branch types

| Type | Description | Naming |
| :------------- | :------------- | :----- |
| Hotfix | This is the only temporary branch originating from `master` and should only be used for severe bugfixes that prevent production from running properly. Merge this branch in both `dev` and `master` after completion. | hotfix/<name> |
| Feature | The most common branch type you will be using. Originating from `dev`, this branch contains one logically definite feature and will be merged back into `dev`. | feature/<name> |
| Bugfix | Exactly the same as the Feature type. This is just a distinction in name for better readability. | bugfix/<name> |
| Release | This branch is used when the development on the `dev` branch continues, but the features for a new milestone have been frozen. Only bugfixes should be added to this branch after creation and it should be first merged into `master` and then `dev` upon release. | release/<name> |

All development happens on these branches. The shorter the lifespan of said branches, the easier it will be to merge them later. After a successful merge, supporting branches are normally deleted (thus temporary).


### Pull Request

When we’re talking about merging one branch into another, a pull request is always involved. In later graphics, an arrow directed to the right side represents a pull request. Or in other words, this is our tool for getting code from one branch to another.

Pull requests are a feature of Git itself, however the “vanilla” way of creating a pull request would be copying a diff between your branch and the one you want to merge into, and then sending this diff via Email to the repository maintainer. Fortunately, services like Github simplify this process significantly by providing a GUI.


### Forking

A fork is a complete copy of a repository. This is widely used in open source: The code base is publicly available on for example Github, but you won’t be able to directly push changes into the repository, as you’re not the maintainer and therefor don’t have the privileges to do so. By creating your own fork, you can freely experiment without affecting the original project. The maintainer then has the responsibility to decide, which changes will flow into his repository and which won’t. In other words, he accepts or declines pull requests originating from forks.

So additionally to the main project repository, every involved employee will have his own fork. Make sure that your peers have at least read access to your fork.



## 2. The Big Picture

The previous chapter was intentionally held short, because by experience it’s easiest to explain Git using flowcharts. This chapter introduces the "big picture", a flowchart picturing the life cycle of a project repository in Gitflow. Each of the steps will be explained in their own subchapter.


### Hotfix
// todo

### Feature/Bugfix
// todo

### Release
// todo

### Rebase
// todo

### Clean up
// todo



## 3. Nuggets
// todo



## 4. Recommended Tools
// todo
