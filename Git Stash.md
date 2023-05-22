## How to use git stash

Here's the sequence to follow when using git stash:

1.  Save changes to branch A.
2.  Run `git stash`.
3.  Check out branch B.
4.  Fix the bug in branch B.
5.  Commit and (optionally) push to remote.
6.  Check out branch A
7.  Run `git stash pop` to get your stashed changes back.

Git stash stores the changes you made to the working directory locally (inside your project's .git directory; `/.git/refs/stash`, to be precise) and allows you to retrieve the changes when you need them. It's handy when you need to switch between branches without commiting a checkpoint. It allows you to save changes that you might need at a later stage and is the fastest way to get your working directory clean while keeping changes intact.