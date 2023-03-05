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