used to perform a for loop operation on iterables. Where each time it iterates over the iterable, it executes the element that contains the for loop

# Syntax

```Html
<element v-for= "(item, index) in items">
//perform operations or statements with those elements
</element>
```

- **`item`** represent each element of the iterable being looped through
- **`index` (OPTIONAL)** the index of the current element being processed in the iterable,
- **`items`** represents the iterables
	- arrays
	- objects
	- number
	- string
- if there is only one argument for the v-for directive, we dont need to surround it with parentheses `()`
- arguments inside of parentheses `()` must be separated by commas `,`

# How it works with different iterables

the way to use for loops changes with the type of iterable being used. 

## Arrays and Strings

the simplest ,you basically iterate thought 1 element at a time

### Example

```Html
<div id="app">
<ul>
    <li v-for="(item, index) in items">{{ index }}: {{ item }}</li>
</ul>
</div>
<script>
    const { createApp } = Vue; 

    const app = createApp({
        data() {
            return {  
                items: ["Item 1", "Item 2", "Item 3"]
            };
        }
    });
    const mountedApp = app.mount("#app");
</script>
```

## Objects

When iterating over objects, you have the option to access the key, value, or both.

### Syntax

```Html
<element v-for= "(value, key, index) in items">
//perform operations or statements with those elements
</element>
```

### Example

```Html
<div id="app">
<ul>
    <li v-for="(value, key,index) in items">{{index}}: {{ key }}: {{ value }}</li>
</ul>
</div>
<script>
    const { createApp } = Vue; 

    const app = createApp({
        data() {
            return {  
                items: {name: "John", age: 30, city: "New York"}
            };
        }
    });
    const mountedApp = app.mount("#app");
</script>
```

## Number

extremely similar to python `for i in range(number)`

### Example

```Html
<div id="app">
<ul>
    <li v-for="(value,index) in items">{{index}}: {{ value }}</li>
</ul>
</div>
<script>
    const { createApp } = Vue; 

    const app = createApp({
        data() {
            return {  
                items: 10
            };
        }
    });
    const mountedApp = app.mount("#app");
</script>
```

