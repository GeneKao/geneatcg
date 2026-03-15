---
title: "Using Git like a Pro"
date: 2020-04-01
tags: ["blog", "git", "teaching"]
description: "Git tutorial 101."
cover:
  image: "git-flow.png"
  alt: "Git flow diagram"
  relative: true
  hiddenInSingle: true
---

I wrote a Git tutorial a while ago and share it on the [GitHub](https://github.com/GeneKao/programming-notes/tree/master/git).
Now I would like to share it again here on my website.

To see some of my other notes, please have a look at my [programming-notes](https://github.com/GeneKao/programming-notes).

### Table of Contents

1. [Git vs GitHub vs GitLab](#1)
2. [Set up your Git](#2)
3. [Basic commands](#3)
4. [Review a repo's history](#4)
5. [Add commit to a repo](#5)
6. [Tagging, branching, merging](#6)
7. [Experiments using checkout](#7)
8. [Undoing changes](#8)
9. [Collaborating and syncing with GitLab](#9)
10. [Other useful commands](#10)
11. [Development pipeline, branching model and discussion](#11)


### Appendix

A. [Git Bash setup](#12)
B. [Cygwin setup](#13)


## 1. Git vs GitHub vs GitLab <a name="1"></a>

![](https://raw.githubusercontent.com/GeneKao/programming-notes/master/git/img/git-1-1.bmp)

Figure 1‑1: Icon of Git, Github and GitLab.

Git is a very powerful tool that every developer should be familiar with.

> By far, the most widely used modern version control system in the world
> today is Git. Git is a mature, actively maintained open-source project
> originally developed in 2005 by Linus Torvalds, the famous creator of the Linux
> operating system kernel. A staggering number of software projects rely on Git
> for version control, including commercial projects as well as open-source.
[Atlassian.com](https://www.atlassian.com/git/tutorials/what-is-git)

However, many people confuse Git with Github, GitLab, but they are not the same.
[**Git**](https://git-scm.com/) **is a free and open-source distributed version
control system, a tool that you can manage your code history. Where**
[**Github**](https://github.com/) **and** [**GitLab**](https://about.gitlab.com/)
**are web-based hosting services for Git repositories. With Git, you don't even need Internet access, you can
work everything locally and have all version controls.**

More discussion about Git and Github can be found here in the [Stack Overflow](https://stackoverflow.com/questions/13321556/difference-between-git-and-github).

Here are some nice free tutorials you can find online:

1. [Official Git documentation](https://git-scm.com/docs/gittutorial).
2. [Learn Git with Bitbucket Cloud](https://www.atlassian.com/git/tutorials/learn-git-with-bitbucket-cloud).
3. Udacity: [Version Control with Git](https://www.udacity.com/course/version-control-with-git--ud123) and [How to Use Git and Github](https://www.udacity.com/course/how-to-use-git-and-github--ud775).
4. [Learn Enough Git to Be Dangerous](https://www.learnenough.com/git-tutorial).
5. [Try Git: Git Tutorial](https://try.github.io/levels/1/challenges/1).

## 2. Set up your Git <a name="2"></a>

You should do those configuration commands below before start using git.

``` bash
$ git config --global user.name "Git Rock"
$ git config --global user.email "git.rock@email.com"
$ git config --global color.ui auto
$ git config --global merge.conflictstyle diff3
$ git config --global core.editor "emacs -nw"
$ git config --list
```

## 3. Basic commands <a name="3"></a>

``` bash
$ git init
$ git clone https://github.com/GeneKao/udacity-build-a-portfolio-site.git
$ git status
$ git log
$ git add
$ git commit
$ git diff
```

## 4. Review a repo's history <a name="4"></a>

``` bash
$ git log --oneline --graph --all
$ git show
$ git diff
```

## 5. Add commit to a repo <a name="5"></a>

``` bash
$ git add <file>
$ git commit -m "message"
$ git stash
```

## 6. Tagging, branching, merging <a name="6"></a>

``` bash
$ git tag -a v1.0
$ git branch
$ git branch dev_frontend
$ git checkout dev_frontend
$ git merge dev_frontend
```

## 7. Experiments using checkout <a name="7"></a>

``` bash
$ git checkout dev_frontend
$ git checkout 43s20r
$ git checkout HEAD
```

## 8. Undoing changes <a name="8"></a>

``` bash
$ git commit --amend
$ git revert 43s20r
$ git reset HEAD~1
$ git reset --mixed HEAD~1
$ git reset --soft HEAD~1
$ git reset --hard HEAD~1
```

## 9. Collaborating and syncing with GitLab <a name="9"></a>

``` bash
$ git remote
$ git fetch
$ git pull
$ git push
```

## 10. Other useful commands <a name="10"></a>

``` bash
$ git diff-tree --no-commit-id --name-only -r d51488d
$ git ls-tree --name-only -r d51488d
```

## 11. Development pipeline, branching model and discussion <a name="11"></a>

See the full tutorial at [programming-notes on GitHub](https://github.com/GeneKao/programming-notes/tree/master/git).
