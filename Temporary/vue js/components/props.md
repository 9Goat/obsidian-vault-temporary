props (which stands for properties) is used as a way to receive data from a parent component to a child component in Vue.

#  Syntax

```Js
app.component('component-name',{
props: [ 'propName1', 'propName2',,,,, 'propNameN'];
// or
props: { 
  propName1: type1, 
  propName2: type2, 
  ........ 
  propNameN: typeN 
} 
,
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

- we can either define the props as an array of strings where each string is the name of the prop, or we can define the props as an object where the keys are the prop names and the values are the corresponding data types.
- props are also a key concept in component that we must separate by comma `,` just like data or methods
- we can treat the props variable as if we have a data property with the same name as the prop.
- props are defined as **READ -ONLY** by default, meaning that we cannot change the value of a prop directly from within the child component.

# sending data from parent to child

the entire point of props is that we send data from a parent component or main to a child component ,we can do  that by specifying the prop name in HTML when we call the child component.

## Syntax

```Html
// parent component:

<component-name v-bind:propName1 = "dataToSend"></component-name>
```

- the [[v-bind]] is optional we only use it if we want to pass a variable from the parent  component otherwise we can just pass a static value directly.
# Example

```Html
<div id="app">
    <!-- Calling the child component and passing a string directly -->
    <child-message message="Hello from the parent!"></child-message>

    <!-- Calling the child component and binding a data property from the parent -->
    <child-message :message="parentDataMessage"></child-message>
  </div>

  <script>
    const app = Vue.createApp({
      data() {
        return {
          parentDataMessage: 'This message comes from the parent\'s data!'
        };
      }
    });

    // Registering the child component
    app.component('child-message', {
      props: ['message'],
      template: `
        <div style="border: 1px dashed #666; padding: 8px; margin-bottom: 5px; background-color: #f0f0f0;">
          <p><strong>Child Component:</strong> {{ message }}</p>
        </div>
      `
    });

    app.mount('#app');
  </script>
```

# props specifications

in props we could either call the variable by its name,or we could make it an object where it contains specifications on how to handle the prop. keep in mind that specifications are **OPTIONAL**

## Syntax

```Js
props:[

propName1{
specification1: value1, 
specification2: value2, 
..., 
specificationN: valueN 
}, 

propName2,

... , 
propNameN 
]
```

## types of specifications

props offers 4 types of specifications which are:

- type
- required
- default
- validator

### type specification

if we want a certain prop to be of a specific type, we can specify it using the `type` property. If the datatype of the value passed does not meet the specification ,vue will throw an error in the console

vue only allows these datatypes for specifications:

- `String`
- `Number`
- `Boolean`
- `Array`
- `Object`
- `Date`
- `Function`
- `Symbol`
- `Error`

there are 2 types of type specifications which are:

- single
- array

#### single type specification

in this case we only expect a single datatype from our prop

##### Syntax

```Js
props:[

propName1{
type: datatype, 
}
]
```

##### Example

```Html
<div id="app">  
<child-message :message="parentDataMessage"></child-message>  
</div>  
  
<script>  
const app = Vue.createApp({  
data() {  
return {  
parentDataMessage: 123 //this will cause a type conflict warning
};  
}  
});  
  
// Registering the child component  
app.component('child-message', {  
props: {  
message: {  
type: String  
}  
},  
template: `  
<div style="border: 1px dashed #666; padding: 8px; margin-bottom: 5px; background-color: #f0f0f0;">  
<p><strong>Child Component:</strong> {{ message }}</p>  
</div>  
`  
});  
  
app.mount('#app');  
</script>  
```

#### array type specification

very  similar to single except that we pass an array of datatypes and it will accept one of the datatypes ,otherwise it will thrown a warning if none of them matches

##### Syntax

```js
props:[

propName1{
type: [datatype1, datatype2, ..., datatypeN],
}
]
```

##### Example

```Html
<div id="app">
    <h2>Parent Component</h2>
    <p>Passing different types to the child component:</p>

    <!-- Passing a String -->
    <flexible-message :content="stringMessage"></flexible-message>

    <!-- Passing a Number -->
    <flexible-message :content="numberMessage"></flexible-message>

    <!-- Passing an incompatible type (Boolean) - this will cause a warning in the console -->
    <flexible-message :content="booleanMessage"></flexible-message>
