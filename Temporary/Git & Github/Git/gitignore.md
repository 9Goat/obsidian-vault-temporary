the  .gitignore file is used to tell git which files to ignore. "Ignoring" a file or folder using a `.gitignore` file means that Git will **not track** that item, and it will intentionally **exclude** it from version control.

When Git ignores something:

1. **It doesn't monitor it:** Git will not monitor the file for changes. You can create, modify, or delete the ignored file, and Git will not list it as a modified or untracked file when you run `git status`.
2. **It isn't included in commits:** Since Git is not tracking the file, it **cannot be included in any commit**. When you run `git add .` or `git commit -a`, Git simply skips over the ignored files.

# How to Use .gitignore

## Creating a .gitignore File

To start ignoring files in a Git repository, you need to create a `.gitignore` file. This file is typically placed in the root directory of your project.

### Syntax

```Bash
touch .gitignore
```

## writing on a `.gitignore`

### Syntax

```Bash
nano .gitignore
```

there are different patterns we can use to tell gitignore what exactly to look for

| **Syntax**        | **Example**       | **Description**                                                                                                                                |
| ----------------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| **File Name**     | `config.local.js` | Ignores this specific file anywhere in the repository.                                                                                         |
| **Directory**     | `node_modules/`   | Ignores the entire `node_modules` directory and everything inside it. The trailing slash (`/`) indicates a directory.                          |
| **Wildcard**      | `*.log`           | Ignores any file ending with the `.log` extension (e.g., `error.log`, `app.log`).                                                              |
| **Specific Path** | `build/temp/`     | Ignores only the `temp` folder located inside the `build` directory.                                                                           |
| **Negation**      | `!README.md`      | Tells Git **not** to ignore a specific file, even if it matches a previous ignore pattern (e.g., ignoring `*.md` but un-ignoring `README.md`). |

