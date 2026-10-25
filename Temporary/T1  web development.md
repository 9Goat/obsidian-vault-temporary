# String functions

```js
let s = "hello world";

alert(s.length); // 11

alert(s.charAt(1)); // "e"

alert(s.charCodeAt(1)); // 101

alert(s.slice(3)); // "lo world"

alert(s.slice(-3)); // "rld"

alert(s.substring(3,7)); // "lo w"

alert(s.indexOf("o")); // 4

alert(s.lastIndexOf("o")); // 7

alert(s.toUpperCase()); // HELLO WORLD

alert(s.toLowerCase()); //hello world

alert(s.split(" ")); // [hello],[world]

alert(s + " !"); // hello world !

```

# Math functions

```js
alert(Math.E); // la valeur de e

alert(Math.PI); // la valeur de pi

alert(Math.min(5,12)); // 5

alert(Math.max(23,5,7,130,12)); // 130

alert(Math.ceil(25.3)); // 26

alert(Math.floor(25.8)); //25

alert(Math.random()); // valeur aléatoire entre 0 et 1

let x =5,y=3;

alert(Math.abs(x))

alert(Math.exp(x)) 

alert(Math.log(x))

alert(Math.pow(x,y))

alert(Math.sqrt(x))

alert(Math.sin(x)) 

alert(Math.cos(x))

alert(Math.tan(x))
```

# date functions 


| getFullYear() | Donne l’année : year sous le format<br><br>numérique |
| ------------- | ---------------------------------------------------- |
| getMonth()    | Récupère le mois : month (0-11)                      |
| getDate()     | Récupère le jour : day (1-31)                        |
| getHours()    | Récupère l’heure : hour (0-23)                       |
| getMinutes()  | Récupère les minutes : minute (0-59)                 |
| getSeconds()  | Récupère les secondes : second (0-59)                |
| getDay()      | returns the day in a number between 0-6              |
that is to get the date **BUT** to set the date we use `set` instead of `get`

# Array functions

```js

var colors = new Array(); // tableau vide

var colors2 = new Array(20); // tableau avec 20 cases

var colors3 = new Array("red","blue","green"); // 3 cases

var colors4 = ["red","blue","green"]; // notation littérale

var colors = ["red","blue","green"];
alert(colors.length); // 3

colors[colors.length]="black"; // nouvelle couleur

colors[99]="pink";

alert(colors.length); // 100

alert(colors[50]): // undefined

colors.length=10; // plus que 10 cases

var colors = ["red","blue","green"];

alert(colors); // red,blue,green

alert(colors.join(";")); // red;blue;green

colors.push("black"); //Ajouter un élément à la fin du tableau

alert(colors); // red,blue,green,black

var item = colors.pop(); // Enlever le dernier élément du tableau

alert(item + " " + colors); // black red,blue,green

var item2= colors.shift(); // Enlever le premier élément du tableau

alert(item2 + " " + colors); // red blue,green

colors.unshift("yellow"); // Ajouter un élément au début du tableau

alert(colors); // yellow,blue,green

var values = [0, 1, 2, 3, 4];

alert(values.reverse()); // 4,3,2,1,0

values = [0, 1, 15, 10, 5];

alert(values.sort()); // 0, 1, 15, 10, 5
```

# Object functions :

```js
var personne = new Object();

personne.nom = "Wissam";

personne.age = 23;
//ou bien
var personne = { nom : "Wissam", age : 23 }

const person = {

firstName: "John",

lastName : "Doe",

id : 5566,

fullName : function() {
return this.firstName + " " + this.lastName;
}

alert(personne.nom);

alert(personne["nom"]);

var attribut="age"; alert(personne[attribut]); //23

for (var pers in personne)

document.writeln(pers + " : " + personne[pers] );

//nom : Wissam age : 23
```

# Events

- **onClick**: When the user clicks a button, link, or any other element.
- **onDbClick**: When the user double-clicks a button, link, or any other element.
- **onLoad**: When the page is loaded by the browser.
- **onUnload**: When the user leaves the page.
- **onMouseOver**: When the user places the mouse pointer over a link or any other element.
- **onMouseOut**: When the mouse pointer leaves a link or any other element.
- **onMouseUp**: When the user releases the mouse button.
- **onMouseDown**: When the user presses the mouse button on an element.
- **onFocus**: When a form element gains focus, meaning it becomes the active input area.
- **onBlur**: When a form element loses focus, meaning the user clicks outside the field and the input area is no longer active.
- **onChange**: When the value of a form field is modified.
- **onSelect**: When the user selects a field within a form element.

```js
lien.addEventListener('click', function () {
alert('Retour à l\'accueil !'); // allows you to execute a function upon an evenemt
})
```

# DOM functions

