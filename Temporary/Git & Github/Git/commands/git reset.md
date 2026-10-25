The core function of `git reset` is to change commitments we made to our repository BUT have not pushed yet, to change a pushed commitment we use the invert command instead.By using reset you are instructing Git to **discard** all the commits that came _after_ that target commit on your current branch, making the target commit the **new, latest commit** (the tip of the branch).

# Syntax

```Bash
git reset <mode> [<commit>]
```

- the mode is  optional by default it will be --mixed
- the commit can either be by the reference of the commit has or by its relative position using the HEAD pointer.

## Reset via reference

in this method we need to choose a specif commit id to reset to by using the git log command
### Syntax

```Bash
git log --oneline
```

## Reset via header

by using the header pointer,**`HEAD~N`** means "the Nth commit before HEAD."

### Syntax

```Bash
git reset HEAD~2
```

**`HEAD~2`**: The commit two steps before the current HEAD.Undoes the last **2** commits.

# Options

To properly understand `git reset`, you need to know the three trees Git uses to manage your project:

1. **HEAD:** A pointer to the last commit you made (or the tip of the current branch).
2. **Staging Area (or Index):** The area where you prepare your next commit (using `git add`).
3. **Working Directory:** The actual files you see and edit on your file system.

`git reset` operates on these three areas, and the most important part of the command is the **mode** (or flag) you use: `--soft`, `--mixed`, or `--hard`.

Let's say you have three commits: **A** (oldest) → **B** → **C** (HEAD). You want to go back to commit **B**.

| Command               | `HEAD` moves to... | Staging Area...                  | Working Directory...             | Resulting State                                                |
| --------------------- | ------------------ | -------------------------------- | -------------------------------- | -------------------------------------------------------------- |
| `git reset --soft B`  | Commit **B**       | Keeps changes from **C** staged. | Keeps files from **C**.          | Changes from **C** are ready to be re-committed.               |
| `git reset --mixed B` | Commit **B**       | Unstages changes from **C**.     | Keeps files from **C**.          | Changes from **C** are _unstaged_ modifications in your files. |
| `git reset --hard B`  | Commit **B**       | Discards all changes from **C**. | Discards all changes from **C**. | **All work from C is permanently gone.**                       |
