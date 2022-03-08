+++
title = "Top 20 lệnh sử dụng Git và ví dụ"
description = "Top 20 lệnh sử dụng Git và ví dụ"
tags = ["Git", "Git command", "lệnh sử dụng Git", "sử dụng Git"
, "git config", "git init", "git clone", "git add", "git commit", "git diff", "git reset", "git status", "git rm", "git log", "git show", "git tag", "git branch", "git checkout", "git merge", "git remote", "git push", "git pull", "git stash"]
keywords = ["Git", "Git command", "lệnh sử dụng Git", "sử dụng Git"
, "git config", "git init", "git clone", "git add", "git commit", "git diff", "git reset", "git status", "git rm", "git log", "git show", "git tag", "git branch", "git checkout", "git merge", "git remote", "git push", "git pull", "git stash"]
date = "2022-03-08"
+++

Top 20 lệnh Git hàng đầu mà bạn sẽ sử dụng thường xuyên khi làm việc với Git.

Dưới đây là các lệnh Git đang được đề cập:

* git config
* git init
* git clone
* git add
* git commit
* git diff
* git reset
* git status
* git rm
* git log
* git show
* git tag
* git branch
* git checkout
* git merge
* git remote
* git push
* git pull
* git stash

# Bắt đầu thôi

## **git config**

Usage: `git config –global user.name “[name]”`

Usage: `git config –global user.email “[email address]”`

This command sets the author name and email address respectively to be used with your commits.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/1-9.png)

## **git init** 
Usage: `git init [repository name]`

This command is used to start a new repository.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/2-6.png)

## **git clone**
Usage: `git clone [url]`

This command is used to obtain a repository from an existing URL.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/4-4.png)

## **git add**
Usage: `git add [file]`

This command adds a file to the staging area.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/5-4.png)

Usage: `git add *`

This command adds one or more to the staging area.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/6-3.png)

## **git commit**
Usage: `git commit -m “[ Type in the commit message]”`  

This command records or snapshots the file permanently in the version history.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/7-3.png)

Usage:` git commit -a`

This command commits any files you’ve added with the git add command and also commits any files you’ve changed since then.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/8-2.png)

## **git diff**
Usage: `git diff`

This command shows the file differences which are not yet staged.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/9-2.png)

Usage: `git diff –staged`

This command shows the differences between the files in the staging area and the latest version present.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/10-2.png)

Usage: `git diff [first branch] [second branch]` 

This command shows the differences between the two branches mentioned.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/43.png)

## **git reset**
Usage: `git reset [file]`

This command unstages the file, but it preserves the file contents.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/11-1.png)

Usage: `git reset [commit]`

This command undoes all the commits after the specified commit and preserves the changes locally.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/14-1.png)

Usage: `git reset –hard [commit]`

This command discards all history and goes back to the specified commit.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/13-1.png)

## **git status**
Usage: `git status`

This command lists all the files that have to be committed.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/15-1.png)

## **git rm**
Usage: `git rm [file]`

This command deletes the file from your working directory and stages the deletion.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/16-2.png)

## **git log**
Usage: `git log`

This command is used to list the version history for the current branch.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/18.png)

Usage: `git log –follow[file]`

This command lists version history for a file, including the renaming of files also.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/19.png)

## **git show**
Usage: `git show [commit]`  

This command shows the metadata and content changes of the specified commit.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/20.png)

## **git tag**
Usage: `git tag [commitID]`

This command is used to give tags to the specified commit.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/22.png)

## **git branch**
Usage: `git branch`

This command lists all the local branches in the current repository.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/23.png)

Usage: `git branch [branch name]`  

This command creates a new branch.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/24.png)

Usage: `git branch -d [branch name]`  

This command deletes the feature branch.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/25.png)

## **git checkout**
Usage: `git checkout [branch name]`

This command is used to switch from one branch to another.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/27.png)

Usage: `git checkout -b [branch name]`

This command creates a new branch and also switches to it.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/28.png)

## **git merge**
Usage: `git merge [branch name]`  

This command merges the specified branch’s history into the current branch.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/31-1.png)

## **git remote**
Usage: `git remote add [variable name] [Remote Server Link]` 

This command is used to connect your local repository to the remote server.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/32.png)

## **git push**
Usage: `git push [variable name] master`

This command sends the committed changes of master branch to your remote repository.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/33.png)

Usage: `git push [variable name] [branch]  `

This command sends the branch commits to your remote repository.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/34.png)

Usage: `git push –all [variable name]` 

This command pushes all branches to your remote repository.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/36.png)

Usage: `git push [variable name] :[branch name]`

This command deletes a branch on your remote repository.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/37.png)

## **git pull**
Usage: `git pull [Repository Link]`

This command fetches and merges changes on the remote server to your working directory.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/38.png)

## **git stash**
Usage: `git stash save`

This command temporarily stores all the modified tracked files.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/39.png)

Usage: `git stash pop ` 

This command restores the most recently stashed files.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/40.png)

Usage: `git stash list`

This command lists all stashed changesets.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/44.png)

Usage: `git stash drop`

This command discards the most recently stashed changeset.

![Git Commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/07/42.png)

# Tham khảo
[https://dzone.com/articles/top-20-git-commands-with-examples](https://dzone.com/articles/top-20-git-commands-with-examples)