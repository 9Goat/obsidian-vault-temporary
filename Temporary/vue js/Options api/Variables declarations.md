inside the return method we enter our selection of variables to declare and use inside of our app

# Syntax

```Js
data() {
    return {
    variable1 : value1,
    variable2 : value2,
    ,,,
    variable3 : value3                           
};
}
```

- to declare variables we must specify their initial value be separating them with a collon `:` 
- between each variable declaration we must separate them with a comma `,`

# Displaying variables in HTML

to display those variables we use the double curly braces syntax `{{ }}` in our HTML template.

## Syntax

```Html
<element> {{ variableName }} </element>
```

# Example

```Html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
</head>
<body>
    <div id="app">
        <p>{{variable}}</p>
    </div>
    <script>
        const {createApp}= Vue;
        const app = createApp({
            data(){
                return{
                    variable:"Hello this is my first message in vue"
                };
            }
        })
        const mountedApp = app.mount("#app"); 
    </script>
</body>
</html>
```

## Notes

- double curly brackets are used to display the value of a variable **AND** to execute any valid javascript expression/statement.
	- **Examples**
		- `<p>The total is **{{ price * quantity }}** dollars.</p>`
		- `<p>Status: **{{ isOnline ? 'Online' : 'Offline' }}**</p>`
		- `<p>Formatted Date: **{{ formatDate(timestamp) }}**</p>`