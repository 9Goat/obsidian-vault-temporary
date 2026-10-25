The primary purpose of `git add` is to move changes from your **Working Directory** to the **Staging Area** (or index).

- **Working Directory:** Where you currently edit and save files.
- **Staging Area:** A buffer or waiting area where you prepare a snapshot of your project's current state. Only changes in this area will be included in the next commit.

In simple terms, `git add` tells Git: "**I want to include this file's current version in the next commit.**"


# different options

| **Command**                                | **Description**                                                                                                                | **What is Staged?**                                                                                                         |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------- |
| **`git add <file-name>`**                  | Stages the specified single file.                                                                                              | Only the changes in that specific file.                                                                                     |
| **`git add <dir-name>`**                   | Stages all changes within a specific directory.                                                                                | All changes (new, modified, deleted) within that directory.                                                                 |
| **`git add .`**                            | **(Most common)** Stages all new and modified files in the **current directory and all subdirectories**.                       | **New** and **Modified** files in the current scope. _Does not stage file deletions reliably across all versions/contexts._ |
| **`git add -A`** or **`git add --all`**    | Stages all changes in the **entire repository** from the project root, regardless of where you run the command.                | **New**, **Modified**, AND **Deleted** files.                                                                               |
| **`git add -u`** or **`git add --update`** | Stages changes to **tracked files only**.                                                                                      | **Modified** and **Deleted** files. It **ignores new/untracked files**.                                                     |
| **`git add -p`** or **`git add --patch`**  | Launches an **interactive session** to let you select which _hunks_ (small blocks) of changes you want to stage within a file. | Only the specific lines you select within a file.                                                                           |

# Example

![[image-43.png]]

- to check  if the command add has worked used the command [[git status]] -sb and see if the status of all the files are A which means added

