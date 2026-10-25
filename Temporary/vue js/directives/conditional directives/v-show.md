the v-show attribute is used to either show or hide an element based on a condition. Unlike v-if, v-show always renders the element, but changes its CSS display property to `none` meaning  its still visible to the `DOM` but cannot be seen when rendering if set to `false` the page

# Syntax

```Html
<element v-show="condition/expression/variable">This content visib lity is controlled by the v-show</element>
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
<p>this text is above the v-show element</p>
<p v-show="isTrue">this text is shown when isTrue is true</p>
<p>this text is below the v-show element</p>
</div>
<script>
    const { createApp } = Vue; 

    const app = createApp({
        data() {
            return {  
                isTrue: false
            };
        }
    });
    const mountedApp = app.mount("#app");
</script>
</body>
</html>
```

