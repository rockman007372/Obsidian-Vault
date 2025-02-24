https://www.warp.dev/terminus/understanding-git-push-origin
#### General format

```
$ git push [remote repository] [flags] [local branch name]
```

#### Basic workflow

**You can push an entire local repository** to GitHub, to form an entirely new remote repository. For example, you created a local repo and worked with it for a while but now you want to upload it onto GitHub (as a backup or to share it with others). The steps are:

1. Create an empty remote repo on GitHub
2. Add the Github repo URL as a remote of the local repo. You can give it the name `origin` or any other name
```
$ git remote add origin [remote rep url]
```
3. Push the repo to the remote.
```
$ git push origin -u master
```

- `origin` is the conventional name of a remote repository
- `master` is the branch name shared by both local and remote repos.
- ? Use the `-u` flag to inform Git that you wish to track the branch.
- The local repository can run parallel with the remote repository

After you have added the remote repo, you can push **any new commits** you have made in your local repo to the remote repo with the `git push` command, without the `-u flag`.

```
git push origin master
```

#### Pushing to a different branch

`git push origin` will push the current branch to the **branch of the matching name in the remote repository** (aka, “branch configured upstream”), if it exists, otherwise, it will not push and notify that the current branch has no remote counterpart.

The default branch in your project is conventionally a branch named **“main”**. This branch is the version of the project that goes into production or the version from which you will create further branches to isolate changes, and merge back into the default branch.

If a project you are working on is older, the default branch might be named “master”, [which GitHub changed to remove references to slavery in conventional terminology.](https://www.zdnet.com/article/github-to-replace-master-with-alternative-term-to-avoid-slavery-references/)