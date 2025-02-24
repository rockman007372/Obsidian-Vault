---
tag: remote repo, github, RCS
date: Jul 3, 2022
course: CS2103T
---
- [[What is a Remote Repo]]
- [[How to Interact with a Remote Repo]]
- [[Git Development Workflow]]

## Summary

![[Pasted image 20230118003300.png]]


![[Pasted image 20220727225646.png]]

## Questions

### What is the difference between git pull and git fetch?
- `git fetch` is similar to `pull` but doesn't merge. i.e. it fetches remote updates (`refs` and `objects`) but your local stays the same (i.e. `origin/master` gets updated but `master` stays the same) .

- `git pull` pulls down from a remote and instantly merges.

How to use this in practice:
1.  Update your local repo from the remote (but don't merge):
    
    ```
     git fetch 
    ```
    
2.  After downloading the updates, let's see the differences:
    
    ```
     git diff master origin/master 
    ```
    
3.  If you're happy with those updates, then merge:
    
    ```
     git pull
    ```

### What is the difference between git clone and git pull

**tldr; think of 'clone' as "make me a local copy of that repo" and 'pull' as "get me the updates from some specified remote.**

`git clone` is how you get a local copy of an existing repository to work on. It's usually only used once for a given repository, unless you want to have multiple working copies of it around. (Or want to get a clean copy after messing up your local one...)

`git pull` (or `git fetch` + `git merge`) is how you _update_ that local copy with new commits from the remote repository. If you are collaborating with others, it is a command that you will run frequently.

As your first example shows, it is possible to emulate `git clone` with an assortment of other git commands, but it's not really the case that `git pull` is doing "basically the same thing" as `git clone` (or vice-versa).