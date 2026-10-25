this directive is used to render the component/element **ONLY ONCE** which makes it immune to all possible updates. Its useful when we want render something that we want to never change

# Syntax

```Html
<span v-once>This will never change: {{msg}}</span>
```

in this syntax the `span` element will show case the initial value of `msg` and will not update even if the `msg` data property changes.

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
<p v-once>This will never change: {{msg}}</p>
<button @click="changeValue">Click here to change value</button>
</div>
<script>
    const { createApp } = Vue; 

    const app = createApp({
        data() {
            return {  
                msg : "Hello, Vue!"                   
            };
        },
        methods: {
          changeValue() {
              this.msg = "This will not be displayed because v-once is used.";
          }
        }
    });
    const mountedApp = app.mount("#app");
</script>
</body>
</html>
```

