components are used to build sections of a webpage. It contains everything we can have in a main function ,but with few extra features like html template and props. It is used to separate our page into smaller sections where each section has it own functionality and logic


# Syntax

```Js
app.component('component-name',{

template: `<element>text</element>`

,data(){
return{}
}
,methods:{
}

,computed:{
}
})
```

- the only thing different here is that we have a template that contains the html that will be rendered when the component is used

# Calling the component

the great thing about component is that we can call them anywhere in our application, as many times as we want, and they will be rendered with their own isolated scope.

## Syntax

```Html
<div id="app"> 
    <component-name></component-name> 
</div>
```

The name of the html elements **MUST** match the component name in the component registration.
# Example

```Html
<div id="app">
    <h2>My Application</h2>
    <p>Below are instances of my simple component:</p>
    <my-simple-component></my-simple-component>
    <my-simple-component></my-simple-component>
  </div>

  <script>
    // 1. Create a Vue application instance
    const app = Vue.createApp({});

    // 2. Register a global component
    app.component('my-simple-component', {
      template: `
        <div style="border: 1px solid #ccc; padding: 10px; margin-bottom: 10px;">
          <h3>{{ componentTitle }}</h3>
          <p>{{ componentMessage }}</p>
          <button @click="incrementCount">Click me!</button>
          <p>You clicked {{ count }} times.</p>
        </div>
      `,
      data() {
        return {
          componentTitle: 'Hello from a Simple Component!',
          componentMessage: 'This component has its own data and logic.',
          count: 0
        };
      },
      methods: {
        incrementCount() {
          this.count++;
        }
      }
    });

    // 3. Mount the application to the DOM element with id="app"
    app.mount('#app');
  </script>
```

# Notes

- each call of the component will be treated as a difference instance
	- **Example** if we look at the code above ,if we increment one of the counters it wont affect the others
- it is **BEST** practice to place each component inside its own file and have a folder called "*components*" that contains all of the components, and have our pages link those files use script src
- make sure that we close the app using mount **AFTER** we have linked it to our page otherwise it wont render
- its best practice to name our components in a way where we separate multiple words with a minus `-`

## Example 1

```Html
<script src="main.js"></script>
<script src="components/component-name"></script>
<script>
app.mount('#app');
</script>
```