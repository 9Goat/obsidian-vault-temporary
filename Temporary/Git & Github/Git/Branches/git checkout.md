git checkout is used to switch a to different branch

#  Syntax

```Bash
git  checkout <branch-name>
```

- the branch name  is required
- if we want to create and also  switch to that branch we could add -b before the name of the branch we are going to create

# Example

```Bash
# Switch to an existing branch named 'develop'
git checkout develop

# Create a new branch named 'feature/login' and switch to it
git checkout -b feature/login

# Switch to the 'main' branch
git checkout master
```