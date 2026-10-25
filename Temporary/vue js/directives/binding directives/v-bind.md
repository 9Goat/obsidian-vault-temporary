used to bind expressions and variables from js or vue js to be the value of HTML attributes or content.

# Syntax

## Full Syntax

```Html
<element v-bind:attribute-name="expression" />
```

## Shorthand Syntax

You can use the `:` symbol as a shorthand for `v-bind:`.

```Html
<element :attribute-name="expression" />
```

**Core Principle:** The value inside the quotes (`"expression"`) is treated as **raw JavaScript** and is actively monitored by Vue. When the underlying data changes, the attribute is automatically updated.

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
<button :disabled="isTrue">if you see this that mean isTrue is true</putton>
</div>
<script>
    const { createApp } = Vue; 

    const app = createApp({
        data() {
            return {  
                isTrue: true
            };
        }
    });
    const mountedApp = app.mount("#app");
</script>
</body>
</html>
```

# Notes

there a very important concept in binding called style binding,for it to be valid we need to remember that styles in CSS accept only objects meaning

## Syntax 1 of style binding

```Html
<element :style="{ attribute1: variable, attribute2: variable }">
  </element>
```

## Syntax 2 of style binding

```Html
<element :style="style"> </element>

data(){

return{
style: {color:"red",fontSize:"30px"}
}

}
```

## Example

```Html
<div id="app">
<p :style="style">This is a styled text</p>
<p :style="{color: color, backgroundColor: backgroundColor, fontSize: '30px'}">This is another styled text</p>
</div>
<script>
    const { createApp } = Vue; 

    const app = createApp({
        data() {
            return {
                color:"red",
                backgroundColor: "blue",
                style: {color:"red",fontSize:"30px"}
            };
        }
    });
    const mountedApp = app.mount("#app");
</script>
```

