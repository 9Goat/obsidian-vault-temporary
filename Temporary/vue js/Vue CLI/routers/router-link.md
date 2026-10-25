router links are used are a replacement to the standard HTML anchor tags. They allow users to navigate between routes in a single-page application. When a user clicks on a router link, the router will navigate to the corresponding route without requiring a full page reload.

# Syntax

```Html
//inside the app page (App.vue)
<template>
<nav> //router links are usually placed inside of nav bars
<router-link to="path">link text here</router-link>
</nav>
</template>
```

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

# Notes

- we could apply CSS to those links and when the link is active by using the following classes
	- **rounter-link-active**: which selects all the paths where it contains the parent path
		- **Example** for path /jobs we can also accept /jobs/frontEndDev
	- **rounter-link-exact-active**: very similar to the above except that we only accept the parent path and not children paths
		- **Example** for path /jobs we **CANNOT** accept /jobs/frontEndDev

## Example 1

```Css
/* Example 1: CSS for router-link-active and router-link-exact-active */

/* Styles for any link that is part of the current active route path */
.router-link-active {
  color: blue;
  font-weight: bold;
  text-decoration: underline;
}

/* Styles for the link that exactly matches the current active route path */
.router-link-exact-active {
  color: green;
  font-weight: bolder;
  border-bottom: 2px solid green;
}
```

