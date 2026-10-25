v-if statements are very similar to [[v-show]] but with few changes. in this note not only will we talk about `v-if` but we will also mention `v-else` and `v-else-if` directives, which are closely related to `v-if` and are used together to create conditional rendering blocks in Vue.js

# Syntax

```Html
<element v-if="condition/express/varaible"></element>
<element v-else-if="condition/express/varaible"></element>
,,,, more v-else-if (optional)
<element v-else> </element>
```

# How it works

- it works just like a regular if statements in any programming language.
- it is very similar to [[v-show]] except that if the express/condition/value is false the element will be visible and will be hidden within the `DOM`

# Example

```Html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Vue App</title>
    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
    <style>
        .box {
            width: 200px;
            height: 200px;
            background-color: blue;
        }
        .two {
            background-color: green;
        }
        .three {
            background-color: coral;
        }
    </style>
</head>
<body>

<div id="app">
<div v-if="firstVariable" class="box">hello</div>
<div v-else-if="secondVariable" class="box two"></div>
<div v-else class="box three"></div>
</div>
<script>
    const { createApp } = Vue; 

    const app = createApp({
        data() {
            return {  
                firstVariable: false,
                secondVariable: false
            };
        }
    });
    const mountedApp = app.mount("#app");
</script>
</body>
</html>
```

