
# structures

## Grind pane

with grind pane you have to specify the position of each element inside it:

```java
<GridPane>

<Label text="Login" GridPane.rowIndex="0"
GridPane.columnIndex="0"></Label >

<TextField promptText="votre Login" GridPane.rowIndex="0"
GridPane.columnIndex="1" fx:id="tfLog"></TextField>

<Label text="Password" GridPane.rowIndex="1"
GridPane.columnIndex="0"></Label>

<PasswordField GridPane.rowIndex="1" GridPane.columnIndex="1"
fx:id="tfPass"></PasswordField>

<Button text="valider" GridPane.rowIndex="2" GridPane.columnIndex="0"
onAction="#authentification"></Button>

</GridPane>
```

## BorderPane

it divides the screen into :

- top and bottom
- left and right
- center

```java
<BorderPane xmlns="http://javafx.com/javafx" prefHeight="300" prefWidth="400">

 <top> 
<Label text="Top: Header or Menu Bar" /> 
</top> 

<left> 
<Label text="Left: Sidebar" /> 
</left>

 <center>
  <Label text="Center: Main Content Area" />
   </center> 
   
   <right> 
   <Label text="Right: Details or Ads" /> 
   </right> 
   
   <bottom> 
   <Label text="Bottom: Status Bar" /> 
   </bottom>
   
    </BorderPane>
```

# Sample fxml

## Label

```Java
<Label text="your name"></Label>
```

## TextField

**With placeholder (prompt text)**

```Java
<TextField fx:id="tfName" promptText="Enter your name here..."></TextField>
```

**With default text**

```java
<TextField fx:id="tfName" text="your text"></TextField>
```

## Button

```java
<Button text="Say hello!!" onAction="#sayHello"></Button>
```

- **onAction**: calls a method from the controller

## PasswordField

basically the same as TextField but for passwords

```java
<PasswordField fx:id="pfPassword" promptText="Enter your password" />
```

## radio

radio buttons but in javafx

```java
<fx:define>
    <ToggleGroup fx:id="myGroup" />
</fx:define>

<RadioButton text="Option A" toggleGroup="$myGroup" />
<RadioButton text="Option B" toggleGroup="$myGroup" />
```

- checkbox is exaclty  like radio buttons except that it doesnt use the toggle functionality

## ComboBox

ComboBox is basically a select option but in java fx

```java
<ComboBox fx:id="DepCombo" promptText="choisir"
onAction="#affichDep">
<items>
<FXCollections fx:factory="observableArrayList">

<String fx:value="TI" />
<String fx:value="AA" />
<String fx:value="GE" />
</FXCollections>
</items>
</ComboBox>
```

- we are not limited to **String** we can provide any class we want

## ListView

displays items inside a list

```java
<ListView fx:id="lvCouse">
<items>
<FXCollections fx:factory="observableArrayList">
<String fx:value="Pain" />
<String fx:value="Fromage" />
<String fx:value="Lait" />
</FXCollections>
</items>

</ListView>
```

- just like ComboBox we are not limited to strings to only string

## Table view

is used to display objects inside a table

```java
<TableView fx:id="personTable" prefWidth="380">  
<columns>  
  
<TableColumn text="First Name" prefWidth="130">  
<cellValueFactory>  
<PropertyValueFactory property="firstName" />  
</cellValueFactory>  
</TableColumn>  
  
<TableColumn text="Last Name" prefWidth="130">  
<cellValueFactory>  
<PropertyValueFactory property="lastName" />  
</cellValueFactory>  
</TableColumn>  
  
<TableColumn text="Age" prefWidth="100">  
<cellValueFactory>  
<PropertyValueFactory property="age" />  
</cellValueFactory>  
</TableColumn>  
  
</columns>  
</TableView>
```

- **`TableView`** and **`columns`** are wrappers around the entire table
- **`TableColumn`** is a wrapped around each column where it defines the header text/title of the column
- **`cellValueFactory`** and **`PropertyValueFactory`** both define the object column that will be linked with the column, lets say that we have an object called person with an attribute called **FirstName** the `property="FirstName"` will look for the getters and setters for that attribute

### Important

remember to always add this line to this file, otherwise our tableview will not function properly
![[image-363.png]]

![[image-362.png]]
## ids

there are 2 types of id in fxml which are:

- css ids which is: **id="value"**
- controller id which is **fx:id="tfName"**

```java
<Button 
    fx:id="btnSave" 
    id="fancy-button" 
    text="Save" />
```

# Controller

## Basics

```java
public class SampleController {
@FXML
TextField tfName;
@FXML
Label lMessage;

public void sayHello() {
lMessage.setText("Hello "+tfName.getText());
}

}
```

