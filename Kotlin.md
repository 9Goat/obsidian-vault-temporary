# Kotlin basics

the 2 biggest advantages of using kotlin over  java are:

- fewer lines of code
- simplicity and  readability


## Variables

### How to declare variables

there are 3 ways to declare variables which are:

```kotlin
val message = "Bonjour tout le monde!" _// 1st: type inferred_

val message2: String = "Bonjour tout le monde!" _// 2nd: type written explicitly_

var message3: String = "Bonjour tout le monde!" _// 3rd: var + explicit type_
```

### Val and var

one of them is basic variable  the other is final that cannot change it values after intialization

|**Keyword**|**Meaning**|**Can be reassigned?**|**Java equivalent**|
|---|---|---|---|
|val (value)|A reference that **cannot change** once initialised|No|final|
|var (variable)|A variable whose content **can change**|Yes|a normal variable|


```kotlin
val message = "Bonjour tout le monde!" _// type String is guessed (inferred)_

var counter = 0 _// type Int is guessed_

counter = counter + 1 _// OK, it is a var_
_// message = "Salut" // ERROR: Val cannot be reassigned_
```

### lateinit

we CANNOT declare a var variable without instantly intializating  it

```kotlin
var name: String      // ERROR: property must be initialized
```

the solution to that is to use the lateinit keyword

```kotlin
lateinit name: String      // Correct
```


###  Constant in kotlin

to turn a final variable into constant we add the keyword **`const`** before it

```kotlin
const val URL: String = "https://mon serveur.com"
```



### Datatypes

  
|**Type**|**Example**|**Used for**|
|---|---|---|
|Int|42|whole numbers|
|Long|42L|big whole numbers|
|Double|4.5|decimal numbers (prices)|
|Float|4.5f|smaller decimals|
|Boolean|true / false|yes/no|
|Char|'A'|one character|
|String|"text"|text|

To convert data types we have to use the following syntax:
`variable/value.toDatatype`, where we replace Datatype with the datatype we want to convert to

```kotlin
val age: Int = "22".toInt() _// String -> Int_

val price: Double = "4.5".toDouble() _// String -> Double_

val text: String = 22.toString() _// Int -> String_
val safe: Int? = "abc".toIntOrNull() _// returns null instead of crashing_

_// val d: Double = 5 // ERROR: write 5.0_

val d: Double = 5.0
```

### Strings manipulation

**inside or print**: to print a variable inside a string message in print we use the **`$variable`** syntax

```kotlin
val nom = "Ali"
print("Bonjour $nom")
```

and to concat 2 strings together we use the plus **`+`** operator

```kotlin
var msg = "Spécialité "
msg += "SEM"
msg += " club Android"
println(msg)     // Spécialité SEM club Android
```
## Null safety

to avoid crashing the programming we can add the null safety notation to our variable so that it accept null values

```kotlin
var a: String = "Hello"

_// a = null // ERROR: String cannot be null_

var message: String? = "Mon message peut être null !" _// String? can be null_

message = null _// OK_
```


**Note**: trying to call a method while it is declared with null safety will cause an error 

```kotlin
var message: String? = "hello"
// message.uppercase()          // ERROR: the value may be null
```

**Here is how to call a method when a variable is declared with null safety**:

```kotlin
// 1) Safe call ?.  : does nothing and returns null if message is null
message?.uppercase()
 
// 2) Classic check
// inside the if, Kotlin knows it is not null
if (message != null) message.uppercase()
 
// 3) Elvis operator ?:  : give a default value
val length = message?.length ?: 0
 
 
// 4) !! : "I promise it is not null" (crashes if wrong - avoid!)
val l = message!!.length
```

### Summary

  
|**Operator**|**Name**|**Meaning**|
|---|---|---|
|? after a type|nullable type|this variable may be null|
|?.|safe call|call only if not null, else result is null|
|?:|Elvis|use the right side if the left side is null|
|!!|not-null assertion|force it; crashes if null|

