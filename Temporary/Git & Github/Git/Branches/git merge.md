The `git merge` command is used to join two or more development histories together. When you merge, Git takes the changes from the specified branch and applies them to the branch you are currently on.

# Syntax

```Bash
//lets say we are currently on the master branch

git merge <branch-name> -m "messsage"
```

- this will result in a new merge commit that combines the histories of the two branches. the result branch will be placed on our current working branch which is master for this syntax
- we could also **OPTIONALLY** pass a message for our merge commit using the -m flag

# Example

```Bash
# Assume you are on the 'main' branch
# Merge changes from 'feature/new-feature' into 'main'
git merge feature/new-feature

# Assume you are on the 'develop' branch
# Merge changes from 'hotfix/bug-fix' into 'develop'
git merge hotfix/bug-fix
```