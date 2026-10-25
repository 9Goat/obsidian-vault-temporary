it is used to stop compiling an element and render it as if we dont have vue 

# Syntax

```Html
<p v-pre> this message variable will NOT be rendered: {{msg}} </p>
```

# How `v-pre` Works

When Vue compiles a template, it looks for special syntax. When it encounters an element with `v-pre`, it immediately stops processing the contents, treating that section as pure, static HTML.

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
<p v-pre> this message variable will NOT be rendered: {{msg}} </p>
</div>
<script>
    const { createApp } = Vue; 

    const app = createApp({
        data() {
            return {  
                msg : "Hello, Vue!"                   
            };
        }
    });
    const mountedApp = app.mount("#app");
</script>
</body>
</html>
```

