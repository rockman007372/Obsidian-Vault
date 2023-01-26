---
tag: remote repo, github, RCS
date: Jul 3, 2022
course: CS2103T
type: content
---
## Overview

**Remote repositories are repos that are hosted on remote computers** and allow remote access. They are especially useful for sharing the revision history of a codebase among team members of a multi-person project. They can also serve as a remote backup of your codebase.

**It is possible to set up your own remote repo on a server**, but the easier option is to use a remote repo hosting service such as GitHub or BitBucket.

**You can _clone_ a repo** to create a copy of that repo in another location on your computer. The copy will even have the revision history of the original repo i.e., identical to the original repo. For example, you can clone a remote repo onto your computer to create a local copy of the remote repo.  

**When you clone from a repo, the original repo is commonly referred to as the _upstream_ repo.** A repo can have multiple upstream repos. For example, let's say a repo `repo1` was cloned as `repo2` which was then cloned as `repo3`. In this case, `repo1` and `repo2` are upstream repos of `repo3`.

**You can _pull_ from one repo to another, to receive new commits in the second repo**, if the repos have a shared history. Let's say some new commits were added to the `upstream` repo after you cloned it and you would like to copy over those new commits to your own clone i.e., sync your clone with the upstream repo. In that case, you pull from the upstream repo to your clone.

**You can _push_ new commits in one repo to another repo** which will copy the new commits onto the destination repo. Note that pushing to a repo requires you to have write-access to it. Furthermore, you can push between repos only if those repos have a shared history among them (i.e., one was created by copying the other at some point in the past).

Cloning, pushing, and pulling can be done between two local repos too, although it is more common for them to involve a remote repo.

**A repo can work with any number of other repositories as long as they have a shared history** e.g., `repo1` can pull from (or push to) `repo2` and `repo3` if they have a shared history between them.

**A _fork_ is a remote copy of a remote repo**. As you know, cloning creates a local copy of a repo. In contrast, forking creates a remote copy of a Git repo hosted on GitHub. This is particularly useful if you want to play around with a GitHub repo but you don't have write permissions to it; you can simply fork the repo and do whatever you want with the fork as you are the owner of the fork.

**A _pull request_ (PR for short) is a Github mechanism for contributing code to a remote repo,** i.e., "I'm _requesting_ you to _pull_ my proposed changes to your repo". For this to work, the two repos must have a shared history. The most common case is sending PRs from a fork to its 
upstream repo.

![[Pasted image 20230118112604.png]]

## Commands

### Clone (Download)
-  We can clone public remote respository to our local repository

```
git clone [url of remote repository]
```

- We can use `git log` to see previous commits
  
### Pull

- To update the working directory + local repo with the new commits from the remote repo

```
git pull origin
```

- We can achieve the same thing with `git fetch` then `git merge`

>[!What is origin]
> **When you clone a repo, Git automatically adds a _remote_ repo named `origin`** to your repo configuration. As you know, you can pull commits from that repo.

### Add remote repo

A Git repo can work with remote repos other than the one it was cloned from. **To communicate with another remote repo, you can first add it as a _remote_ of your repo**. Here is an example scenario you can follow to learn how to pull from another repo:

1.  Navigate to the folder containing the local repo.
2.  Set the new remote repo as a _remote_ of the local repo. 

```
git remote add {remote_name} {remote_repo_url}
git remote add upstream1 https://github.com/johndoe/foobar.git
```

3. Now you can pull from the new remote.  
    e.g., `git pull upstream1 master`

### Push (Upload)

**You can push an entire local repository** to GitHub, to form an entirely new remote repository. For example, you created a local repo and worked with it for a while but now you want to upload it onto GitHub (as a backup or to share it with others). The steps are:
1. Create an empty remote repo on GitHub
2. Add the Github repo URL as a remote of the local repo. You can give it the name `origin` or any other name
3. Push the repo to the remote.

```
git remote add origin [remote rep url]
git push -u origin master
```

- `origin` is the conventional name of a remote repository
- `master` branch is the main branch of commits
- ? Use the `-u` flag to inform Git that you wish to track the branch.
- The local repository can run parallel with the remote repository

After you have added the remote repo, you can push **any new commits** you have made in your local repo to the remote repo with the `git push` command, without the `-u flag`.

```
git push origin master
```


### Forking and Pull Requests

- **Forking** is copying a file from owner's remote repository to collaborator's remote repository, can be done via GUI on Github.
- **Pull request** is the collaborators asking for permissions to upload their changes to the owner's remote repo.
- Owner can approve the pull request and merges the changes to their repo.

**Steps to create a pull request**
1. Commit your changes to a new branch e.g., `add-intro` branch.
2. Push the `add-intro` branch to your `origin` fork by `git push origin add-intro`
3. Initiate a PR creation on Github and submit the PR.

**Tips**

**Sending PRs using the `master` branch is less common** than sending PRs using separate branches. For example, suppose you wanted to propose two bug fixes that are not related to each other. In that case, it is more appropriate to send two separate PRs so that each fix can be reviewed, refined, and merged independently. 

**You can update the PR along the way too.** Suppose PR reviewers suggested a certain improvement to your proposed code. To update your PR as per the suggestion, you can simply modify the code in your local repo, commit the updated code to the same `master` branch, and push to your fork as you did earlier. The PR will auto-update accordingly.

**If there is a merge conflicts in outgoing PRs,** you have to manually resolve the conflict in your PR branch. The steps are:

1.  Pull the `master` branch from the upstream repo to your local repo.
  
```
git checkout master
git pull upstream master
```
   
2.  In the local repo, and attempt to merge the `master` branch (that you updated in the previous step) onto the PR branch, in order to bring over the new code in the `master` branch to your PR branch.

```
git checkout pr-branch  
git merge master
```

3.  The merge you are attempting will run into a merge conflict, due to the aforementioned conflicting code in the `master` branch. Resolve the conflict manually (this topic is covered elsewhere), and complete the merge.
4.  Push the PR branch to your fork. As the updated code in that branch no longer is conflicting with the `master` branch, the merge conflict alert in the PR will go away automatically.

### Summary

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