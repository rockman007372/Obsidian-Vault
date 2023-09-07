A Git repo can work with remote repos other than the one it was cloned from. **To communicate with another remote repo, you can first add it as a _remote_ of your repo**. Here is an example scenario you can follow to learn how to pull from another repo:

1.  Navigate to the folder containing the local repo.
2.  Set the new remote repo as a _remote_ of the local repo. 

```
git remote add {remote_name} {remote_repo_url}
git remote add upstream1 https://github.com/johndoe/foobar.git
```

3. Now you can pull from the new remote.  
    e.g., `git pull upstream1 master`