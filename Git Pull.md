>[!analogy]
>Update/sync your local files with the remote files


```
git pull origin
```
- Update the working directory + local repo with the new commits from the remote repo
- We can achieve the same thing with `git fetch` then `git merge`

>[!What is origin]
> **When you clone a repo, Git automatically adds a _remote_ repo named `origin`** to your repo configuration. As you know, you can pull commits from that repo.