</div>

<script>
    const app = Vue.createApp({
        data() {
            return {
                stringMessage: 'This is a string message!',
                numberMessage: 42,
                booleanMessage: true // This will cause a type warning
            };
        }
    });

    // Registering the child component
    app.component('flexible-message', {
        props: {
            content: {
                // This prop can accept either a String or a Number
                type: [String, Number]
            }
        },
        template: `
            <div style="border: 1px solid #aaddaa; padding: 8px; margin-bottom: 5px; background-color: #eefee0;">
                <p><strong>Flexible Child:</strong> {{ content }} (Type: {{ typeof content }})</p>
            </div>
        `
    });

    app.mount('#app');
</script>
```

### required specification

it takes a boolean value indicating whether the prop is required or not. If set to `true`, Vue will warn if the prop is not provided.

#### Syntax

```javascript
props: {
  propName: {
    required: booleanValue
```

#### Example

```Html
<div id="app">    
<!-- This component call provides the required 'title' prop -->  
<required-prop-component title="This is a required title"></required-prop-component>  
  
<!-- This component call OMITS the required 'title' prop -->  
<required-prop-component></required-prop-component>  
</div>  
  
<script>  
const app = Vue.createApp({});  
  
// Registering the child component  
app.component('required-prop-component', {  
props: {  
title: {  
type: String,  
required: true // This prop MUST be provided by the parent  
}  
},  
template: `  
<div style="border: 1px solid #ccaaee; padding: 10px; margin-bottom: 10px; background-color: #f5eefd;">  
<h3>{{ title }}</h3>  
<p v-if="subtitle">Subtitle: {{ subtitle }}</p>  
<p v-else>No subtitle provided.</p>  
</div>  
`  
});  
  
app.mount('#app');  
</script>
```

### default specification

mostly used when required is set to **`false`** ,it is used to provide a prop with default value in case we did not provide it when calling the component.

#### Syntax

```javascript
props: {
  propName: {
    default: defaultValue
  }
}
```

#### Example

```html
<div id="app">
  <default-prop-component message="This is a provided message"></default-prop-component>

  <!-- This component call omits the 'message' prop, so it will use the default value -->
  <default-prop-component></default-prop-component>
</div>

<script>
  const app = Vue.createApp({});

  // Registering the child component
  app.component('default-prop-component', {
    props: {
      message: {
        type: String,
        default: 'This is the default message if none is provided.' // The default value
      }
    },
    template: `
      <div style="border: 1px solid #aaddff; padding: 10px; margin-bottom: 10px; background-color: #e0f5ff;">
        <h3>Message: {{ message }}</h3>
      </div>
    `
  });

  app.mount('#app');
</script>
```

#### Notes

- if the default value is different than the types allowed in the specification we will get a warning in the console

### Validator specification

is used to determine whether the value entered is valid or not.To do that we create a function called `validator(value)` which returns a boolean. If validator returns false we will get a console warnings

#### Syntax

```javascript
props: {
  propName: {
    validator(value) {
      // The validator function receives the prop's value as an argument
      // It must return true if the value is valid, false otherwise.
      return booleanExpressionBasedOnValue;
    }
  }
}
```

#### Example

```html
<div id="app">
    <h2>Parent Component</h2>
    <p>Demonstrating the 'validator' prop specification:</p>

    <!-- Valid number (positive) -->
    <my-number :num="10"></my-number>

    <!-- Invalid number (zero) - will cause a Vue warning in the console -->
    <my-number :num="0"></my-number>

    <!-- Invalid number (negative) - will cause a Vue warning in the console -->
    <my-number :num="-5"></my-number>
</div>

<script>
    const app = Vue.createApp({});

    app.component('my-number', {
        props: {
            num: {
                type: Number,
                // Validator checks if the number is positive
                validator(value) {
                    return value > 0;
                }
            }
        },
        template: `
            <div style="border: 1px solid #ccc; padding: 8px; margin-bottom: 5px;">
                <p>The number is: <strong>{{ num }}</strong></p>
            </div>
        `
    });

    app.mount('#app');
</script>
```