- to access elements inside the controller:
	- **@FXML** annotation
	- specify the type of the element we are trying to  access alongside the fx:id name from the fxml file
- to execute methods:
	- create any method
	- add an onAction="#sayHello" attribute to the element that you want to execute the method

## basic methods

- **`setVisible(boolean)`**: Shows or hides the component.
- **`setDisable(boolean)`**: Greys out the component and prevents interaction.
- **`getText()`**: Returns the string currently in the field.
- **`setText(String)`**: Sets the content of the field.
- **`clear()`**: Wipes the content (a shortcut for `setText("")`).
- **`setPromptText(String)`**: Sets the placeholder hint text.
- **`setEditable(boolean)`**: Determines if the user can type in the box.

## radio button

- **`isSelected()`**: Returns `true` if the radio button is currently selected.
- **`setSelected(boolean)`**: Sets the selection state programmatically (`true` to select, `false` to deselect).

## ComboBox & ListView

- **`setItems(ObservableList<T> value)`**: Replaces the list.
	- **Example of ObservableList**:

```java
ObservableList<String>l=FXCollections.observableArrayList("banane","
pomme");
```

- **`getItems()`**: Returns the `ObservableList` to add/remove/clear items.
	- **`.add(item)`** Adds a single item to the end of the list.
	- **`.addAll(item1, item2, ...)`** Adds multiple items to the end of the list at once.
	- **`.remove(item)`** Removes a specific object from the list.
	- **`.remove(index)`** Removes the item at the specific numerical position.
	- **`.removeAll(collection)`** Removes all items that are present in the provided collection.
	- **`.clear()`** Removes every single item, effectively emptying the component.
	- **`.set(index, item)`** Replaces the item at the given index with a new one.
	- **`.get(index)`** Retrieves the item at the specific index (without selecting it).
	- **`.size()`** Returns the total count of items currently in the list.
	- **`.contains(item)`** Returns `true` if the item exists in the list.

- **`getSelectionModel()`** Returns the object responsible for handling item selection.
- **`getSelectionModel().getSelectedItem()`** Returns the currently selected object.
- **`getSelectionModel().getSelectedIndex()`** Returns the integer index of the selected item.
- **`getSelectionModel().select(item/index)`** selects a specific item.
- **`getSelectionModel().clearSelection()`** Removes any active selection.

## intializable

the method initialize executes when we first run the program (useful for intializating ListView and ComboBox)

```java
public class SampleController implements Initializable{

@Override
public void initialize(URL arg0, ResourceBundle arg1) {

LvCourse.setItems(l);

}

}
```



**test this in eclispse**

```java
@FXML 
private void initialize() { 
lvCouse.getItems().addAll("Pain", "Fromage", "Lait"); 
} 
```

## Alerts

**types of alerts**:

- **`INFORMATION`** Displaying general info (e.g., "Data saved successfully").
- **`WARNING`** Alerting the user to potential issues (e.g., "File will be overwritten").
- **`ERROR`** Showing that something failed (e.g., "Database connection lost").
- **`CONFIRMATION`** Asking for permission (e.g., "Are you sure you want to delete this?").
- **`NONE`** A blank alert with no default buttons or icons.

```java
Alert alert = new Alert(Alert.AlertType.INFORMATION);
alert.setTitle("Success");
alert.setHeaderText("Operation Complete");
alert.setContentText("The data has been saved successfully.");

alert.show();
```

# CSS

- **`-fx-background-color`**: Sets the background color of a container or component.
- **`-fx-text-fill`**: Changes the color of the text itself (equivalent to `color` in standard web CSS).
- **`-fx-font-weight`**: Sets the thickness of the font (e.g., making it `bold`).

**Border Styling**

- **`-fx-border-color`**: Sets the color of the border surrounding the component.
- **`-fx-border-width`**: Determines the thickness of the border (e.g., `5px` or `2.0`).
- **`-fx-border-radius`**: Rounds the corners of the border.
- **`-fx-border-style`**: Defines the type of line for the border (e.g., `solid inside`).
- **`-fx-border-insets`**: Adjusts the distance of the border from the actual edge of the region.

**Spacing & Interaction**

- **`-fx-padding`**: Adds internal space between the border of the component and its inner content.
- **`-fx-cursor`**: Changes the mouse pointer when hovering over an element (e.g., changing it to a `hand` pointer to indicate it is clickable).
- **`fx-spacing`**: The `-fx-spacing` property is exclusive to layout panes that arrange their children in a line, primarily **`VBox`** (vertical box) and **`HBox`** (horizontal box).it sets a **fixed pixel distance between the child nodes** inside that container. It does not add space before the first item or after the last item—only _between_ them.
- **`fx-hgap and fx-vgap`**: is the equivalent of spacing to the gridpane layout




