# components

## creating components

to create a component we use the following command:

```bash
ng generate component <component-name>
```

- **Note**: ng is the main command for angular

## files of the components

when creating a component we find 4 files inside of it which are the followings:

- an html file for writing the html content of the component
- a css file for writing the css content of the component
- ts file which is contains all the functionalities of the component
- spec.ts file which is used for unit testing

we will only be focusing on the ts file for now

### ts file

when first creating that file we get 2 important things inside of it which are the following:

- meta data of the component, like the html and css file connected to it, what the component name is ,,,etc
- an export class methods which contains all the logic and functionalities of the component

```ts
@Component({
  selector: 'app-user-profile',      // 1. The custom HTML tag for this component
  standalone: true,                  // 2. Specifies if this is a standalone component
  templateUrl: './user-profile.html',// 3. Path to the UI/HTML file
  styleUrl: './user-profile.css',    // 4. Path to the component-specific styles
  imports: []                        // 5. List of external modules or components needed
})
export class UserProfileComponent { }
```

## linking child component with parent component

to put a child component inside a parent component, we first need to specify the standalone option to be `true`

after that we simply add the child component to the list of imports and call it by its selector name in the html file

**TS file**:

```ts
import { SingleProduct } from '../single-product/single-product';  
  
@Component({  
selector: 'list-of-products',  
standalone: true,  
imports: [SingleProduct],  
templateUrl: './list-of-products.html',  
styleUrl: './list-of-products.css',  
})
```

**HTML file**:

```html
<p>list-of-products works!</p>  
<p>{{x}}</p>  
  
<single-product></single-product>
```

# event listeners 

to add event listeners like on click we put the event inside of parentheses

## Example

**Html file**:

```html
<ul>  
@for (product of numberOfProductsArray; track $index) {  
<li>  
<button (click)="removeElement($index)"> remove element</button><single-product [integer]="product + 1"></single-product>  
</li>  
}  
</ul>
```

**typescript file**

```ts
removeElement(index: number) : void{  
this.numberOfProductsArray.splice(index,1)  
console.log(this.numberOfProductsArray)  
}
```
# Directives

## for loop

the newest way to use a for loop is with the @for keyword here is how it works:

there are 3 things to consider when using the loop directive which are the followings:

```html
@for (item of items; track item.id; let i = $index, isFirst = $first, ...) {
  ...
}
```

-  the loop item which is written as **`item of items`**
- the id of each loop is written as **`track uniqueItem`**
- other variables to store (mostly booleans)

| **Variable** | **Use Case Example**                                                                                       |
| ------------ | ---------------------------------------------------------------------------------------------------------- |
| **`$count`** | Useful for showing "Page 1 of X" or displaying a total tally in a UI header.                               |
| **`$index`** | Essential for numbering lists (e.g., `i + 1`) or performing calculations based on position.                |
| **`$first`** | Use this to add a special CSS class (like `border-top`) or show a "Header" element only on the first item. |
| **`$last`**  | Use this to hide a separator line after the final item in a list.                                          |
| **`$even`**  | Commonly used for "Zebra Striping" (e.g., `[style.background]="isEven ? 'gray' : 'white'"`).               |
| **`$odd`**   | The inverse of `$even`, used for alternating row colors or alternating layout directions.                  |
### Example

```html
<ul>
  @for (user of users; track user.name; 
        let i = $index, 
        isFirst = $first, 
        isLast = $last, 
        isEven = $even, 
        isOdd = $odd, 
        count = $count) {
    
    <li [class.highlight]="isEven">
      Row {{ i + 1 }} of {{ count }}: 
      {{ user.name }} 
      {{ isFirst ? '(Start)' : '' }} 
      {{ isLast ? '(End)' : '' }}
      {{ isOdd ? '- [Odd row]' : '- [Even row]' }}
    </li>
  }
</ul>
```

## if directives

```html
@if (a > b) {
  {{a}} is greater than {{b}}
} @else if (b > a) {
  {{a}} is less than {{b}}
} @else {
  {{a}} is equal to {{b}}
}
```

## switch directive

```html
@switch (userPermissions) {
  @case ('admin') {
    <app-admin-dashboard />
  }
  @case ('reviewer')
  @case ('editor') {
    <app-editor-dashboard />
  }
  @default {
    <app-viewer-dashboard />
  }
}
```

## let directive

sometimes we create a varaible just for a simple use inside the html template, instead of creating it inside the ts template we can use the let directive and use it directly inside the html template

```html
@let user = user$ | async;
@if (user) {
  <h1>Hello, {{user.name}}</h1>
  <user-avatar [photo]="user.photo"/>
  <ul>
    @for (snack of user.favoriteSnacks; track snack.id) {
      <li>{{snack.name}}</li>
    }
  </ul>
  <button (click)="update(user)">Update profile</button>
}
```

- **Important**: let variables are **CONSTANTS** once a values is given to a  let variable it **CANNOT** be resigned 

## loading directives

this category contains many directives including the following:

- @defer
- @placeholder
- @loading
- @error
# parrent and child components

## passing data from parent to child
to pass data from parent to child we use the **`@Input`** keyword

**child component**

we first need to import the input keyword and then define the variable that we will be receiving from the parent with this syntax

```ts
import { Component, Input} from '@angular/core';  
  
@Component({  
selector: 'single-product',  
imports: [],  
templateUrl: './single-product.html',  
styleUrl: './single-product.css',  
})  

export class SingleProduct {  
@Input("integer") i:number = 0;  
}
```

- the string inside the parentheses specifies the alias of the variable we will be passing inside the parent component

**parent component**

after that inside the child component class in the html file we pass the value to the child

```html
<ul>  
@for (product of numberOfProductsArray; track $index) {  
<li>  
<single-product [integer]="product + 1"></single-product>  
</li>  
}  
</ul>
```


# running the project 

here is the main command to run the project:

```bash
ng serve
```

## computed

```ts
totalUsersCount = computed(() => this.users().length);
```