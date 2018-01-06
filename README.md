# Notes on Git from Git Pro book

## Table of Contents  
[git config](#config)  
[git remote](#remote)  
[git fetch | git pull](#fetch-pull)  
[git status](#status)  
[git log](#log)  
[git commit](#commit)  

## Notes


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

* git commit -m "commit message here"
* git commit -amend: modifies last commit. Most common is to just change the message
