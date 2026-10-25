this is the file responsible for directing the user to a specific page after entering a url like /products 

# Basic routing

this routing will just connect the user to a specific without checking if he is connected or not

```Php
use Illuminate\Support\Facades\Route;
use App\Http\Controllers\ProductController;
use Inertia\Inertia;

Route::get('/products', [ProductController::class, 'index'])->name('products.index');
```

- we are using the **GET** method to access the page
- this route gets triggered when the user visits */products*
- it immediately calls the controller responsible for this page which is *ProductController* and the function responsible for loading the page which is **function index()** 
- **OPTIONAL** we can provide a route with a name

## The controller

for this routing to  work we need a controller that loads the page in this example the controller is called **ProductController** and lets assume that from this controller we want to load all of the members of the page

```PHP
use App\Models\Member;  
use Inertia\Inertia;  
  
class ProductController extends Controller  
{  
public function index(){  
$members = Member::all();  
  
// Render the Vue page located at resources/js/Pages/Products/Index.vue  
return Inertia::render('Products/Index', [  
'members' => $members  
]);  
}  
}
```

- this controller contains the index function that is called by the router
- it creates an attribute called *members* which contains the info of all the members from the modal (*database*) with the method **::all()***
- this render method provided by **Inertia** asks for 2 informations which are:
	- the following package that contains the vue page:
		- **Inside a folder called *Products***
		- **The file MUST be called *Index***
	- a list of variables to send as *props*

## Vue page

the vue page will receive the variable **members** as props and display it inside the page

```JS
<script setup>  
// This prop 'products' comes directly from the Controller we just wrote  
const props = defineProps({  
members: Array  
});  
  
const showMembers = () =>{  
console.log(props.members);  
}  
</script>
```