## Functions

A function starts with fun, then its name, parameters with types, and the return type after a colon.

```Kotlin
fun add(a: Int, b: Int): Int {
    return a + b
}
 
println(add(2, 3))     // 5
```

### Short function

if the function only contains a single line we can write it like this

```kotlin
fun add(a: Int, b: Int) = a + b
 
private fun minOf(a: Int, b: Int) = if (a < b) a else b
```

### Unit  datatype

unit is the equivalent of void in java, when we have a method that does NOT return a value we use it

```kotlin
fun sayHello() = println("Hello !")             // returns Unit
fun sayHello2(): Unit = println("Hello !")      // same, type written
fun sayHello3(): Unit { println("Hello !") }    // same, with braces
```

## Operations in kotlin

this section will koltin operations that we see in every programming language, like loop, if else , switch,, etc

### If else operations

```kotlin
val ch = "Bonjour"
if (ch.length == 0) {
    print("la chaine est vide!")
} else if (ch.length < 5) {
    print("La chaine est courte!")
} else {
    print("La chaine est longue!")
}
```

### Switch operation

```kotlin
val x = "Samedi"
when (x) {
    "Samedi", "Dimanche" -> println("week-end")     // several values in one branch
    else -> println("jour de travail")
}
```

### for loops

```kotlin
val list = listOf("chaine1", "chaine2", "chaine3")
for (str in list) { print(str) }                        // loop on a list
 
for (i in 0..9) { print(i) }          // 0 to 9 (9 included)

list.forEach { print(it.toString()) }     // "it" is the current element
```

### while loops

```kotlin
var n = 3
while (n > 0) {          // test first
    println(n)
    n--
}
 
do {                     // body runs at least once
    println("once")
} while (false)
```

### Continue and break

work in all loops

```kotlin
while (true) {
    if (condition1) {
        continue      // jump to the next iteration, skip the rest of the body
    }
    if (condition2) {
        break         // leave the loop completely
    }
}
```

## Class and objects

kotlin by defaults generate the constructor and getters and setters for us, for example this single like of code in kotlin

```kotlin
class User(var email: String, var password: String, var age: Int)
```

is equivalent to the following code in java

![[image-454.png]]

### Objects in kotlin

unlike java we dont use the **`new`** keyword to create objects, instead we call classes the same way we call functions

```kotlin
val user = User("hello@gmail.com", "azerty", 27)   // no "new" in Kotlin!
println(user.email)               // getter: user.email
user.email = "new_email@gmail.com"    // setter
```

### Inheritance and implementation

- with parameters: inheritance
- without: implementation

```kotlin
class MainActivity : AppCompatActivity()                    // extends a class: with ()
// + implements an interface: no ()
class MainActivity : AppCompatActivity(), OnItemClickListener
```

## Access modifiers

the same as java except that we have internal instead of package

|**Modifier**|**Visible...**|
|---|---|
|public (default)|everywhere|
|private|only inside the class (or file) where it is declared|
|protected|inside the class and its subclasses|
|internal|inside the same module|

# Jetpack Compose

in compose the ui is generated depending on the given state

![[image-455.png]]

## Components

### Creating simple components with composable

![[image-457.png]]
### Displaying components

this is the equivalence of using int main in c to execute a program

```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            BonjourScreen()
        }
    }
}
```

### 1. Text Components

#### Text

Displays text on screen.

- `text` (String): The text content to display
- `fontSize` (TextUnit): Size of the text (e.g., `24.sp`)
- `fontWeight` (FontWeight): Thickness of text (e.g., `FontWeight.Bold`, `FontWeight.Normal`)
- `color` (Color): Color of the text (e.g., `Color.Blue`, `Color.White`)

---

### 2. Button Components

#### Button

A clickable button with a content slot.

