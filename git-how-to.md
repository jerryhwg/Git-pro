# Git How-To

## git branch management

list all local branches
```console
git branch
```

create a new branch
```console
git branch <name>
```

checkout a specific branch
```console
git checkout <name>
```

delete a specific branch
```console
git branch -d <name>
```

rename a specific branch
```console
git branch -m <old> <new>
```

shortcut for creating a branch with checkout
```console
git checkout -b <name>
```

## merging branches

**fast forward**: when there are no further commits in the receiving branch (master) after the commits where feature branch was created

1. create a new feature branch from the main branch (master)
2. make changes in the new branch and commit them
3. checkout to master branch (receiving branch)
4. merge feature branch to the receiving branch (master)

**3 way merge**

1. create a new branch
2. add commits in the new branch
3. checkout to master and add some commits there
4. merge the branch into the master branch

```console
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

push to remote repository
```console
git push
```

fetch update from remote repository to local git repository
```console
git fetch
git fetch -v
```

merge remote branch into current branch(working directory)

`git pull` = `git fetch` + `git merge FETCH_HEAD`
```console
git pull
git pull -v
```

NOTE: git pull updates only single local currently checked out branch

check remote repository
```console
git remote -v
```

list all (local and remote) branches
```console
git branch -a
```

tracking branch
```console
git branch -vv
```
NOTE: checkout remote branch will auto create (tracking) a local branch

git remote show origin
```console
git remote show origin
```

clean up after deleting branch on remote origin
```console
git remote prune origin
git branch -d <name>
```

create remote branch based on local branch
```console
git checkout -b <name>
# make some changes and commits
git push -u
```