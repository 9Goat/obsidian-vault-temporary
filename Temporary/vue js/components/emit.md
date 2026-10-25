very similar to [[props]] except that it goes from the child component to the parent instead of the opposite, it is used to call a function from the child component that is defined in the parent component. 

**The Two-Step Process**

1. **The Child Emits:** The child component calls an emit function (like `$emit` or an alias) to announce an action, such as a button click or a user input change.
2. **The Parent Listens:** The parent component listens for this custom event using the `v-on` directive (or the `@` shorthand) and runs a method to update its own state

# emiting a signal

the emiting process happens in the methods of the child component. When a specific action occurs, such as a button click, the child component uses the `$emit` function to emit a custom event.

## Syntax

```Js
app.component( 'child-component', { 
  methods: { 
    methodName(){
    this.$emit('event-name', args) 
    }
}
```

# Receiving the Signal

The receiving process happens in the parent component's template where the child component is used. To listen to the custom event emitted by the child, the parent component uses the `v-on` directive or its shorthand `@` followed by the event name and the method to be executed when the event is received.

## Syntax

```html
<child-component @event-name="methodName"></child-component>
```

In the above code, `methodName` is a method in the parent component that will be executed when the child component emits the 'event-name' event.

# Example

```Html
<div id="app">  
<p>Message from child: <strong>{{ parentMessage }}</strong></p>  
  
<!-- The parent listens for the 'child-clicked' event from the child -->  
<child-button @child-clicked="updateMessage"></child-button>  
</div>  
  
<script>  
const app = Vue.createApp({  
data() {  
return {  
parentMessage: 'Waiting for child...'  
};  
},  
methods: {  
// This method is called when the child emits 'child-clicked'  
updateMessage(messageFromChild) {  
this.parentMessage = messageFromChild;  
}  
}  
});  
  
app.component('child-button', {  
template: `  
<div style="border: 1px dashed #666; padding: 10px; margin-top: 10px; background-color: #f0f0f0;">  
<p>Child Component</p>  
<button @click="handleClick">Click me!</button>  
</div>  
`,  
methods: {  
handleClick() {  
// The child emits a custom event 'child-clicked' and sends data  
this.$emit('child-clicked', 'Child button was clicked!');  
}  
}  
});  
  
app.mount('#app');  
</script>
```

# Notes

-  we can specify arguments/parameters in the child component's `$emit` function to pass data to the parent parent component.
- and we can use those parameters inside the parent component's method that is called BUT we need to remember that the order or the parameters will match the child component order