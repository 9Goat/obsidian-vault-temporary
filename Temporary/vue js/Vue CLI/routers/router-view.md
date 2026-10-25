is used to showcase the corresponding view page from our current page path

# Syntax

```Html
//inside the app page (App.vue)
<template>
<nav>
<router-link to="path">link text here</router-link>
</nav>

<router-view/>
</template>
```

for example when we start a page our default path is usually **`/`** meaning [[router-view]] will look for which view page correspondence to that path from the routes object and display it

# Example

```Html
<!-- App.vue (This is your main application component) -->
<template>
  <div id="app">
    <h1>My Vue Router App</h1>
    <nav>
      <!-- Link to the Home route (path: '/') -->
      <router-link to="/">Home</router-link> |

      <!-- Link to the About route (path: '/about') -->
      <router-link to="/about">About</router-link> |

      <!-- Link to the Contact route (path: '/contact') -->
      <router-link to="/contact">Contact</router-link>
    </nav>

    <hr>

    <!-- This is where the component for the current route will be rendered -->
    <router-view></router-view>
  </div>
</template>
```

