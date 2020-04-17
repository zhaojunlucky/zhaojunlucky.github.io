---
date: 2018-01-15 11:29:08 +0800
categories: github git branch sync
title: GitHub Branch Code Sync
update: 2018-12-11 13:34:18 +0800
---

## Sync From Forked Repository
1. Check is upstream configured
  - run `git remote -v` to check upstream configuration
  - run `git remote add upstream {upstream repo path}` if upstream is not well configured
2. run `git fetch upstream` to fetch upstream to local
3. run `git merge upstream/{upstream branch}` to merge upstream branch to local branch
4. run `git push origin {local branch}` to push changes

## Squash Commits and Sync From Head Branch
1. run `git log` to find the commit id which will be squashed from
2. run `git reset --soft {commit id}` to bring up all the commits after it in the editor
3. run `git add .` to add all the changes
4. run `git commit -m "{message}"` to commit the changes
5. run `git push -f origin {local branch}` to push changes

> Note: you need do squash before sync from head branch, if you need do squash

run `git pull` to pull the head branch first, then run `git merge origin/{head branch}` to sync changes to local branch, and run `git push origin {local branch}` to push.

## Import New Branch From Upstream

1. run `git fetch upstream`
2. run `git checkout -b {new local branch name} upstream/{upstream new branch}`
3. run `git push -u origin {new local branch name}` to push the new local branch

## Pull master Branch's Change to Dev Branch
Assume currently in the development branch, and want to merge the master branch's change to current banch, Run `git pull origin master:master`, it will do pull, update master branch and merge into current development branch.

## Update Submodule

1. Checkout Submodule
    * Check one submodule

      Run `git submodule update --init {submodule relative path}`

    * Check all submodule
      Run `git clone --recursive`
2. Update Submodule
    * Go to the submodule source folder, and checkout a new commit
    * Go to the root folder, commit as usual.