```js
document // represents the entire web page

document.getElementById("message")

document.getElementsByName('assaisoner'); //multiple elements in a list not just a single element like id

document.getElementsByTagName("p");

document.getElementsByClassName("id");

document.querySelector('input[name=paiement]:checked') // allows us to select elements using CSS selectors (a  single FIRST element will be selected not multiple)

document.querySelectorAll("p"); // save as above but returns all elements that match the selector

document.getElementById(id).innerHTML // converts the content of the element (HTML) to string that we can store in a variable or modify

document.getElementById('message').textContent

document.getElementById(identifiant_element).text //also used to get the text of an element

nb = document.getElementById("nbP").value;

fichier = document.getElementById("fichier").value; // for files .value gets the path for the image -> chemin_sur_disque/plan.gif

document.getElementById(identifiant_element).defaultValue // to access its default value we gave to it in html  with the attribute value

document.getElementById(id).nom_attribut = new value // allows us to access the value of a specific attribute like src and modify it

e.style.color = 'red'; // allows you to change the CSS style of an element
```

## For checkbox and radio

```js
document.getElementById(identifiant_element).checked

let carte = document.querySelector('input[name=paiement]:checked').value;

document.getElementById(identifiant_element).defaultChecked // looks for elements that have the checked attribe in HTML
```

## For select drop lists

```js
document.getElementById(identifiant_element)[num_element].selected //checks if an option in the list is selected or not

document.getElementById(identifiant_element).selectedIndex //returns the index (from 0 to length -1) of the *first* selected option
```

## For accessing a collection of elements

to access a collect of elements just like getElementsByTagName we can use call certain elements that will return a list of their elements that share the same type

```js
document.body //access ALL <body>

document.documentElement//access ALL <html>

document.forms//access ALL <form>

document.title//access ALL <title>

document.head//access ALL <head>

document.images//access ALL <img>

document.links//access ALL <a>

document.scripts//access ALL <script>
```

# Node DOM 

```js
document.getElementById("id").parentNode //access the direct parent node of this element (node is different than an element)

document.getElementById("id").parentElement

document.getElementById("id").childNodes // returns a list of all DIRECT nodes that are within that element

document.getElementById("id").children //for elements only

document.getElementById("id").firstChild // returns the FIRST DIRECT child node of that element

document.getElementById("id").firstElementChild

document.getElementById("id").lastChild

document.getElementById("id").lastElementChild

document.getElementById("id").nextSibling // returns the next element that is in the same tree level

document.getElementById("id").nextElementSibling

document.getElementById("id").previousSibling

document.getElementById("id").previousElementSibling

document.createElement("p"); // creates an empty elements that we can modify

document.createTextNode("This is new."); // same but this is just text and not an element

document.getElementById("id").appendChild(node); // appends an element at the end of the node

document.getElementById("id").prepend(element) //adds at the beginning of the node

element.insertBefore(newElement,child); // allows you to insert a new element before an already existing element inside that node

// if the reference element (second argument) is NULL then it will add it at the end just like appendChild

// otherwise if the newElement already exists it will just move it to that new position (insertBefore doesnt create duplicates)

document.getElementById("id").replaceChild(newChild,oldChild) //if it already exists it will just move it to the new position of the old child (replaces only once not all instances)

parent.removeChild(child); // removes the direct element within the paramters from that node 

document.getElementById("id").hasChildNodes //returns true or false if that element has direct child nodes or not 

document.getElementById("id").hasAttributes // returns True or false if it has any attributes

document.getElementById("id").hasAttribute("attribute") //returns true of false if that specific attribute exists within that element

document.getElementById("id").getAttribute("attribute") //returns the value that the attribute is holding (if it has no value it will return an empty string "")

document.getElementById("id").setAttribute("attribute","value") // allows you to add the attribute with that value if it doesnt exist otherwise it will just change the value of that existing attribute

document.getElementById("id").removeAttribute("attribute")

document.createElement("element name")

clone = document.getElementById("id").cloneNode(boolean) //return a copy of that node depending on the boolean value -True : copies the node and all its child nodes with it -False: only that node is copied and its attributes/value without child nodes
```

## element types and their node values

```js
document.getElementById("id").nodeValue //its return value depends on the type of element (look below)

document.getElementById("id").nodeType //returns a number that indicates the type of element being accessed
```

| Element Type | NodeType | `nodeValue` Returns                                    |
|:------------ |:-------- |:------------------------------------------------------ |
| Element      | 1        | `null`                                                 |
| Attribute    | 2        | The value of the attribute (as a string)               |
| Text         | 3        | The text content of the node (as a string)             |
| Comment      | 8        | The content of the comment (as a string, excluding ``) |
| Document     | 9        | `null`                                                 |



