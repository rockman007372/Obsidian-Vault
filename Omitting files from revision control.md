## Omitting files from revision control

Often, there are files inside the Git working folder that you don't want to revision-control. These include:
-   **Binary files** _generated_ when building your project e.g., `*.class`, `*.jar`, `*.exe` (reasons: 1. no need to version control these files as they can be generated again from the source code 2. Revision control systems are optimized for tracking text-based files, not binary files.)
-   **Temporary files** e.g., log files generated while testing the product
-   **Local files** i.e., files specific to your own computer e.g., local settings of your IDE
-   **Sensitive content** i.e., files containing sensitive/personal information e.g., credential files, personal identification data (especially, if there is a possibility of those files getting leaked via the revision control system).

**Steps to obmit files:**
- Make a .gitignore

```
vim .gitignore
```

- Type in the name of the files to be ignored

You can commit the .gitignore file just like any other files.

You can ignore file patterns instead of single files: 
- add `temp/*.tmp` to the `.gitignore` file to prevents Git from tracking any `.tmp` files in the `temp` directory.