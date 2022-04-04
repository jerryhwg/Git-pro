# Git How-To

## Contents

* [git branch management](https://github.com/jerryhwg/git_pro/blob/main/git-how-to.md#git-branch-management])
* [merging branches](https://github.com/jerryhwg/git_pro/blob/main/git-how-to.md#merging-branches)
* [git push, fetch, pull](https://github.com/jerryhwg/git_pro/blob/main/git-how-to.md#git-push-fetch-pull)
* [pull requests](https://github.com/jerryhwg/git_pro/blob/main/git-how-to.md#pull-requests)
* [git tags](https://github.com/jerryhwg/git_pro/blob/main/git-how-to.md#git-tags)
* [git rebase](https://github.com/jerryhwg/git_pro/blob/main/git-how-to.md#git-rebase)
* [git ignore](https://github.com/jerryhwg/git_pro/blob/main/git-how-to.md#git-ignore)
* [git log](https://github.com/jerryhwg/git_pro/blob/main/git-how-to.md#git-log)
* [git reset](https://github.com/jerryhwg/git_pro/blob/main/git-how-to.md#git-reset)
* [git revert](https://github.com/jerryhwg/git_pro/blob/main/git-how-to.md#git-revert)
* [git advanced](https://github.com/jerryhwg/git_pro/blob/main/git-how-to.md#git-advanced)

## git branch management

List all local branches

```bash
git branch
```

List all (local and remote) branches

```bash
git branch -a
```

> **VS Code**: left bottom corner click `main` to view local and remote branches

Create a new branch

```bash
git branch <name>
```

> **VS Code**: left pane -> Source Control -> Branch -> Create Branch

Checkout a specific branch

```bash
git checkout <name>
```

> **VS Code**: left bottom corner click `main` -> select a branch to check out to

Delete a specific branch

```bash
git branch -d <name>
```

> **VS Code**: left pane -> Source Control -> Branch -> Delete Branch -> Select a branch to delete

Rename a specific branch

```bash
git branch -m <old> <new>
```

> **VS Code**: check out to a branch -> left pane -> Source Control -> Branch -> Rename Branch -> Rename

Shortcut for creating a branch with checkout

```bash
git checkout -b <name>
```

> **VS Code**: left pane -> Source Control -> Branch -> Create Branch -> Name one for the new branch

## merging branches

**fast forward**: when there are no further commits in the receiving branch (master) after the commits where feature branch was created

1. create a new feature branch from the main branch (master)
2. make changes in the new branch and commit them
3. checkout to master branch (receiving branch)
4. merge feature branch to the receiving branch (master)

**3 way merge (no conflict)**:

1. create a new branch
2. add commits in the new branch
3. checkout to master and add some commits there
4. merge the branch into the master branch

```bash
git checkout master
git merge <feature-branch>
```

**merge conflicts**: same files were edited in both branches

1. create a new branch
2. change a file in the new branch
3. return to the master branch and change the same file
4. try to merge the new branch to the master branch
5. resolve conflicts manually
6. stage the file with resolved conflicts
7. commit changes
8. git will create merge commit

## git push, fetch, pull

Push to remote repository

```bash
git push
```

Push while creating a new remote repository

```bash
git push --set-upstream origin {new branch name}
```

Fetch update from remote repository to local git repository

```bash
git fetch
git fetch -v
```

Pull: Merge remote branch into current branch(working directory)

`git pull` = `git fetch` + `git merge FETCH_HEAD`

```bash
git pull
git pull -v
```

`NOTE: git pull updates only single local currently checked out branch`

Check remote repository

```bash
git remote -v
```

List all (local and remote) branches

```bash
git branch -a
```

Tracking branch

* View what tracking branches you have set up
* list out your local branches with more information including what each branch is tracking and if your local branch is ahead, behind or both

```bash
git branch -vv
```

`NOTE: checkout remote branch will auto create a local branch (tracking)`

Git remote show origin

* View more information about a particular remote
* It lists the URL for the remote repository as well as the tracking branch information

```bash
git remote show origin
```

Create a remote branch after creating a branch on the local repository

```bash
git checkout -b <name>
# make some changes and commits
git push -u origin <name>
```

Clean up after deleting a branch in the remote repository

```bash
# in the branch
git remote prune origin
git branch -d <name>
```

Update tracking status after deleting a branch in the remote repository

```bash
# create a branch in the remote repository
git fetch
git branch -a
git checkout <name>
# delete a branch in the remote repository
git fetch
git branch -vv
git remote update origin --prune
git branch -vv
# to remove the branch locally
git branch -d <name>
```

Delete a remote branch from local terminal

```bash
git checkout <name>
git push origin -d <name>
git checkout master
git branch -D <name>
git branch -a
```

git show-ref

list references in a local repository

```bash
git show-ref
git show-ref master
```

## pull requests

pull request: github, bitbucket

merge reuqest: gitlab

## git tags

list git tag

```bash
git tag
```

create a new tag # 1 (lightweight)

```bash
git tag v1.0.0
```

show dtail of a tag

```bash
git show v1.0.0
```

create a new tag # 2 (annotated)

```bash
git tag -a v1.0.0 -m "Initial tag"
git tag -v v1.0.0
```

pushing tag to remote

```bash
git push --tags

git push -v origin v1.0.1
```

## git rebase

```bash
git checkout feature1
# rebase feature1 branch on top of the base(master) branch
git rebase master
git checkout master
# merge feature branch into the base(master) branch using fast forward
git merge feature1
git branch -d feature1
git push -v
```

## git ignore

Useful links

* https://www.toptal.com/developers/gitignore
* https://github.com/github/gitignore 

Untrack files already added to git repository based on .gitignore
* https://www.codeblocq.com/2016/01/Untrack-files-already-added-to-git-repository-based-on-gitignore/

## git log

git lg

```bash
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr)%C(bold blue)<%an>%Creset' --abbrev-commit"
```

git log

```bash
git log
git log --oneline
git log --graph (--oneline)
git log --stat
git log -5 (--oneline)
```

```bash
git shortlog -n -s -e
```

```bash
git log --author="JH"
git log --all --grep='Build v1.0'
```

## git reset

git reset (mixed)

* `git reset --mixed <SHA hash>`
* discard commit
* discard changes in staging area (index)
* keep changes in working directory
  
```bash
git reset <commit id to move to>
```

git reset --soft

* discard commit
* keep changes in staging area (index)
* keep changes in working directory
  
```bash
git reset --soft <commit id to move to>
```

git reset --hard

* discard commit
* discard changes in staging area (index)
* discard changes in working directory
  
```bash
git reset --hard <commit id to move to>
```

reset last 5 commits

```bash
git reset HEAD~5
```

## git revert

git revert is used to record some new commits to reverse the effect of some earlier commits (often only a faulty one)

* only a single commit
* not delete a history

check a commit to revert

```bash
git show <SHA ID>
```

git revert

```bash
git revert <commit id to remove>
git revert HEAD (= last commit)
git revert HEAD~3
git revert --continue
```

## git advanced

cherry-picking

```bash
git cherry-pick <SHA ID of a commit from another branch>
git cherry-pick --no-commit <SHA ID of a commit from another branch>
```

git stashing

* useful for unsaved (uncommited) works when switching to another branch
  
```bash
git stash
git stash pop
```

git squash and merge

* multiple commits from this branch will be combined into one branch

git rebasing with squashing

* multiple commits from this branch will be rebased

git amend

```bash
git commit --amend -m "new message for the last commit"
git commit --amend --author="JH <jh@email.local>"
```

reflog

* log of all git operations
* local repository only
* 90 days keep

Garbage collection

```bash
git gc
```

Local init and remote add

```bash
git init
git add .
git commit -m "initial commits"
git remote add origin git@github.com:jerryhwg/docker-react.git
git push --set-upstream origin main
```

Get the latest commit SHA

```bash
git rev-parse HEAD
```

## Appendix: notes

1. Avoid using git rebase, reset, amend in prod, release branch

2. [GitHub ssh-key setup](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh)