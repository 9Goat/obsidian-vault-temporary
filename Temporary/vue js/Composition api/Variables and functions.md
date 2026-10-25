# Declaring variables

to declare variables and functions we need to specify it inside the return function to make the vue app recognise it as a reaction variable and create a **`ref`** for it and assign it a value

## Syntax

```Js
setup(){
const variableName = ref(initialValue); //const is optional but recommended
function functionName(paramters){
//statements
}
return { 
 variableName,
 functionName
}
}
```

- **`ref`** is used to initialise variables and tell vue that this variables in a reactive variable and not a regular variable (`initialValue` will be the value assigned to the variable)
	- To change the value of a reactive variable created using `ref`, we need to access its `.value` property. For example, if we have a variable `variableName` declared as `const variableName = ref(initialValue);`, we can change its value by doing `variableName.value = newValue;`. 
- inside the **`return`** we declare all functions and variables ,they **MUST** be separated by commas between each declaration


