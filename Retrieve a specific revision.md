
Git can load a **specific version** of the history to the working directory. Note that if you have uncommitted changes in the working directory, you need to stash them first to prevent them from being overwritten.

Use the `checkout <commit-identifier>` command to change the working directory to the state it was in at a specific past commit.

-   `git checkout v1.0`: loads the state as at commit tagged `v1.0`
-   `git checkout 0023cdd`: loads the state as at commit with the hash `0023cdd`
-   `git checkout HEAD~2`: loads the state that is 2 commits behind the most recent commit

For a list of commands, see [[Git Basic Commands]]
