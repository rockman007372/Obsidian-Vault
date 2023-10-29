
**Each Git commit is uniquely identified by a hash** e.g., `d670460b4b4aece5915caf5c68d12f560a9fe3e4`. As you can imagine, using such an identifier is not very convenient for our day-to-day use. As a solution, Git allows adding a more human-readable _tag_ to a commit e.g., `v1.0-beta`.

To add a tag to the current commit as `v1.0`,

```bash
git tag –a v1.0
```

To view tags

```bash
git tag
```