ssh keys are used to connect github accounts to our local machines

# generating new SSH keys

##  Syntax

```Bash
ssh-keygen -t ed25519 -C "Message"
```

- we can add a message to our SSH key using the `-C` ,mostly our message will be the following
	- `github-account -email` for example `Elyes-Belk elyesbelkahia22@gmail.com`

afterwards it will prompt you to enter a file in which to save the key.

![[image-82.png]]

in our case we will just copy the path and rename the file to our github account name

# adding the SSH key

after creating the account we then add the SSH key to github by first naviagating to the path of the public key and copy the content of the file that ends with .pub

![[image-83.png]]

afterwards we go to github->click on our profile->settings->ssh keys->add new ssh keys
and then we paste it

![[image-85.png]]

# managing the config file

this is only a problem if we are working with multiple github accounts to solve that we create a new account inside the .ssh folder name config and we add a new confing element to it in this syntax

## Syntax

```Bash
# custom message for your confing element
Host github.com-newuser # <--- YOUR CUSTOM ALIAS
  HostName github.com      # <--- The REAL host
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/id_newuser # <--- The path to your NEW PRIVATE key
```

## Example

![[image-84.png]]


# Using the SSH keys

when we copy the **SSH** link from github code of someone else repository to clone from we **MUST** replace the  default alias we the alias we have set up using the config file

![[image-88.png]]
![[image-86.png]]

# Testing

to test if it worked we run this command

![[image-87.png]]

