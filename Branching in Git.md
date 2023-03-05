## Overview

**_Branching_ is the process of evolving multiple versions of the software in parallel.** For example, one team member can create a new branch and add an experimental feature to it while the rest of the team keeps working on another branch. Branches can be given names e.g. `master`, `release`, `dev`.

**A branch can be _merged_ into another branch.** Merging usually results in a new commit that represents the changes done in the branch being merged.

![](https://nus-cs2103-ay2223s2.github.io/website/book/revisionControl/branching/images/diagram.png)

**_Merge conflicts_ happen when you try to merge two branches that had changed the same part of the code** and the RCS cannot decide which changes to keep. In those cases, you have to ‘resolve’ the conflicts manually.

## Branch - Doing multiple parallel changes

A Git branch is simply a _named label_ pointing to a *commit*. 

The `HEAD` label indicates *which branch* you are on.

Git creates a branch named `master` by default. When you add a commit, it goes into the branch you are currently on, and the branch label (together with the `HEAD` label) moves to the new commit.

##### Git branch demonstration

![[Pasted image 20230124231727.png]]

![[Pasted image 20230124231732.png]]

1.  There is only one branch (i.e., `master`) and there is only one commit on it.
2.  A new commit has been added. The `master` and the `HEAD` labels have moved to the new commit.
3.  A new branch `fix1` has been added. The repo has switched to the new branch too (hence, the `HEAD` label is attached to the `fix1` branch).
4.  A new commit (`c`) has been added. The current branch label `fix1` moves to the new commit, together with the `HEAD` label.
5.  The repo has switched back to the `master` branch.
6.  A new commit (`d`) has been added. The `master` label has moved to that commit.
7.  The repo has switched back to the `fix1` branch and added a new commit (`e`) to it.
8.  The repo has switched to the `master` branch and the `fix1` branch has been merged into the `master` branch, creating a _merge commit_ `f`. The repo is currently on the `master` branch.

##### Commands to branch repo

![[Pasted image 20230125004426.png]]

1. Start a branch named `feature1` and switch to the new branch

```
git branch feature1
git checkout feature1

# 1-step shortcut
git checkout -b feature1
```

2. Create some commits in the new branch. Just commit as per normal. These commits will be part of the `feature1` branch. Note how the `master` label and `HEAD` label move to the new commit
3. Switch to the `master` branch. Note the changes made in `feature1` branch are no longer in the working directory.

```
git checkout master
```

4. Add a commit to the master branch.
5. Switch back to the `feature1` branch
6. Merge the `master` branch to the `feature` branch.

```
git merge master
```

The objective of that merge was to **sync** the `feature1` branch with the `master` branch. This is to test and make sure any changes made to the `master` branch does not conflict with the changes you are working on in `feature1` branch.

> [!Avoid this common rookie mistake!]
> Always remember to switch back to the `master` branch before creating a new branch. If not, your new branch will be created on top of the current branch.

If you want to sync `master` branch with `feature1` branch instead, you `checkout` to `master`  then merge with `feature1`

```
git checkout master
git merge feature1
```

##### Fast Forward Merge

**Git does a _fast forward_ merge if possible**. Seeing that the `master` branch has not changed since you started the `add-countries` branch, Git has decided it is simpler to just put the commits of the `add-countries` branch in front of the `master` branch, without going into the trouble of creating an extra merge commit.

**It is possible to force Git to create a merge commit even if fast forwarding is possible.**

```
git merge --no-ff add-countries
```

##### Pushing a branch to a remote repo

```
git push {remote repo} {branch}
```

## Dealing with Merge Conflicts

**Merge conflicts happen when you try to combine two incompatible versions** (e.g., merging a branch to another but each branch changed the same part of the code in a different way).

After you merge and there is conflict, you have to resolve it yourself (by editing the files/codes manually). *Once done, stage the changes and commit.*









