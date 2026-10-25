git remote is used to manage the connection between our terminal and our github repository. The remote connection is permanent on a folder until we either push the changes or we remove the remote

#  Displaying connections

|**Option**|**Purpose**|**Output Details**|**Example**|
|---|---|---|---|
|**`git remote`**|**List Aliases**|Displays a simple list of the short names (aliases), like `origin` or `upstream`, for your configured remotes.|`origin`<br><br>  <br><br>`upstream`|
|**`git remote -v`**|**Verbose List** (Most Common)|Displays the remote aliases along with their full, associated **URLs** for both **fetching** (pulling) and **pushing**.|`origin https://github.com/user/repo.git (fetch)`<br><br>  <br><br>`origin https://github.com/user/repo.git (push)`|
|**`git remote show <name>`**|**Show Details**|Displays detailed information about a **specific remote** (e.g., `origin`), including its URL, the local branches that track it, and the default branch it pushes to.|Shows a block of text detailing the remote's URL, branches, and configured pull/push status.|

# adding connections

## Syntax

```Bash
git remote add <alias-name> <remote-url>
```

|**Component**|**Description**|**Example Value**|
|---|---|---|
|**`git remote add`**|The command to create and define a new remote connection.|—|
|**`<alias-name>`**|The **nickname** you give to this remote. This is almost always set to `origin` for your primary remote.|`origin`|
|**`<remote-url>`**|The unique address (URL) used to access the remote repository. This is provided by the hosting service (e.g., GitHub).|`https://github.com/user/project.git`|

## Note 

to get the remote-url from github simply go to repository you want to connect to and click on this button

![[image-48.png]]

# renaming a remote

## Syntax

```Bash
git remote rename <old-name> <new-name>
```

|**Component**|**Description**|
|---|---|
|**`git remote rename`**|The command to change a remote's alias.|
|**`<old-name>`**|The existing nickname of the remote (e.g., `origin`).|
|**`<new-name>`**|The new nickname you want to use for that remote.|

# Changing url of a remote

## Syntax

```Bash
git remote set-url <name> <new-url>
```


| **Component**            | **Description**                                           |
| ------------------------ | --------------------------------------------------------- |
| **`git remote set-url`** | The command to update a remote's stored URL.              |
| **`<name>`**             | The existing nickname of the remote (e.g., `origin`).     |
| **`<new-url>`**          | The complete new URL that Git should use for that remote. |

# removing a remote

```Bash
git remote rm <alias-name>
```
# Example

```Bash
# List all configured remotes
git remote

# List all configured remotes with their URLs (verbose)
git remote -v

# Add a new remote named 'origin' with its URL
git remote add origin https://github.com/your-username/your-repo.git

# Rename the remote 'origin' to 'upstream'
git remote rename origin upstream

# Change the URL for the remote 'origin'
git remote set-url origin https://github.com/new-username/new-repo.git

# Show detailed information about the 'origin' remote
git remote show origin
```

