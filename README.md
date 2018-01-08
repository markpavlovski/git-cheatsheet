# Notes on Git from Git Pro book

## Table of Contents

#### General

[git config](#config)  
[git remote](#remote)  
[git fetch | git pull](#fetch-pull)  
[git status](#status)  
[git log](#log)  
[git commit](#commit)  
[git tag](#commit)  
[git alias](#alias)  
[git show](#show)


#### Branching Basics


[git branch](#branch)  
[git checkout](#checkout)  
[git log](#branchlog)  
[git merge](#merge)




---

## General


<a name="config"></a>

### git config

--global specifies settings for user, --system for overall computer, and with no option just for the projects
* git config --global user.name "Mark Pavlovski"
* git config --global user.email "markpavlovski@gmail.com"
* git config --global core.editor vim

<a name="remote"/>

### git remote


* git remote -v: shows detailed remote addresses
* git remote add myfork https://github.com/mrkpvlvski/reponame
* git remote show origin: inspects remote branches

<a name="fetch-pull"/>

### git fetch | git pull

The difference is that fetch just pull the files down but does not automatically merge them. the pull command fetches and tries to merge automatically.

To use git pull with no options, an upstream needs to be set up.

* git fetch myfork master: the format is git fetch [remote name] [branch name]

<a name="status"/>

### git status

* git status -s: short option condenses the status output

<a name="log"/>

### git log

Shows the commit history, with a lot of different options

* git log --pretty=oneline
* git log --pretty=format:"%h-%an,%ar:%s"

<a name="commit"/>

### git commit
Each commit contains info on the 'parent' commit, file 'blobs' in the snapshot, and a unique hash.

* git commit -m "commit message here"
* git commit -amend: modifies last commit. Most common is to just change the message

<a name="tag"/>

### git tag

Tags are used to denote key commits in project history, like v1.0, etc. These can be long form (standard) or short form lightweight (that only stores a reference to the commit without storing committers info).
Tags do not automatically transfer to server with a push command

* git tag -a v1.0 -m "message"
* git show v1.0
* git tag v1.1-lw: lightweight is not the preferred way. Does not work with the -a,-s, or m versions.
* git show v1.1-lw
* git tag -a v1.2 9fceb02: this is used when tagging later, and refers to the hex or partial hex of the commit checksum
* git push origin v1.2: pushes the tag to the server
* git push origin --tags: pushes all the tags that are not already on the server

<a name="alias"/>

### git alias

Alias is a way to create your own git commands. Often used to short hand notations for common git commands or create custom commands that you feel should already be a thing.

* git alias: shows existing aliases
* git config --global alias.co checkout
* git config --global alias.br branch
* git config --global alias.st status
* git config --global alias.unstage 'reset HEAD --'
  * git unstage fileA
* git config --global alias.last 'log -1 HEAD'
  * git last: will return only the log of last commit
* git config --global alias.visual '!gitk': this is a way to run non-git commands; you simply include the "!" character.

<a name='show'/>

### git show

* git show 00fbe44a863077189e6cdf8ec79d99d44323896e: shows details of the commit object


---


## Branching Basics

Branching in git is a pointer to a commit. Its essentially a 41 bite file that holds a 40 character hex hash. A special HEAD pointer is used to specify which branch you are currently on.

There are several type of objects that get created along the way. For example, when you create three files in a brand new project and add then commit them, 5 files are created: master branch object that points to the latest commit in the branch (this only includes the hash of the commit it's pointing to), commit object that shows whats included in the snapshot of files added in the commit + some additional info (with a hexadecimal hash), and three files that were added.

<a name="branch"/>

### git branch

* git branch: shows existing branches
* git branch newbranchname
* git branch -d mybranchname: deletes the branch

<a name="checkout"/>

### git checkout
Warning: git checkout replaces the content of the working directory with whatever the target branch snapshot is. This may give errors if git cant do it cleanly.

* git checkout master: moves HEAD to master branch.
* git checkout otherbranch: moves HEAD pointer to otherbranch branch.

<a name="branchlog"/>

### git log
There are a couple of nice ways to visualize branching in the terminal

* git log  --oneline --decorate --graph --all
* git log  --oneline --decorate    

<a name="merge"/>

### git merge
Checkout the branch you want to merge onto first, then use the merge command
* git checkout master
* git merge testbranch -m "merge message": this will merge test branch onto master.
If there are no conflicts, this is very straight forward. This will create a new commit with the parent set to be both of the commits merged.
