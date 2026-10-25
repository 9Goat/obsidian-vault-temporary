dependency is the only association allowed in the package diagram which means that it depends on an another package to function correctly

# Syntax

to create dependency we draw a dashed line with an arrow pointing from the package that depends on the other package to the depended package

![[image-80.png]]

# Types of dependency

there are 3 main types of dependency which are :

- import
- access
- merge

all of these types are written exactly like [[stereotype]] but above the dependency line instead

## import

the import association means that we are fully calling the entire package which gives us full access to all of its elements at once which means when we call an element like class from the imported package we write its name instead of its path

## access

when we access a package we only access 1 element of it at a time but calling it from other packages by its full path instead of its name (unlike import) we use access when we dont rely heavily on other package but only need them for shorter and smaller access 

## Merge

# Examples

![[image-81.png]]
