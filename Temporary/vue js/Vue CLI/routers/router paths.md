we can set up router paths and decide what each path will show to the user

# file navigation


![[image-38.png|400x200]]

inside the router folder we can find the index.js file which contains all the paths in the router

![[image-39.png]]

# 1 imports section

this section contains the import statements of the vue router function and all the views that we are going to link to different paths

meaning if we want to add a new view to our paths we have to follow this syntax

## Syntax

```Js
import VueFileName from 'PathToTheVueFile';
```

- it is best practice to name the vue file using camel case


# 2. paths section

the section contains a routes object array that includes all the paths defined in the application, where each path is associated with a specific view or component that will be rendered when the user navigates to that path.

## Static route path

### Syntax

```Js
const routes = [
  {
path: '/', 
    name: 'Home', 
    component: HomeView 
  }, 
  { 
    path: '/path', 
    name: 'componentName', 
    component: importedComponent
  } 
]
```

- the slash `/` in path resembles the main page/home of the website
- for now we are only using these 3 parameters to set up a route which are:
	- **`path`** : the URL path that the route will respond to, 
	- **`name`**: a unique identifier for the route,
	- **`component`**: the Vue component that will be rendered when the route is accessed.

### Example

```Js
// router/index.js (This file defines your routes)

import { createRouter, createWebHistory } from 'vue-router';

import HomeView from '../views/HomeView.vue';
import AboutView from '../views/AboutView.vue';
import ContactView from '../views/ContactView.vue';

// 2. Define your static routes
const routes = [
  {
    path: '/', 
    name: 'Home',
    component: HomeView 
  },
  {
    path: '/about',
    name: 'About',
    component: AboutView
  },
  {
    path: '/contact',
    name: 'Contact',
    component: ContactView
  }
];
```
## 3. router creation

after we have defined our paths, we create a new instance of the Vue Router, passing an object with the routes configuration to it.

this object contains 2 properties:

- createWebHistory: which defines how our function will handle history requests like going back a page in the browser
- routes: which contains the list of all of our paths

## 4. exporting the router

after creating the Vue Router instance, we need to make it available to the rest of the application by exporting it, typically as the default export of the index.js file in the router folder.

in JS to export a variable and make it possible to import in to other js files we use the following syntax

## Syntax

```Js
export default variableName;
```
