## 1. Getting Started

This workflow heavily relies on branches and working with them. Hence we first introduce the tools involved to make Gitflow work.

### Branch Types

Gitflow differentiates between permanent and supporting branch types, where permanent branches usually represent a certain project state. The obvious example is the `master` branch, whose state should always be equal to the live environment. The supporting branches have a limited life time and are deleted once they are merged into one or both of the permanent branch types.

#### Permanent branch types

Usually there are only two permanent branches:

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
