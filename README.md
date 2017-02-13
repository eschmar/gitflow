**This is a work in progress.**

The goal of this repository is to have a shareable reference point for working with git, specifically using the gitflow branching model. Everything in this guide is heavily inspired and based on [nvie's original blog post](http://nvie.com/posts/a-successful-git-branching-model/). As he correctly realised, the easiest way to teaching git is using a "big picture" figure:

<a href="https://github.com/eschmar/gitflow/blob/master/gitflow.pdf">
    <img width="580" src="https://github.com/eschmar/gitflow/raw/master/pdf-link.png" alt="Gitflow Life Cycle PDF Version">
</a>

Is this guide for you? Gitflow works well in mid-sized teams with multple deployment environments. There are reasons for not using any dev branch at all (in flat organisations), but it requires continuous live deployment, which is not always possible (when working for a customer, rather than on a product).

Since there is already comprehensive documentation on Git basics available on the internet, they won't be covered here. Instead, I assume that you are already somewhat familiar with git and refer you to other resources otherwise:

* [git - the simple guide](http://rogerdudler.github.io/git-guide/)
* [Got 15 minutes and want to learn Git?](https://try.github.io)

Please take your time to go through each chapter in this guide and **ask your peers** in case something is unclear! It's advicable to have a printed version of the PDF at hand.

## Table of contents
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
    * Clean up
3. [Nuggets](#3-nuggets)
    * Advanced rebasing
    * Undo commits
    * CLI aliases
