The core function of `git push` is to move the local Git history (your commits) to a specified remote alias, updating the remote's branch pointers.

# Syntax

```Bash
git push <remote-alias> <branch-name>
```

| **Component**        | **Description**                                           | **Example**               |
| -------------------- | --------------------------------------------------------- | ------------------------- |
| **`git push`**       | The action to send changes.                               | —                         |
| **`<remote-alias>`** | The nickname of the remote connection (usually `origin`). | `origin`                  |
| **`<branch-name>`**  | The specific local branch you want to push.               | `main` or `feature/login` |
# Example

```Bash
# Push the current local 'main' branch to the 'origin' remote
git push origin main

# Push a new local branch named 'feature/new-feature' to 'origin'
# The -u (or --set-upstream) flag sets the upstream tracking branch,
# so subsequent pushes from this branch can just be 'git push'
git push -u origin feature/new-feature

# After setting upstream, simply push changes from the current branch
git push
```