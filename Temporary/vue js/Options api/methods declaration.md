to declare variables we need to pass an another argument to the app instance, called `methods`

# Syntax

```Js
const app = createApp({
        data() {
            return {
	             //variables declaration here
            };
        }, //comma here is very important dont forget it
        methods:{
        
        metodName(parameters){
        //statements of the method here
        }
        
        }
    });
```

# Example

```Html
<div id="app">
  <p>{{ message }}</p>
  
  <button @click="reverseMessage">Reverse Message</button>
</div>

<script>
  const { createApp } = Vue; 

  app = createApp({
    data() {
      return {  
        message: 'Hello Vue!'
      };
    },
    methods: {
      reverseMessage() {
        this.message = this.message.split('').reverse().join('');
      }
    }
  }).
  
  mountedApp = app.mount('#app');
</script>
```

