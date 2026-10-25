v-on is used to apply event listeners to elements. and execute JavaScript functions or statements when certain events occur, such as a click or mouseover.

# Syntax

```Html
//Standard syntax
<element v-on:eventName="functionNameOrExpression"></element>

//Shorthand Syntax
<element @eventName="functionNameOrExpression"></element>
```

- in the shorthand syntax we simply replace the **`v-on:`** with the **`@`** symbol.
- when the event occurs *like a mouse click for example* it will execute the
	- **expression:** if it is a single line statement like `count++` or `alert('Hello')`, it will be executed directly. 
	- **functionName:** if it's a function name like `handleClick`, the corresponding method defined in the Vue instance's `methods` object will be called.

# Example

```Html
<div id="app">
<p>{{ counter1 }}</p>
<button v-on:click="counter1++">click here to update the counter using direct statement</button>
<p>{{ counter2 }}</p>
<button v-on:click="incrementCounter">click here to update the counter using method</button>
</div>
<script>
    const { createApp } = Vue; 

    const app = createApp({
        data() {
            return {  
                counter1: 0,
                counter2: 0,
            };
        },
        methods:{
            incrementCounter(){
                this.counter2++;
            }
        }
    });
    const mountedApp = app.mount("#app");
</script>
```

