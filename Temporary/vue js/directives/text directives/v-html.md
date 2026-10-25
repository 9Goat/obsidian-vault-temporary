is exactly the same as [[v-text]] except that it also supports html elements as text

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
<p v-html="'<h1>hello</h1>'"></p>
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

