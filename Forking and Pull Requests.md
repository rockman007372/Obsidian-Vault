### Forking and Pull Requests

- **Forking** is copying a file from owner's remote repository to collaborator's remote repository, can be done via GUI on Github.
- **Pull request** is the collaborators asking for permissions to upload their changes to the owner's remote repo.
- Owner can approve the pull request and merges the changes to their repo.
- ! It is possible to create pull request within the same repo (eg. between a branch and the master branch of the same repo).

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