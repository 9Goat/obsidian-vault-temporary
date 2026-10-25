v-model is a directive in Vue.js that is used for two-way data binding on form elements.
# How it works

## for text input and textarea elements

it takes the value of the input (the text content entered by the user) and applies it value to the variable specified in the v-model directive.the variable value updates everytime the user types or deletes text in the input field,

### Syntax

```HTML
<input type="text" v-model="variableName" />

<textarea v-model="variableName">   </textarea>
```

## for checkboxes and radio buttons

same as above but instead of taking the value of the input, v-model takes the checked state of the input (whether it is checked or not meaning **`true`** or **`false`**), the variable value updated everytime the user checks or unchecks the checkbox or radio button.

### Syntax

```Html
<input type="checkbox" v-model="checkedName"> //checkedName will eithe be true or false

<input type="radio" v-model="checkedName">
```

## for select elements

very similar to the text input and textarea elements, except that it will take the value of the selected option. The variable value updates every time the user selects a different option from the dropdown list.

### Syntax

```HTML
<select v-model="selectedName">
<option value="option1">Option 1</option>
,,,,,more options
</select>
```

# Example

```Html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Vue App</title>
    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
</head>
<body>

<div id="app">
<input type="text" name="" v-model="variable" id="">
<p>{{variable}}</p>
<input type="checkbox" v-model="checkedName">ilyes
<p>{{checkedName}}</p>
</div>
<script>
    const { createApp } = Vue; 

    const app = createApp({
        data() {
            return {  
                variable:"default",
                checkedName:""                     
            };
        }
    });
    const mountedApp = app.mount("#app");
</script>
</body>
</html>
```

# Notes

- v-model can also be used to set value for form elements since its *two-way data binding* nature
- if the select element allows multiple selections, v-model will bind the selected values to an array. not a single value
- for textarea the v-model will also takes the `\n` and adds it the variable value 
