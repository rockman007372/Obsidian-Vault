## Comparing revisions

**Git can show you what changed in each commit**

```bash
git show < part-of-commit-hash >
```

eg: `git show v1.0`

**Git can show you the difference between 2 points in history of the repo**

The `diff` command can be used to view the differences between two points of the history.

-   `git diff`: shows the changes (uncommitted) since the last commit.
-   `git diff 0023cdd..fcd6199`: shows the changes between the points indicated by commit hashes. Note that when using a commit hash in a Git command, you can use only the first few characters (e.g., first 7-10 chars) as that's usually enough for Git to locate the commit.
-   `git diff v1.0..HEAD`: shows changes that happened from the commit tagged as `v1.0` to the most recent commit.

[More](https://www.git-tower.com/learn/git/ebook/en/command-line/advanced-topics/diffs) on how to use `git diff`.