The `git commit` command captures the contents of the **staging area** (the files you added with `git add .`) and creates a new, immutable commit object. This commit object contains:

- A pointer to the snapshot of the project you staged.
- Metadata, including the author, date, and, most importantly, the **commit message**.
- A pointer back to the commit(s) that came immediately before it (its parent), which builds the project's history.

# Syntax

```bash
git commit
```

# Options

| **Parameter/Flag**        | **Purpose**                                                                                                                                                                                                                                                                                | **Example**                                      |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------ |
| **`-m "<message>"`**      | **Message:** Allows you to provide the commit message directly on the command line, skipping the text editor.                                                                                                                                                                              | `git commit -m "Fix login button styling"`       |
| **`-a`** (or `--all`)     | **Automatic Staging:** Automatically stages all **modified** and **deleted** tracked files before committing. **Caution:** It _does not_ include new, untracked files (you still need `git add` for those).                                                                                | `git commit -a -m "Fixing tracked files"`        |
| **`-am "<message>"`**     | **Shortcut:** Combines the `-a` and `-m` flags for a quick commit of all modified/deleted files.                                                                                                                                                                                           | `git commit -am "Combined stage and commit"`     |
| **`-v`** (or `--verbose`) | **Verbose:** Shows a detailed inline diff of the changes being committed right within the commit message editor, providing context while you write your commit message.                                                                                                                    | `git commit -v`                                  |

## Fixing mistakes

to fix a mistake inside a commitment we use git commit --amend

### Example

![[image-45.png]]
# Example

![[image-44.png]]