- `onClick` (() -> Unit): Lambda executed when button is clicked
- `enabled` (Boolean): Whether the button is clickable (optional)
- `modifier` (Modifier): Styling, sizing, and positioning (optional)
- `content` (@Composable): Content inside the button (typically a Text)

---

### 3. Image Components

#### Image

Displays an image from resources.

- `painter` (Painter): The image resource (e.g., `painterResource(R.drawable.photo)`)
- `contentDescription` (String): Accessibility description of the image
- `modifier` (Modifier): Size, padding, and other styling (optional)

---

### 4. Spacing Components

#### Spacer

Adds empty space between elements.

- `modifier` (Modifier): Must specify `height()` or `width()` to determine space size

---

### 5. Text Input Components

#### TextField

Standard text input field.

- `value` (String): Current text value in the field
- `onValueChange` ((String) -> Unit): Callback when text changes, receives new text
- `modifier` (Modifier): Styling and sizing (optional

#### OutlinedTextField

Text input with an outline border.

- `value` (String): Current text value in the field
- `onValueChange` ((String) -> Unit): Callback when text changes
- `label` (@Composable): Label text displayed inside the field (optional)
- `modifier` (Modifier): Styling and sizing (optional)

---

### 6. Selection Components

#### Checkbox

A checkbox that can be checked/unchecked.

- `checked` (Boolean): Current checked state
- `onCheckedChange` ((Boolean) -> Unit): Callback when state changes, receives new state

#### Switch

A toggle switch (on/off).

- `checked` (Boolean): Current on/off state
- `onCheckedChange` ((Boolean) -> Unit): Callback when toggled, receives new state

#### RadioButton

A radio button for single selection.

- `selected` (Boolean): Whether this option is currently selected
- `onClick` (() -> Unit): Callback when the radio button is clicked

---

### 7. Container Components

#### Card

A material design card with elevation and rounded corners.

- `modifier` (Modifier): Padding, size, and positioning (optional)
- `elevation` (Dp): Shadow depth (e.g., `CardDefaults.cardElevation(4.dp)`)
- `content` (@Composable): Content inside the card

---

### 8. Layout Components

#### Column

![[image-460.png]]

Arranges children vertically in a sequence.

- `modifier` (Modifier): Size, padding, background, etc.
- `verticalArrangement` (Arrangement): How children are distributed vertically (Start, Center, End, SpaceBetween, SpaceAround, SpaceEvenly)
- `horizontalAlignment` (Alignment): How children are aligned horizontally (Start, CenterHorizontally, End)

#### Row

![[image-466.png]]

Arranges children horizontally in a sequence.

- `modifier` (Modifier): Size, padding, background, etc.
- `horizontalArrangement` (Arrangement): How children are distributed horizontally (Start, Center, End, SpaceBetween, SpaceAround, SpaceEvenly)
- `verticalAlignment` (Alignment): How children are aligned vertically (Top, CenterVertically, Bottom)

#### Box

![[image-467.png]]

Stacks children on top of each other (equivalent to FrameLayout).

- `modifier` (Modifier): Size of the box
- `contentAlignment` (Alignment): Default alignment for all children (TopStart, TopCenter, TopEnd, CenterStart, Center, CenterEnd, BottomStart, BottomCenter, BottomEnd)
- `content` (@Composable): Children that will be stacked

---

### 9. List Components

![[image-468.png]]

#### LazyColumn

Efficient scrolling vertical list for large datasets.

- `modifier` (Modifier): Size constraints and styling
- `content` (LazyListScope): DSL block containing `items()` calls
    - `items(list)` (List): Iterates over a list of data
    - `item` (Any): Single item in the list

#### LazyRow

Efficient scrolling horizontal list for large datasets.

- `modifier` (Modifier): Size constraints and styling
- `content` (LazyListScope): DSL block containing `items()` calls
    - `items(list)` (List): Iterates over a list of data
    - `item` (Any): Single item in the list

#### LazyVerticalGrid

Efficient scrolling grid layout.

- `columns` (GridCells): Grid configuration (Fixed(n) for fixed columns, Adaptive for auto-sizing)
- `modifier` (Modifier): Size constraints and styling
- `content` (LazyGridScope): DSL block containing `items()` calls
    - `items(list)` (List): Iterates over a list of data
    - `item` (Any): Single item in the grid


 
|**Old world (Views)**|**New world (Compose)**|
|---|---|
|TextView|Text()|
|Button|Button()|
|LinearLayout (vertical)|Column()|
|LinearLayout (horizontal)|Row()|
|FrameLayout|Box()|
|findViewById()|not needed|
|setText() / LiveData|state (mutableStateOf)|
|Observer|recomposition|
|RecyclerView + Adapter + ViewHolder|LazyColumn / LazyRow|
|GridView|LazyVerticalGrid|

### Modifiers

#### **Size & Dimension Modifiers**

- `Modifier.fillMaxSize()` – Fills the entire available space (both width and height)
- `Modifier.fillMaxWidth()` – Fills the entire available width
- `Modifier.fillMaxHeight()` – Fills the entire available height
- `Modifier.height(100.dp)` – Sets a specific height
- `Modifier.width(100.dp)` – Sets a specific width
- `Modifier.size(56.dp)` – Sets both width and height to the same value

#### **Spacing Modifiers**

![[image-463.png]]

- `Modifier.padding(16.dp)` – Adds space around the component (equivalent to margins)
- `Modifier.padding(8.dp)` – Can be applied to individual elements inside containers
- `Modifier.padding(start = 12.dp)` – Directional padding (start/end/top/bottom)

#### **Arrangement** (For Row/Column - controls spacing on main axis)

![[image-461.png]]

- `Arrangement.Start` – Aligns items to the start
- `Arrangement.Center` – Centers items
- `Arrangement.End` – Aligns items to the end
- `Arrangement.SpaceBetween` – Distributes space between items
- `Arrangement.SpaceAround` – Distributes space around items
- `Arrangement.SpaceEvenly` – Distributes space evenly

#### **Alignment** (For Row/Column - controls cross-axis alignment)

![[image-462.png]]

- `Alignment.CenterHorizontally` – Centers children horizontally (in Column)
- `Alignment.CenterVertically` – Centers children vertically (in Row)
- `Alignment.Top` – Aligns to top
- `Alignment.Bottom` – Aligns to bottom
- `Alignment.Center` – Centers content (in Box)
- `Alignment.TopEnd` – Positions at top-end corner (in Box)

![[image-465.png]]

#### **Weight** (Space distribution)

![[image-464.png]]

- `Modifier.weight(1f)` – Takes up proportion of available space (e.g., 1/3)
- `Modifier.weight(2f)` – Takes up double the space of weight(1f) (e.g., 2/3)

#### **Visual Styling**

- `Modifier.background(Color.Blue)` – Sets background color
- `Modifier.background(Color.Blue, CircleShape)` – Background with specific shape
- `Modifier.background(Color.LightGray)` – Light gray background

#### **Layout-Specific Parameters**

- `verticalArrangement = Arrangement.Center` – For Column (vertical spacing)
- `horizontalAlignment = Alignment.CenterHorizontally` – For Column (horizontal positioning)
- `horizontalArrangement = Arrangement.SpaceEvenly` – For Row (horizontal spacing)
- `verticalAlignment = Alignment.CenterVertically` – For Row (vertical positioning)
- `contentAlignment = Alignment.Center` – For Box (positioning of stacked children)


in kotlin, components can be used multiple times

![[image-456.png]]

## stateful components

to make a composable component stateful we use the following syntax

**`var compteur by remember { mutableStateOf(0) }`**

- **`compteur`** is the variable that will determine the state of the component
- **`by remember`** keyword used to specify a stateful variable
- **`mutableStateOf(0)`** determines the starting value of the variable, in this case 0

whenever the value of that variable changes, the composable component will automatically detect it and update the ui of the component
### Examples

![[image-458.png]]
![[image-459.png]]

### Shared states

a state can be passed  as a parameter to an another component, and when the value of the passed parameter changes it will also update that component UI

```kotlin
@Composable
fun Ecran() {
    var compteur by remember { mutableStateOf(0) }    // the parent owns the state
    Affichage(compteur)                               // value goes DOWN
    Bouton(onClick = { compteur++ })                  // event comes UP
}
 
@Composable
fun Affichage(valeur: Int) {
    Text("Valeur : $valeur")
}
 
@Composable
fun Bouton(onClick: () -> Unit) {
    Button(onClick = onClick) { Text("+1") }
}
```

### State list

sometimes a single state variable is not enough, which is why we can use a statelist to store multiple values

```kotlin
val commandes = remember { mutableStateListOf<String>() }
Button(
onClick = {
 commandes.add("Pizza ${commandes.size + 1}") 
 }) {
  Text("Ajouter") 
  }
commandes.forEach { Text(it) }
```

## Communication between activities with intent

![[image-469.png]]

Android apps are made of **Activities** (screens). An **Intent** is the message used to start another Activity, with or without data.

Activity A ── Intent (action + data URI + extras) ──► Activity B

 
|**Intent type**|**How it works**|
|---|---|
|**Explicit**|You **name the class** of the Activity to open (inside your own app).|
|**Implicit**|You **describe an action**; Android chooses the app (call, share, open a web page...).|

### Explicit intent

#### sending explicit intent without parameters/variables

```kotlin
val context = this@MainActivity
val intent = Intent(context, SecondActivity::class.java)
context.startActivity(intent)
```

**Parameters:**

- `context`: The current Activity context (`this@MainActivity`)
- `SecondActivity::class.java`: The target Activity class reference
- `startActivity(intent)`: Method to launch the Activity

#### with parameters

```kotlin
val context = this@MainActivity
val intent = Intent(context, ProfileActivity::class.java)
intent.putExtra("nom", "Rayan")
intent.putExtra("age", 22)
context.startActivity(intent)
```

**Parameters:**

`putExtra(key: String, value: Any)`: Adds data to the intent
- `key`: String identifier for the data
- `value`: The data (String, Int, Boolean, Parcelable, etc.)


#### receiving the intent

```kotlin
class ProfileActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        val nom = intent.getStringExtra("nom") ?: "Inconnu"
        val age = intent.getIntExtra("age", 0)
        setContent {
            ProfileScreen(nom, age)
        }
    }
}
```

**Parameters:**

- `intent.getStringExtra(key)`: Retrieves String data (returns null if not found, use `?:` for default)
- `intent.getIntExtra(key, defaultValue)`: Retrieves Int data with default value

### implicit intent

implicit intent are defined by their actions, they dont rely on other pages to execute their actions

| Action         | Constant               | Data (URI)                 | Key Extras                                    | setType()      | Use Case               |
| -------------- | ---------------------- | -------------------------- | --------------------------------------------- | -------------- | ---------------------- |
| **View URL**   | `Intent.ACTION_VIEW`   | `Uri.parse("https://...")` | None                                          | None           | Open browser           |
| **Dial Phone** | `Intent.ACTION_DIAL`   | `Uri.parse("tel:...")`     | None                                          | None           | Open phone number dial |
| **Send Email** | `Intent.ACTION_SENDTO` | `Uri.parse("mailto:...")`  | `Intent.EXTRA_SUBJECT`<br>`Intent.EXTRA_TEXT` | None           | Send email             |
| **Share Text** | `Intent.ACTION_SEND`   | None                       | `Intent.EXTRA_TEXT`                           | `"text/plain"` | Share to any app       |
| **Open Map**   | `Intent.ACTION_VIEW`   | `Uri.parse("geo:...")`     | None                                          | None           | Show location          |

```kotlin
// View URL
Intent(Intent.ACTION_VIEW, Uri.parse("https://android.com"))

// Dial
Intent(Intent.ACTION_DIAL, Uri.parse("tel:0612345678"))

// Email
Intent(Intent.ACTION_SENDTO, Uri.parse("mailto:a@b.fr"))
    .putExtra(Intent.EXTRA_SUBJECT, "Subject")

// Share Text
Intent(Intent.ACTION_SEND)
    .putExtra(Intent.EXTRA_TEXT, "Hello")
    .setType("text/plain")

// Map Location
Intent(Intent.ACTION_VIEW, Uri.parse("geo:48.85,2.35"))
```

#### sending implicit intent

```kotlin
val context = this@MainActivity
val intent = Intent(Intent.ACTION_VIEW, Uri.parse("https://www.android.com"))
context.startActivity(intent)
```

**Parameters:**

- `Intent.ACTION_VIEW`: The action constant (view the data)
- `Uri.parse(url)`: Parses the URL string into a Uri object

# XML views

## The files of a project

|**File / folder**|**Role**|
|---|---|
|res/layout/activity_main.xml|the **design** of the screen (widgets)|
|MainActivity.kt|the **logic** of the screen (Activity)|
|res/menu/*.xml|menus|
|res/values/strings.xml|texts (@string/name), also string-array|
|res/drawable, res/mipmap|images and icons|
|AndroidManifest.xml|declares activities, permissions, the launcher screen|
|R class (generated)|gives access to resources: R.layout.x, R.id.x, R.string.x|

### The three steps of every Activity

```kotlin
class MainActivity : AppCompatActivity() {
 
    lateinit var btnAffich: Button                          // 1) declare the widgets
 
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)              // 2) load the XML layout
 
        btnAffich = findViewById(R.id.btnAffich)            // 3) find the widgets by id
        btnAffich.setOnClickListener {                      //    ... and attach actions
            Toast.makeText(this, "Clicked", Toast.LENGTH_SHORT).show()
        }
    }
}
```

## components


### 1. LinearLayout
Container that arranges children in a single direction (vertical or horizontal).

**Key Attributes:**
- `android:orientation` (`vertical`/`horizontal`): Direction of child arrangement
- `android:layout_width`, `android:layout_height` (`match_parent`/`wrap_content`/dimension): Size of the layout
- `android:gravity`: Alignment of children within the layout
- `android:layout_weight` (on children): Proportional space distribution
- `android:id` (`@+id/name`): Unique identifier

**MainActivity Manipulation:**
```kotlin
val layout = findViewById<LinearLayout>(R.id.myLayout)
layout.orientation = LinearLayout.HORIZONTAL  // Change orientation
layout.setBackgroundColor(Color.RED)            // Change background
val child = layout.getChildAt(0)                // Access children
```

---

### 2. TextView
Displays text to the user.

**Key Attributes:**
- `android:text` (`@string/name` or literal): Text content
- `android:textSize` (`24sp`): Font size
- `android:textColor` (`#RRGGBB` or `@color/name`): Text color
- `android:textStyle` (`bold`/`italic`/`normal`): Font style
- `android:gravity` (`center`/`left`/`right`): Text alignment within the view
- `android:layout_width`, `android:layout_height`: Size
- `android:id` (`@+id/name`): Unique identifier

**MainActivity Manipulation:**
```kotlin
val textView = findViewById<TextView>(R.id.myText)
textView.text = "Nouveau texte"           // Change text
textView.setTextColor(Color.BLUE)         // Change color
textView.textSize = 20f                   // Change size (float)
textView.visibility = View.GONE           // Hide (VISIBLE/INVISIBLE/GONE)
```

---

### 3. EditText
Text input field for user entry.

**Key Attributes:**
- `android:hint` (`@string/name`): Placeholder text when empty
- `android:inputType` (`text`/`textPassword`/`number`/`phone`/`textEmailAddress`): Keyboard type and behavior
- `android:text` (`@string/name` or literal): Initial text content
- `android:textSize`, `android:textColor`: Styling
- `android:layout_width`, `android:layout_height`: Size
- `android:id` (`@+id/name`): Unique identifier

**MainActivity Manipulation:**
```kotlin
val editText = findViewById<EditText>(R.id.myEdit)
val text = editText.text.toString()       // Get text as String
editText.setText("Nouveau contenu")     // Set text
editText.hint = "Nouvel indice"          // Change hint
editText.inputType = InputType.TYPE_CLASS_NUMBER  // Change input type
editText.isEnabled = false               // Disable editing
```

---

### 4. Button
Clickable button that performs an action.

**Key Attributes:**
- `android:text` (`@string/name`): Button label
- `android:onClick` (`methodName`): Method to call when clicked (must be public void with View parameter)
- `android:background` (`@color/name` or drawable): Background color/image
- `android:textColor`, `android:textSize`: Text styling
- `android:layout_width`, `android:layout_height`: Size
- `android:id` (`@+id/name`): Unique identifier

**MainActivity Manipulation:**
```kotlin
val button = findViewById<Button>(R.id.myButton)
button.setOnClickListener {
    Toast.makeText(this, "Cliqué!", Toast.LENGTH_SHORT).show()
}
fun myMethod(view: View) { /* action */ }
button.isEnabled = false  // Disable button
```

---

### 5. ImageView
Displays an image resource.

**Key Attributes:**
- `android:src` (`@drawable/image_name`): Image resource to display
- `android:scaleType` (`centerCrop`/`fitCenter`/`center`): How to scale the image
- `android:contentDescription` (`@string/name`): Accessibility description
- `android:layout_width`, `android:layout_height`: Size
- `android:id` (`@+id/name`): Unique identifier

**MainActivity Manipulation:**
```kotlin
val imageView = findViewById<ImageView>(R.id.myImage)
imageView.setImageResource(R.drawable.new_image)  // Change image
imageView.scaleType = ImageView.ScaleType.CENTER_CROP  // Change scaling
imageView.visibility = View.INVISIBLE               // Hide but keep space
```

---

### 6. CheckBox
Binary selection component (checked/unchecked).

**Key Attributes:**
- `android:text` (`@string/name`): Label next to checkbox
- `android:checked` (`true`/`false`): Initial checked state
- `android:layout_width`, `android:layout_height`: Size
- `android:id` (`@+id/name`): Unique identifier

**MainActivity Manipulation:**
```kotlin
val checkBox = findViewById<CheckBox>(R.id.myCheck)
val isChecked = checkBox.isChecked        // Get state
checkBox.isChecked = true                 // Set state programmatically
checkBox.setOnCheckedChangeListener { _, isChecked ->
    // Action when state changes
}
```

---

### 7. RadioGroup & RadioButton
Single selection from multiple options.

**RadioGroup Attributes:**
- `android:orientation` (`vertical`/`horizontal`): Arrangement of radio buttons
- `android:checkedButton` (`@id/radioButtonId`): Initially selected button
- `android:id` (`@+id/name`): Unique identifier

**RadioButton Attributes:**
- `android:text` (`@string/name`): Label text
- `android:checked` (`true`/`false`): Initial state
- `android:id` (`@+id/name`): Unique identifier

**MainActivity Manipulation:**
```kotlin
val radioGroup = findViewById<RadioGroup>(R.id.myRadioGroup)
val selectedId = radioGroup.checkedRadioButtonId  // Get selected ID (-1 if none)
val radioButton = findViewById<RadioButton>(selectedId)
val text = radioButton.text.toString()

