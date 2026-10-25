git fetch is used to update our current local repository with the latest changes from the remote repository. Meaning that we run git fetch after we have cloned the repository using [[git clone]]

# Syntax

```Bash
git fetch <remote-alias> [branch-name]
```

|**Component**|**Description**|**Example**|
|---|---|---|
|**`git fetch`**|The action to download data from the remote.|—|
|**`<remote-alias>`**|The nickname of the remote connection (usually `origin`).|`origin`|
|**`[branch-name]`**|_Optional._ Fetches only the specified branch (defaults to fetching all tracked branches).|`main`|

# Options

we can add --all to add **ALL** remotes to the fetch command. 

# Example

```Bash
git fetch origin
```

