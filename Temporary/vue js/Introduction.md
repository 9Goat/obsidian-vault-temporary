vue is a front end framework for js what is great for creating online web application. there are 2 ways to write code in vue either by using:

- **Options API**: for creating simpler and easier projects
- **Components API** : for creating larger scale projects and maintain reusable code 

# How to import it

to import it we can  use the  CDN link directly in our HTML file

## Syntax

```HTML
<html>
<head>
....
</head>
<body>
... // Html code here
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
... // java and vue code go here
</script>
```

# How to create a vue application

## HTML setup

to create a vue application you need to create an **`app`** div inside of html

#### Syntax

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Learning Vue.js</title>
    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
</head>
<body>

    <div id="app">
        </div>

    <script>
        // We'll write our Vue code here in the next step
    </script>

</body>
</html>
```

## JS setup using component API

### Syntax

```Js
  const { createApp, ref } = Vue

  const app = createApp({
    setup() {
      return {
      }
    }
  })
  
 const mountedApp = app.mount("#app");
```

 1. **`const { createApp, ref } = Vue`** : Used to extract the functions `createApp` and `ref` from the Vue object (this is used to simplify the process of calling those functions instead of writing `Vue.ref` when we want to use the ref function)
 2. **`const app = createApp({...})`** : This line is used to create a vue app instance and store it inside a constant 
 3. **`setup(){...}`**: used to as a container for variables instialization and creating methods
 4. **`return{...}`** is used as a way to store variable declarations for the vue app to recognize
 5. **` const mountedApp = app.mount("#app");`** : This line is used to tell the vue where the app is to take control and render it (it **MUST** be the absolute last line of all the vue code we have on the page)

### Example

```HTML
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
    <h1>{{ message }}</h1>
    <p>You have clicked the button {{ count }} times.</p>
    <button @click="incrementCount">Click Me!</button>
</div>
<script>
    const { createApp, ref } = Vue;

    const app = createApp({
        setup() {
            const count = ref(0);
            const message = ref('Hello Vue!');

            function incrementCount() {
                count.value++;
            }

            return {
                message,
                count,
                incrementCount
            };
        }
    });

    const mountedApp = app.mount("#app");
</script>
</body>
</html>
```

## JS setup using Options API 

similar to the components api but with few changes to it
### Syntax

```Js
const { createApp } = Vue; 

    const app = createApp({
        data() {
            return {                       
            };
        },
        methods: {
        }
    });

    const mountedApp = app.mount("#app");
```

- **`const {createApp} = Vue;`** we dont use the ref function inside the options api that is why we only extract the createApp function
- **`data(){...}`** function that vue js used to return an object full of variables *return*
- **`methods:{...}`** used to contain methods and functions

### Example

```HTML
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
    <h1>{{ message }}</h1>
    <p>You have clicked the button {{ count }} times.</p>
    <button @click="incrementCount">Click Me!</button>
</div>
<script>
    const { createApp } = Vue; 

    const app = createApp({
        data() {
            return {
                message: "Hello Vue 3 (Options API)",
                count: 0,                           
            };
        },
        methods: {
            incrementCount() {
                this.count++;
            }
        }
    });
    const mountedApp = app.mount("#app");
</script>
</body>
</html>
```