radioGroup.setOnCheckedChangeListener { _, checkedId ->
    val selected = findViewById<RadioButton>(checkedId)
}
radioGroup.check(R.id.option1)  // Programmatic selection
```

---

### 8. Spinner
Dropdown list for selecting one item from a list.

**Key Attributes:**
- `android:entries` (`@array/array_name`): Array resource to populate spinner
- `android:prompt` (`@string/name`): Title of selection dialog
- `android:layout_width`, `android:layout_height`: Size
- `android:id` (`@+id/name`): Unique identifier

**MainActivity Manipulation:**
```kotlin
val spinner = findViewById<Spinner>(R.id.mySpinner)
val adapter = ArrayAdapter.createFromResource(
    this,
    R.array.my_array,
    android.R.layout.simple_spinner_item
)
adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item)
spinner.adapter = adapter

val selected = spinner.selectedItem.toString()

spinner.onItemSelectedListener = object : AdapterView.OnItemSelectedListener {
    override fun onItemSelected(parent: AdapterView<*>?, view: View?, position: Int, id: Long) {
        val item = parent?.getItemAtPosition(position).toString()
    }
    override fun onNothingSelected(parent: AdapterView<*>?) {}
}
```

---

### 9. ListView
Scrollable list of items.

**Key Attributes:**
- `android:id` (`@+id/name`): Unique identifier
- `android:layout_width`, `android:layout_height`: Size (usually `match_parent` for height)
- `android:divider` (`@color/name` or drawable): Divider between items
- `android:dividerHeight` (`1dp`): Height of divider

**MainActivity Manipulation:**
```kotlin
val listView = findViewById<ListView>(R.id.myList)
val data = arrayOf("Item 1", "Item 2", "Item 3")
val adapter = ArrayAdapter(this, android.R.layout.simple_list_item_1, data)
listView.adapter = adapter

