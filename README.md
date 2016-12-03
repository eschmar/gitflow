**This is a work in progress.**

The goal of this repository is to have a shareable reference point for working with git, specifically using the gitflow branching model. Everything in this guide is heavily inspired and based on [nvie's original blog post](http://nvie.com/posts/a-successful-git-branching-model/). As he correctly realised, the easiest way to teaching git is using a "big picture" figure:

<a href="https://github.com/eschmar/gitflow/blob/master/gitflow.pdf">
    ![Gitflow Life Cycle PDF Version](gitflow-link.png)
</a>

Is this guide for you? Gitflow works well in mid-sized teams with multple deployment environments. There are reasons for not using any dev branch at all (in flat organisations), but it requires continuous live deployment, which is not always possible (when working for a customer, rather than on a product).

## 0. Table of contents
1. [Getting Started](#1-getting-started)
    * Git basics
    * Checklist
    * Create a pull request
    * Create a fork
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
