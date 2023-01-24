## Using History

**RCS tools store the history of the working directory as a series of commits.** This means you should commit after each change that you want the RCS to 'remember'.

Each commit in a repo is a recorded point in the history of the project that is **uniquely identified by an auto-generated hash** e.g. `a16043703f28e5b3dab95915f5c5e5bf4fdc5fc1`.

You can **tag a specific commit** with a more easily identifiable name e.g. `v1.0.2`.

To **see what changed between two points** of the history, you can ask the RCS tool to `diff` the two commits in concern.

**To restore the state of the working directory at a point in the past, you can _checkout_ the commit in concern.** i.e., you can traverse the history of the working directory simply by checking out the commits you are interested in.

### Naming commits

**Each Git commit is uniquely identified by a hash** e.g., `d670460b4b4aece5915caf5c68d12f560a9fe3e4`. As you can imagine, using such an identifier is not very convenient for our day-to-day use. As a solution, Git allows adding a more human-readable _tag_ to a commit e.g., `v1.0-beta`.

To add a tag to the current commit as `v1.0`,

```
git tag –a v1.0
```

To view tags

```
git tag
```

### Comparing revisions

**Git can show you what changed in each commit**

```
git show < part-of-commit-hash >
```

eg: `git show v1.0`

**Git can show you the difference between 2 points in history of the repo**

The `diff` command can be used to view the differences between two points of the history.

-   `git diff`: shows the changes (uncommitted) since the last commit.
-   `git diff 0023cdd..fcd6199`: shows the changes between the points indicated by commit hashes. Note that when using a commit hash in a Git command, you can use only the first few characters (e.g., first 7-10 chars) as that's usually enough for Git to locate the commit.
-   `git diff v1.0..HEAD`: shows changes that happened from the commit tagged as `v1.0` to the most recent commit.

[More](https://www.git-tower.com/learn/git/ebook/en/command-line/advanced-topics/diffs) on how to use `git diff`.

### Retrieve a specific revision

Git can load a **specific version** of the history to the working directory. Note that if you have uncommitted changes in the working directory, you need to stash them first to prevent them from being overwritten.

Use the `checkout <commit-identifier>` command to change the working directory to the state it was in at a specific past commit.

-   `git checkout v1.0`: loads the state as at commit tagged `v1.0`
-   `git checkout 0023cdd`: loads the state as at commit with the hash `0023cdd`
-   `git checkout HEAD~2`: loads the state that is 2 commits behind the most recent commit

For a list of commands, see [[Git Basic Commands]]

---
Links: