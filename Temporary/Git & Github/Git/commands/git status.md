The `git status` command displays the state of your working directory and the staging area (also called the index). It tells you exactly where you stand before you make a commit.

### What `git status` tells you:

1. **Which branch you are on** (e.g., `On branch main`).
2. **The relationship with the remote branch** (e.g., `Your branch is ahead of 'origin/main' by 1 commit`).
3. **The state of your files**, which are categorized into three main sections:

| Status Section                    | File State      | Action Needed                                                                                                                   |
| --------------------------------- | --------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| **Changes to be committed**       | **Staged**      | These files are ready to be included in the **next `git commit`**.                                                              |
| **Changes not staged for commit** | **Modified**    | These are files Git is **tracking** but have changes that haven't been added to the staging area with `git add`.                |
| **Untracked files**               | **New/Unknown** | These are brand new files that Git is **not currently tracking**. You need to use `git add` to tell Git to start watching them. |

# options

the status command offers several useful options that help you determine the output  of your git status

## short

by adding **`-s`** at the end of the command we can get a shorter version of the status output, Which will show :

- a symbol of the type of change made to a file
- the path of that file 

| **Code** | **Meaning**                                        |
| -------- | -------------------------------------------------- |
| `??`     | **Untracked** file                                 |
| `M`      | File is **modified** in the working directory      |
| `A`      | File is **newly added** and staged                 |

### Example

![[image-41.png]]

## verbose

by adding -v or --verbose at the end of the command, we can get a more detailed version of the status output, which will show the changes made to the files in addition to the status information.

## branch

by adding **`-b`** at the end of the command we can showcase the current branch we are working on

### Example 

![[image-42.png]]

### Note

- when we use the status command by default it shows us the current branch we are working on meaning it is only useful when working with the short version of **`-s`** 

# Example

![[image-40.png]]