## 1. Getting Started

This chapter introduces the tools necessary for gitflow to work. The workflow aims to separate concerns and facilitate contribution among your team by making heavy use of branches. Any new code will be written in a branch holding a descriptive name, following certain naming conventions.

* [Branch Types](#branch-types)
* [Pull Requests](#pull-requests)
* [Forking](#forking)

### Branch Types

Gitflow differentiates between *permanent* and *supporting branch types*. As a general rule, branches should have a short lifespan and be deleted after being merged. However, permanent branches will theoretically live forever and represent a specific project state. The obvious example is the `master` branch, whose state should always be equal to the production environment. When code is merged into a permanent branch, ideally continuous integration kicks in and deploys the new state right away. We want to achieve confidence in the state of our project and avoid deploys on Friday nights of several hundred commits difference.

Following you'll find a list of the individual branch types and naming conventions. Of course this is not set in stone and you may adjust it by adding ticket numbers of your project management tool or similar.


#### Permanent branch types

Usually there are only two permanent branches:

* **Master**. This is the first branch of every Git repository and should always represent the current state on the live server (production). 
* **Dev**. Originating from the master branch, this is the place where development happens. Consequently this branch should represent the current state on a testing server.

Everyone will communicate with the main branches through pull requests only. 

> **No direct pushes to main branches should ever happen.**


#### Supporting branch types

| Type | Description | Prefix |
| :------------- | :------------- | :----- |
| Hotfix | This is the only temporary branch originating from `master` and should only be used for severe bugfixes that prevent production from running properly. | hotfix/<name> |
| Feature | The most common branch type you will be using for adding new features to your project. | feature/<name> |
| Bugfix | Exactly the same as the Feature type. This is just a distinction in name for better readability. | bugfix/<name> |
| Release | This branch is used when the development on the `dev` branch continues, but the features for a new milestone have been frozen. Only bugfixes should be added to this branch after creation. | release/<name> |

All development happens on these branches. The shorter the lifespan of said branches, the easier it will be to merge them later. After a successful merge, supporting branches are usually deleted (thus temporary).

#### Naming conventions

All branch names should be lowercase with dashes. Examples:
* `feature/shop-basket`
* `bugfix/shop-basket-double-entries`

### Pull Requests

When we’re talking about merging one branch into another, a pull request is always involved. In later graphics, an arrow directed to the right side represents a pull request. Or in other words, this is our tool for getting code from one branch to another.

Pull requests are a feature of Git itself, however the “vanilla” way of creating a pull request would be copying a diff between your branch and the one you want to merge into, and then sending this diff via Email to the repository maintainer. Fortunately, services like Github simplify this process significantly by providing a GUI.

Since this process is different depending on the service you are using, I'm simply linking here to the tutorial for Github:

[Creating a pull request](https://help.github.com/articles/creating-a-pull-request/)

### Forking

A fork is a complete copy of a repository. This is widely used in open source: The code base is publicly available, but you won’t be able to directly push changes into the repository, as you’re not the maintainer and therefor don’t have the privileges to do so. By creating your own fork, you can freely experiment without affecting the original project. The maintainer then has the responsibility to decide, which changes will flow into his repository and which won’t. In other words, he accepts or declines pull requests originating from forks.

This minimizes any danger of breaking something in the main repository, as you can `push --force` as much as you want in your own fork. It won't have any consequences and can be easily restored.

So additionally to the main project repository, every involved employee will have his own fork. Make sure that your peers have at least read access to your fork.

[Fork a repo on Github](https://help.github.com/articles/fork-a-repo/)


---

Next up: [The big picture](../2-big-picture)
