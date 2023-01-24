## Repositories

>[!definition]
> **Repository** (_repo_ for short): The database of the history of a directory being tracked by an RCS software (e.g. Git).

**The _repository_ is the database where the meta-data about the revision history are stored.** Suppose you want to apply revision control on files in a directory called `ProjectFoo`. In that case, you need to set up a _repo_ (short for repository) in the `ProjectFoo` directory, which is referred to as the _working directory_ of the repo. For example, Git uses a hidden folder named `.git` inside the working directory.

**You can have multiple repos in your computer**, each repo revision-controlling files of a different working directory, for examples, files of different projects.

## Create new Git local repository 

 ```
git init
```
