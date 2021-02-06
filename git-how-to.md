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

```console
git merge <feature-branch>
```
