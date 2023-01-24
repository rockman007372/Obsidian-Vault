---
tags: version control, SWE
course: CS2103T
aliases: 
date: 2023-01-18 Wednesday
---

>[!definition]
> **RCS**: **Revision control software** are the software tools that automate the process of _Revision Control_ i.e. managing revisions of software artifacts.

![[Pasted image 20230119142412.png]]

[[Benefits of Git]]

[[Git Repositories]]

[[Staging and Committing in Git]]

[[Omitting files from revision control]]

[[Using History in Git]] 

## Branching in Git

**_Branching_ is the process of evolving multiple versions of the software in parallel.** For example, one team member can create a new branch and add an experimental feature to it while the rest of the team keeps working on another branch. Branches can be given names e.g. `master`, `release`, `dev`.

**A branch can be _merged_ into another branch.** Merging usually results in a new commit that represents the changes done in the branch being merged.

![](https://nus-cs2103-ay2223s2.github.io/website/book/revisionControl/branching/images/diagram.png)**Branching and merging**

**_Merge conflicts_ happen when you try to merge two branches that had changed the same part of the code** and the RCS cannot decide which changes to keep. In those cases, you have to ‘resolve’ the conflicts manually.

### Branch - Doing multiple parallel changes

A Git branch is simply a _named label_ pointing to a *commit*. 

The `HEAD` label indicates *which branch* you are on.

Git creates a branch named `master` by default. When you add a commit, it goes into the branch you are currently on, and the branch label (together with the `HEAD` label) moves to the new commit.

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












---
- For a quick recap of all the commands: [[Git Basic Commands]]
- To learn more about remote repository: [[GitHub and Remote Repository]]