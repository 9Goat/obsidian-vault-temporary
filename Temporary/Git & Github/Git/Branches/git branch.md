git branch is command can be used for one of the following purposes:

- listing all the local branches in the repository, 
- creating a new branch, 
- deleting an existing branch,
- rename an old branch

# Syntax

```Bash
git branch <options>
```

- the options are optional

# Options

| **Command**                                                                  | **Action** | **Description**                                                                                         |
| ---------------------------------------------------------------------------- | ---------- | ------------------------------------------------------------------------------------------------------- |
| `git branch`                                                                 | **List**   | Lists all local branches. The current branch is marked with an asterisk (`*`).                          |
| `git branch <name>`                                                          | **Create** | Creates a new branch named `<name>` pointing to the current commit (HEAD), but _does not_ switch to it. |
| `git branch -m <old> <new>` or use -M to  force it (even if the name exists) | **Rename** | Renames the local branch `<old>` to `<new>`.                                                            |
| `git branch -d <name>` or use -D to force it                                 | **Delete** | Deletes the specified branch, but only if it has been fully merged into its upstream branch.            |

## listing branches

These options change what information the command displays when listing branches.

| Option                       | Purpose             | Example                                                                                                                                      |
| ---------------------------- | ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| **`-a`** or **`--all`**      | **Show All**        | Lists all local and **remote-tracking** branches (`origin/main`, etc.).                                                                      |
| **`-r`** or **`--remotes`**  | **Show Remotes**    | Lists only remote-tracking branches.                                                                                                         |
| **`-v`** or **`--verbose`**  | **Verbose**         | Shows the **SHA-1** and the **subject line** of the latest commit on each branch.                                                            |
| **`-vv`**                    | **Very Verbose**    | Shows the SHA-1, subject line, **and** the **upstream** branch relationship (e.g., `[origin/main: ahead 2]`).                                |
| **`--merged [<commit>]`**    | **Filter Merged**   | Lists only the branches that have been **fully merged** into the specified commit (defaults to `HEAD`). Useful before deleting old branches. |
| **`--no-merged [<commit>]`** | **Filter Unmerged** | Lists only the branches that contain **unmerged changes**. Git prevents deleting these with `-d`.                                            |
| **`--contains [<commit>]`**  | **Filter Contains** | Lists only branches whose history includes the specified commit.                                                                             |

# Example 


```Bash
# List all local branches
git branch

# Create a new branch named 'feature/new-feature'
git branch feature/new-feature

# List all local and remote branches
git branch -a

# Delete a branch named 'feature/old-feature' (only if merged)
git branch -d feature/old-feature
```

