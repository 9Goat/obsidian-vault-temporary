v-text is a directive in Vue.js that is used to update an element's textContent. it takes **`String`** as input and sets the text content of the element to the given string.

# Syntax

```Html
<element v-text="string value/variable"> old text that will be erased</element>

//same as this

<element>{{string variable}}</element>
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
<p v-text="'hello'"></p>
</div>
<script>
    const { createApp } = Vue; 

    const app = createApp({
        data() {
            return {                     
            };
        }
    });
    const mountedApp = app.mount("#app");
</script>
</body>
</html>
```

# Notes

-  The v-text directive takes a string as input meaning it can either be a variable or an expression what will result in a string inside of double quotes **`"`** or it can be a string literal inside double quotes and single quotes **'** .
	- **Example**: for variable -> `v-text="varaible"` | for string literal -> `v-text="'some text'"`
- The v-text directive will **OVERRIDE** the default textContent within an element