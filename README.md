**This is a work in progress.**

The goal of this repository is to have a shareable reference point for working with git, specifically using the gitflow workflow. Everything in this guide is heavily inspired and based on [nvie's original blog post](http://nvie.com/posts/a-successful-git-branching-model/). As he correctly realised, the easiest way to teaching git is using a "big picture" figure:

![Gitflow](gitflow-small.png)

Is this guide for you? Gitflow works well in mid-sized teams with multple deployment environments. There are reasons for not using any dev branch at all (in flat organisations), but it requires continuous live deployment, which is not always possible (when working for a customer, rather than on a product).

## Information
This section is only important if you're evaluating this to share with your colleagues. If you were sent here, [jump right to `Getting started`](#1-getting-started).

## 0. Table of contents
1. [Getting Started](#1-getting-started)
    * Git basics
    * Checklist
2. [Gitflow](#2-gitflow)
    * Introduction
    * Branch types
    * Pull Requests
    * Forking
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
To really grasp the concepts behind git, it is critical to get to know the basic commands. That’s why this guide will be using the command line. If you want to later streamline the process with a GUI (see recommended Tools) that’s fine, however command line is and should be the default.

Please take your time to go through each chapter in this guide and **ask your peers** in case something is unclear!

### Git basics
Because there’s already comprehensive documentation on Git basics available on the web and this guide focuses more on the workflow, I won’t cover them here. Instead, I provide links to resources I found best for starting with git. Please go through the following guides:

* [git - the simple guide](http://rogerdudler.github.io/git-guide/)
* [Got 15 minutes and want to learn Git?](https://try.github.io)

Now you should have a basic understanding of how to use git.

### Checklist
Make sure you understand the following commands and concepts before continuing:

* Git init/clone
* Git status
* Git Add
* Git reset
* Git commit Git push
* Git pull
* Git branch 
* Git checkout 
* Git merge 
* Staging Area

## 2. Gitflow
## 3. Cookbook
## 4. Helpers
## 5. Recommended tools

## Todo
* [ ] Improve .png version
* [ ] Write proper todo list