listView.setOnItemClickListener { _, _, position, _ ->
    val item = data[position]
    Toast.makeText(this, "Clicked: $item", Toast.LENGTH_SHORT).show()
}
```


---

### 11. WebView
Displays web content within the app.

**Key Attributes:**
- `android:id` (`@+id/name`): Unique identifier
- `android:layout_width`, `android:layout_height`: Size

**MainActivity Manipulation:**
```kotlin
val webView = findViewById<WebView>(R.id.myWebView)
webView.webViewClient = WebViewClient()
webView.loadUrl("https://www.google.com")
webView.settings.javaScriptEnabled = true

webView.webViewClient = object : WebViewClient() {
    override fun onPageFinished(view: WebView?, url: String?) {
        super.onPageFinished(view, url)
        // Page loaded
    }
}
```

---

### 12. ProgressBar
Shows loading progress.

**Key Attributes:**
- `android:style` (`?android:attr/progressBarStyleHorizontal`): Style type
- `android:max` (`100`): Maximum progress value
- `android:progress` (`50`): Current progress value
- `android:visibility` (`visible`/`invisible`/`gone`): Visibility state
- `android:id` (`@+id/name`): Unique identifier

**MainActivity Manipulation:**
```kotlin
val progressBar = findViewById<ProgressBar>(R.id.myProgress)
progressBar.progress = 75           // Set current progress
progressBar.max = 200               // Set maximum
progressBar.visibility = View.GONE  // Hide when done
```

---

### 13. Toast (Not a View, but essential
Popup message that disappears automatically.

**Usage in MainActivity:**
```kotlin
Toast.makeText(this, "Message text", Toast.LENGTH_SHORT).show()
Toast.makeText(this, "Long message", Toast.LENGTH_LONG).show()

val toast = Toast.makeText(this, "Custom", Toast.LENGTH_SHORT)
toast.setGravity(Gravity.CENTER, 0, 0)
toast.show()
```

---

### 14. AlertDialog (Not a View, but essential
Modal dialog for alerts and choices.

**Usage in MainActivity:**
```kotlin
val builder = AlertDialog.Builder(this)
builder.setTitle("Error")
builder.setMessage("Les champs ne doivent pas être vide")
builder.setIcon(android.R.drawable.btn_dialog)
val dialog = builder.create()
dialog.show()
```

