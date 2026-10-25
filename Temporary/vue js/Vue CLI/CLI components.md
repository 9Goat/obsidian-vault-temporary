in CLI we no longer create components in js files but instead we write them in vue files which means we need a different context for the vue file to recognize it,But thankfully they both are very similar meaning we dont have to learn many new things

# template

## Syntax

```Html
<template>
//html elements here
</template>
```

this is the equivalent of writing template: \` html elements here\` in the js components

# script

this is the section where we write our vue component's JavaScript code, it is equivalent to the object that we used to create in the JavaScript files, but now it's enclosed within the `<script>` tag. The syntax is as follows:

## Syntax

```Html
<script>
// JavaScript code here
export default {
  // component options here
}
</script>
```

this allows us to define the component's properties, data, methods, lifecycle hooks and more, just like we did before, but now in a more organized and structured way.

# style

we can also add CSS styles to our Vue components using the `<style>` tag. Usually the style would affect all the components in the same page To avoid this, Vue provides a special attribute called `scoped` that can be added to the `style` tag, allowing the CSS styles to be applied only to the current component. The syntax for this is as follows:

## Syntax

```Html
<style scoped>
//CSS styles here
</style>
```


# Example

```Html
<!-- MySimpleComponent.vue -->
<template>
  <div class="my-component">
    <h1>{{ title }}</h1>
    <p>This is a basic Vue component.</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: 'Hello from SFC!'
    };
  }
};
</script>

<style scoped>
.my-component {
  border: 1px solid #42b983;
  padding: 15px;
  margin: 10px;
  background-color: #e6ffe6;
  color: #2c3e50;
  border-radius: 5px;
}

h1 {
  color: #42b983;
}
</style>
```

