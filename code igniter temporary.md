# controllers

just like other mvc frameworks

## controller

just set up the controller with the following command and then write the methods for it

```bash
php spark make:controller ControllerName
```

```php
<?php

namespace App\Controllers;

class Blog extends BaseController
{
    // Accessible via: http://your-site.com/blog or http://your-site.com/blog/index
    public function index()
    {
        // 1. Prepare data to pass along
        $data = [
            'title' => 'My First CodeIgniter Blog',
            'posts' => ['Welcome to CI4', 'Understanding Controllers', 'Next Steps with Views']
        ];

        // 2. Load a View file (HTML layout) and hand it the data
        return view('blog_home', $data);
    }

    // Accessible via: http://your-site.com/blog/detail/42
    public function detail($id = null)
    {
        // $id automatically captures the URL segment "42"
        return "Displaying blog post #" . esc($id);
    }
}
```

## route

```php
use App\Controllers\Pages;
use App\Controllers\Blog;

// When visiting example.com/about -> Runs Pages::about()
$routes->get('about', [Pages::class, 'about']);

// When visiting example.com/contact -> Runs Pages::contact()
$routes->get('contact', 'Pages::contact'); // Alternative string syntax

// Matches example.com/products/42
$routes->get('products/(:num)', 'Products::detail/$1');
```

## view page

inside the view page remember to call the variable name inside the data array for it to work

```php
<!DOCTYPE html>  
<html lang="en">  
<head>  
<meta charset="UTF-8">  
<meta name="viewport" content="width=device-width, initial-scale=1.0">  
<title>Document</title>  
</head>  
<body>  
<p>if you are seeing this then this is the dashboard page :D</p>  
  
<h1>also here is the id : <?php echo($id) ?></h1>  
</body>  
</html>
```

# migrations

migrations allows us to define the structure of the database with all its tables and columns

```php
class CreateUsersTable extends Migration  
{  
public function up()  
{  
// 1. Define table columns  
$this->forge->addField([  
'id' => [  
'type' => 'INT',  
'constraint' => 11,  
'unsigned' => true,  
'auto_increment' => true,  
],  
'username' => [  
'type' => 'VARCHAR',  
'constraint' => '100',  
],  
'email' => [  
'type' => 'VARCHAR',  
'constraint' => '255',  
'unique' => true,  
],  
'created_at' => [  
'type' => 'DATETIME',  
'null' => true,  
],  
]);  
  
// 2. Set the primary key ('id')  
$this->forge->addKey('id', true);  
  
// 3. Create the table 'users' (creates if not exists)  
$this->forge->createTable('users');  
}  
  
public function down()  
{  
// Drop the table if we roll back this migration  
$this->forge->dropTable('users');  
}  
}
```

- up method is for creating the table and down is for handling rollbacks related to that table

## commands

```bash
php spark make:migration CreateUsersTable

php spark migrate

php spark migrate:rollback

php spark migrate:status
```

# Model

the model is used to define basic crud methods for tables and define their foreign keys

## basic model variables

here we will list the most basic variables for models, there are alot more to configure

```php
// table name and primary key and specify if auto increment is used  
protected $table = 'users';  
protected $primaryKey = 'id';  
protected $useAutoIncrement = true;  
  
// return type and soft delete(instead of actually deleting them we add a column called deleted_at)  
protected $returnType = 'array';  
protected $useSoftDeletes = false;  
  
//these 2 work together the allowed fields array is used to specify which fields can be updated or inserted into the database, and the boolean strips out any fields that are not in the allowed fields array when inserting or updating records.  
protected $protectFields = true;  
protected $allowedFields = ['username','email'];  
  
//specifies if insert statements with no data should be allowed, specifies if an update statement will only concern fields with changed values or all fields in the table  
protected bool $allowEmptyInserts = false;  
protected bool $updateOnlyChanged = true;  
  
//specifices if code igniter will automatically set the created_at, updated_at, and deleted_at fields when inserting, updating, or deleting records  
protected $useTimestamps = false;  
//specifices the date type and columns related to the table  
protected $dateFormat = 'datetime';  
protected $createdField = 'created_at';  
protected $updatedField = 'updated_at';  
protected $deletedField = 'deleted_at';

//specifices insert and update rules for fields and their error message
protected $validationRules = [
    'username' => 'required|min_length[3]|alpha_numeric',
    'email'    => 'required|valid_email|is_unique[users.email,id,{id}]',
];

protected $validationMessages = [
    'email' => [
        'required'  => 'Please enter your email address.',
        'is_unique' => 'An account with this email already exists.',
    ],
];

//determines whether to apply the validation rules or not
protected $skipValidation = false;
```


## model built in methods 

code igniter offers built it methods for using models inside a controller(or inside itself with the keyword $this) here are some examples of them

```php
namespace App\Controllers;

use App\Models\UserModel;

class UserController extends BaseController
{
    // ----------------------------------------------------
    // 1. CREATE (Insert Records)
    // ----------------------------------------------------
    public function create()
    {
        $userModel = new UserModel();

        // Using insert() -> Returns the newly created primary key ID
        $newUserId = $userModel->insert([
            'username' => 'alex_dev',
            'email'    => 'alex@example.com',
            'status'   => 'active',
        ]);

        // Alternative: Using save()
        // (save() automatically performs an INSERT if no primary key is provided)
        $userModel->save([
            'username' => 'sarah_m',
            'email'    => 'sarah@example.com',
            'status'   => 'pending',
        ]);
    }

    // ----------------------------------------------------
    // 2. READ (Query / Fetch Records)
    // ----------------------------------------------------
    public function read()
    {
        $userModel = new UserModel();

        // Fetch ALL users in the table
        $allUsers = $userModel->findAll();

        // Fetch a single user by primary key ID (e.g., ID = 5)
        $user = $userModel->find(5);

        // Fetch multiple specific IDs
        $users = $userModel->find([1, 2, 3]);

        // Filter results with where() conditions
        $activeUser  = $userModel->where('status', 'active')->first();   // Single record
        $activeUsers = $userModel->where('status', 'active')->findAll(); // Array of records
    }

    // ----------------------------------------------------
    // 3. UPDATE (Modify Records)
    // ----------------------------------------------------
    public function update($id = null)
    {
        $userModel = new UserModel();

        // Update user record by primary key ID
        $userModel->update($id, [
            'username' => 'alex_updated',
            'status'   => 'active',
        ]);

        // Alternative: Using save() with the primary key included
        // (save() automatically performs an UPDATE if the primary key is present)
        $userModel->save([
            'id'       => $id,
            'username' => 'alex_updated',
        ]);

        // Batch update with custom query conditions
        $userModel->where('status', 'pending')
                  ->set(['status' => 'active'])
                  ->update();
    }

    // ----------------------------------------------------
    // 4. DELETE (Remove Records)
    // ----------------------------------------------------
    public function delete($id = null)
    {
        $userModel = new UserModel();

        // Delete a single user by ID
        $userModel->delete($id);

        // Delete multiple users by array of IDs
        $userModel->delete([1, 2, 3]);

        // Delete records matching a condition
        $userModel->where('status', 'inactive')->delete();
    }
}
```

## custom query methods

there are 2 ways or creating custom query methods either by using the $this keyword or by using the $this->db keyword

### $this keyword

when our query can be handled by only built in CRUD methods then we only use the $this keyword

```php
public function getActiveUsersWithOrderCount(int $minOrders = 1): array  
{  
return $this->select('users.id, users.username, users.email, COUNT(orders.id) as total_orders')  
->join('orders', 'orders.user_id = users.id', 'inner')  
->where('users.status', 'active')  
->where('orders.status', 'completed')  
->groupBy('users.id')  
->having('total_orders >=', $minOrders)  
->orderBy('total_orders', 'DESC')  
->findAll();  
}
```

### $this->db

when working with complex queries we add the ->db->query extension to it so we can use regular sql queries to commmunicate with the db

```php
public function getTopSpenders(string $startDate, string $endDate, int $limit = 10): array
{
    $sql = "SELECT users.id, users.username, SUM(payments.amount) as total_spent
            FROM users
            JOIN payments ON payments.user_id = users.id
            WHERE payments.created_at BETWEEN ? AND ?
              AND payments.status = ?
            GROUP BY users.id
            ORDER BY total_spent DESC
            LIMIT ?";

    $query = $this->db->query($sql, [$startDate, $endDate, 'completed', $limit]);

    return $query->getResultArray();
}
```

when working with other tables we can the ->db->table to access them and use queries on them

```php
public function getUserSummary(int $userId): ?array
{
    $user = $this->find($userId);
    if (! $user) {
        return null;
    }
    $loginCount = $this->db->table('user_logins')
                           ->where('user_id', $userId)
                           ->countAllResults();

    $user['total_logins'] = $loginCount;
    return $user;
}
```

## command

here is the command to create a model

```bash
php spark make:model UserModel
```

to generate data with the seeder we will be using the fake library to generate fake data 

```php
public function run()  
{  
// 1. Initialize Faker instance  
$faker = Factory::create();  
  
// 2. Loop to create 10 Users  
for ($i = 0; $i < 10; $i++) {  
$userData = [  
'username' => $faker->userName(),  
'email' => $faker->unique()->safeEmail(),  
];  
  
$this->db->table('users')->insert($userData);  
}  
  
}
```

## command

```bash
php spark db:seed UserSeeder
```

# filters

filters is a middleware used to intercept http request before and after they reach they designated controllers

```php
<?php

namespace App\Filters;

use CodeIgniter\Filters\FilterInterface;
use CodeIgniter\HTTP\RequestInterface;
use CodeIgniter\HTTP\ResponseInterface;

class AuthFilter implements FilterInterface
{
    /**
     * Executes BEFORE the controller method is called.
     * Returning a Response object stops the controller from executing.
     */
    public function before(RequestInterface $request, $arguments = null)
    {
        if (! session()->get('isLoggedIn')) {
            return redirect()->to('/login')->with('error', 'You must be logged in.');
        }
    }

    /**
     * Executes AFTER the controller method has finished running.
     * Allows you to modify the outgoing response object.
     */
    public function after(RequestInterface $request, ResponseInterface $response, $arguments = null)
    {
        // Example: Add a custom security header to all outgoing responses
        $response->setHeader('X-Frame-Options', 'SAMEORIGIN');
    }
}
```

## parameters

the before method accepts 2 method but the after methods accepts 3, they both share 2 paramenters in common

  
**1. `$request` (`CodeIgniter\HTTP\RequestInterface`)**  
  
* **Available in:** `before()` and `after()`  
* **What it is:** An instance of the current incoming HTTP request object.  
* **What you use it for:** Inspecting incoming client data, request metadata, or URI paths.  
* **Common Methods:**  
* `$request->getMethod()` – Returns `GET`, `POST`, `PUT`, etc.  
* `$request->getIPAddress()` – Returns the client's IP.  
* `$request->getGet()` / `$request->getPost()` – Retrieves query or form parameters.  
* `$request->getHeaderLine('User-Agent')` – Reads specific HTTP request headers.  
  
  
**2. `$response` (`CodeIgniter\HTTP\ResponseInterface`)**  
  
* **Available in:** `after()` **only**  
* **What it is:** The HTTP response object generated after your Controller method finishes executing.  
* **What you use it for:** Modifying or logging the output before it is sent back to the user's browser.  
* **Common Methods:**  
* `$response->setHeader('Cache-Control', 'no-cache')` – Adds or overrides HTTP headers. 
* `$response->setStatusCode(403)` – Changes the outgoing HTTP status code.  
* `$response->getBody()` / `$response->setBody($newContent)` – Reads or manipulates the rendered HTML/JSON output.  
  
  
**3. `$arguments` (`array|null`)**  
  
* **Available in:** `before()` and `after()`  
* **What it is:** An indexed array of custom string parameters passed directly from your route configuration.  
* **How it works:** You append parameters after a colon `:` separated by commas in `app/Config/Routes.php`.  
  
```php  
// In app/Config/Routes.php  
// Passes 'admin' and 'manager' into the filter's $arguments parameter  
$routes->get('dashboard', 'AdminController::index', ['filter' => 'role:admin,manager']);  
  
```  

## command

```bash
php spark make:filter AuthFilter
```
# routes

Routes specify the HTTP verb (`get`, `post`, `put`, `delete`, `patch`), the URI pattern, and the handler (`Controller: :method` or closure).

```php
// Standard Controller Mapping  
$routes->get('about', 'Home::about');  
$routes->post('contact/submit', 'ContactController::submit');  
$routes->put('user/update', 'UserController::update');  
$routes->delete('user/delete', 'UserController::destroy');  

  
// Match multiple HTTP verbs for a single URI  
$routes->match(['get', 'post'], 'profile/edit', 'ProfileController::edit');
```


## routes with parameters

```php
// (:num) - Matches numbers only
$routes->get('users/(:num)', 'UserController::show/$1');

// (:segment) - Matches any string single URI segment (no slashes)
$routes->get('posts/(:segment)', 'PostController::view/$1');

// (:any) - Matches all remaining segments including slashes
$routes->get('gallery/(:any)', 'GalleryController::view/$1');

// (:alphanumeric) - Matches letters and numbers only
$routes->get('product/(:alphanumeric)', 'ProductController::detail/$1');
```

## routes with groupes

```php
$routes->group('admin', static function ($routes) {
    // Generates: GET /admin/dashboard -> AdminController::dashboard
    $routes->get('dashboard', 'AdminController::dashboard');
    
    // Generates: GET /admin/users -> AdminController::users
    $routes->get('users', 'AdminController::users');
});
```

# Helpers

helpers are used to store useful global functions that will be used inside of controllers

```php
<?php

if (! function_exists('format_currency')) {
    /**
     * Formats a numeric value as currency.
     */
    function format_currency(float $amount, string $symbol = '$'): string
    {
        return $symbol . number_format($amount, 2);
    }
}

if (! function_exists('render_status_badge')) {
    /**
     * Generates a Bootstrap HTML status badge.
     */
    function render_status_badge(string $status): string
    {
        $class = match (strtolower($status)) {
            'active', 'completed' => 'bg-success',
            'pending'             => 'bg-warning',
            default               => 'bg-danger',
        };

        return '<span class="badge ' . $class . '">' . ucfirst($status) . '</span>';
    }
}
```

## calling the helper inside the controller

we basically declare a variable called $helpers and provide it with an array of strings that contain the name of the file without the `_helper`, afterwards CodeIgniter will search for those methods inside our helper files

```php
namespace App\Controllers;

class OrderController extends BaseController
{
    // Load custom format_helper along with the built-in url helper
    protected $helpers = ['format', 'url'];

    public function show(int $id)
    {
        $orderTotal  = 129.50;
        $orderStatus = 'completed';

        // Call helper functions directly without instantiated objects
        $data = [
            'formattedPrice' => format_currency($orderTotal),       // Returns: "$129.50"
            'statusBadge'    => render_status_badge($orderStatus),  // Returns: "<span class="badge bg-success">Completed</span>"
        ];

        return view('orders/show', $data);
    }
}
```

## Note

to load the helper function to the controller its name must end with `_helper`

# Languages

with languages we can our page show difference text languages depending on the language selected

the way this work is that we have difference language folders with each containing files for differnet translations

```text
app/Language/
├── en/
│   └── Messages.php
└── fr/
    └── Messages.php
```

 and inside each of those files we fill the array with objects and their translations

```php
<?php

return [
    // Simple text translation
    'welcome'     => 'Welcome to our website',
    'login_button' => 'Log In',
    
    // Dynamic text using placeholders
    'greeting'    => 'Hello, {name}! You have {count} unread notifications.',

    // Nested array to group related text (like navigation)
    'nav' => [
        'home'    => 'Home',
        'about'   => 'About Us',
        'contact' => 'Contact Support',
    ],
];

>
```

## using the language feature in controllers and views

to use the feature we need to use the built in method `lang()`

**for views**

```php
<!-- 1. Simple Key Translation -->
<h1><?= lang('Messages.welcome') ?></h1>
<!-- Outputs (EN): <h1>Welcome to our website</h1> -->


<!-- 2. Nested Keys (using dot notation for arrays) -->
<nav>
    <a href="/"><?= lang('Messages.nav.home') ?></a>
    <a href="/about"><?= lang('Messages.nav.about') ?></a>
</nav>
<!-- Outputs (EN): <a href="/">Home</a> -->


<!-- 3. Dynamic Placeholders (Pass associative array as 2nd argument) -->
<p><?= lang('Messages.greeting', ['name' => 'Sarah', 'count' => 5]) ?></p>
<!-- Outputs (EN): Hello, Sarah! You have 5 unread notifications. -->


<!-- 4. Explicit Language Override (Pass locale as 3rd argument) -->
<button><?= lang('Messages.login_button', [], 'fr') ?></button>
<!-- Forces French output: <button>Se connecter</button> -->
```

**for controllers**

```php
namespace App\Controllers;

class UserController extends BaseController
{
    public function dashboard()
    {

        $data = [
            'pageTitle' => lang('Messages.welcome'),
        ];

        return view('user/dashboard', $data);
    }
}
```


## changing languages

**here are the steps to change  a language when the user clicks on a button**

- register all created language in the `App/Config/App.php` file
- The user clicks **Français** (`/lang/fr`).
- `LanguageController` saves `'lang' => 'fr'` in the session and redirects back to the user's previous URL.
- `LanguageFilter` intercepts the request, reads `'fr'` from the session, and executes `$request->setLocale('fr')`.
- All subsequent `lang('FileName.key')` calls render French translations until changed again.

### step 1 

fine the file located at `App/Config/App.php` and change the following variables to this 

```php
//self explanatory
public string $defaultLocale = 'en';
//determine from browser settings the default language to select
public bool $negotiateLocale = true;
//lists all supported languages
public array $supportedLocales = ['en'];
```



### Step 2

step up buttons that connect to a custom language controller to handle language change

```php
<div class="language-switcher">
    <a href="<?= site_url('lang/en') ?>" class="btn">English</a>
    <a href="<?= site_url('lang/fr') ?>" class="btn">Français</a>
    <a href="<?= site_url('lang/es') ?>" class="btn">Español</a>
</div>
```


### Step 3

configure a route and link it to the language controller

```php
$routes->get('lang/(:segment)', 'LanguageController::switch/$1');
```
### Step 4

configure a controller to save the language save in the user session

```php
namespace App\Controllers;

class LanguageController extends BaseController
{
    public function switch(string $locale = 'en')
    {
        $session = session();
        $config  = config('App');

        // Check if the requested language is supported
        if (in_array($locale, $config->supportedLocales, true)) {
            $session->set('lang', $locale);
        }

        // Redirect back to the previous page
        return redirect()->back();
    }
}
```

### Step 5

after saving the language parameter in the user session, we need to use the filter to change the local language to selected language

first we need to save the filter as a global filter so it automatically execute on every controller call to do that we need to go `app/Config/Filters.php`

```php
public array $aliases = [
    'languageFilter' => \App\Filters\LanguageFilter::class,
];

public array $globals = [
    'before' => [
        'languageFilter', // Runs on EVERY request before Controllers execute
    ],
    'after' => [],
];
```

```php
namespace App\Filters;

use CodeIgniter\Filters\FilterInterface;
use CodeIgniter\HTTP\RequestInterface;
use CodeIgniter\HTTP\ResponseInterface;

class LanguageFilter implements FilterInterface
{
    public function before(RequestInterface $request, $arguments = null)
    {
        $session = session();

        // If a language preference exists in session, apply it to the request
        if ($session->has('lang')) {
            $request->setLocale($session->get('lang'));
        }
    }

    public function after(RequestInterface $request, ResponseInterface $response, $arguments = null)
    {
        // No action needed after execution
    }
}
```

# Libraries

libraries are just like helpers except that they are used to register objects instead of procedual functions

```php
class Employer  
{  
private string $name;  
private string $email;  
private int $phoneNumber;  
static private float $taxRate = 0.15; // 15% tax rate  
  
public function __construct(String $name, string $email, int $phoneNumber)  
{  
$this->name = $name;  
$this->email = $email;  
$this->phoneNumber = $phoneNumber;  
}  
  
public function sayHello(): string  
{  
return "Hello, my name is {$this->name}. You can reach me at {$this->email} or call me at {$this->phoneNumber}.";  
}  
  
//getters and setters  
  
public function setName(string $name): void  
{  
$this->name = $name;  
}  
  
public function setEmail(string $email): void  
{  
$this->email = $email;  
}
```

## creating a new object inside of controllers

```php
use App\Libraries\Employer;

$name = $this->request->getPost('name');  
$email = $this->request->getPost('email');  
$phoneNumber = $this->request->getPost('phone');  
  
// Create a new Employer object  
$employer = new Employer($name, $email, (int)$phoneNumber);
```

# Entities

instead of working with database rows as array we can instead use entities which are basically objects that hold information about a specific row and useful functions

```php
<?php  
  
namespace App\Entities;  
  
use CodeIgniter\Entity\Entity;  
  
class User extends Entity  
{  
//specifices the dates and the datatype of the attributes  
protected $dates = ['created_at'];  
protected $casts = ['id' => 'integer', 'username' => 'string', 'email' => 'string'];  
  
public function getEmailDomain(): string  
{  
$emailParts = explode('@', $this->attributes['email']);  
return $emailParts[1] ?? '';  
}  
  
}
```

## linking entities with their prespective model

entities get their information from models which means that we need to specify that models will return entities instead of arrays

```php
protected $returnType = User::class;
```

## example of using entities in controllers

```php
<?php  
  
namespace App\Controllers;  
  
use App\Controllers\BaseController;  
use CodeIgniter\HTTP\ResponseInterface;  
use App\Models\UserModel;  
  
class UserController extends BaseController  
{  
public function index()  
{  
$userModel = new UserModel();  
$data = [  
'users' => $userModel->findAll()  
];  
  
return $this->renderView('UserDisplay', $data);  
}  
}
```
# views with templates

to render template inside a controller we use the render method, to add template to them we have to go the BaseController file in the controller folder and then make the render method extend the footer and the header templates

```php
protected function renderView(string $viewName, array $data = []): string  
{  
return view('templates/header', $data)  
. view($viewName, $data)  
. view('templates/footer', $data);  
}
```

# Events

events work in 2 steps:

- defining the method of the event
- and triggering the event

inside of `app/Config/Events.php` we register an event method 

```php
Events::on('employee_created', static function ($employee) {  
log_message('info', 'Employee created: ' . $employee->name);  
});
```

- the events consists of the event name to trigger it and the method to be executed with parameters

## triggering the event

to trigger the event just write this inside a controller

```php
Events::trigger('employee_created', $employer);
```

## built in triggers

code igniter offers 3 built in triggers which are the followings

- **`pre_system` (Start of Request):** Fires at the very beginning of **every single HTTP request** (each page reload, link click, or API call), before routing or controllers even exist. 
- **`post_controller_constructor` (Before Method Runs):** Fires after the controller class is created, but **right before** your targeted controller method (like `index()`, `create()`, or `save()`) executes.
- **`post_system` (End of Request):** Fires at the very end, **after** your controller method finishes, views are rendered, and the final HTML/data is delivered to the browser.

with these all you have to do is define their methods in the config file, you dont have to manually trigger them


## basic unit testing

the main idea of unit testing is that u want to make sure that your methods do execute exactly  how you want them to without inconsistencies which is why we create tests to see their output when given difference paramters

**test file**

```php
<?php  
  
namespace Tests;  
  
use App\Controllers\CalculatorController;  
use CodeIgniter\CLI\CLI;  
use CodeIgniter\Test\CIUnitTestCase;  
  
class CalculatorTest extends CIUnitTestCase  
{  
protected function setUp(): void  
{  
parent::setUp();  
}  
  
public function testExample(): void  
{  
$calculator = new CalculatorController();  
$result = $calculator->multiply(2, 3);  
  
// The 3rd parameter is the error message printed IF the assertion fails  
$this->assertEquals(6, $result, "Calculation failed: expected 6, but got {$result}");  
  
CLI::write("1st Test passed: 2 * 3 = 6", 'green');  
}  
}
```

## built in testing methods

these are just the basic test methods

| **Method Signature**                                 | **Purpose**                                                                   |
| ---------------------------------------------------- | ----------------------------------------------------------------------------- |
| `assertEquals($expected, $actual)`                   | Asserts loose equality between expected and actual values.                    |
| `assertSame($expected, $actual)`                     | Asserts strict equality , checking both value and data type.                  |
| `assertTrue($condition)` / `assertFalse($condition)` | Asserts that a boolean condition evaluates strictly to `true` or `false`.     |
| `assertNull($actual)` / `assertNotNull($actual)`     | Asserts that a variable is `null` or not `null`.                              |
| `assertCount($expectedCount, $array)`                | Asserts the total number of items in an array or `Countable` object.          |
| `assertInstanceOf($expectedClass, $object)`          | Asserts that an object is an instance of a specific class/interface.          |
| `assertArrayHasKey($key, $array)`                    | Asserts that an array contains a specific array key.                          |
| `assertStringContainsString($needle, $haystack)`     | Asserts that a substring exists within a target string.                       |
| `assertEmpty($actual)` / `assertNotEmpty($actual)`   | Asserts that a variable, string, or array is empty or not empty.              |
| `expectException($exceptionClass)`                   | Asserts that the subsequent code execution throws a specific Exception class. |

## command

**to create a new test**

```bash
php spark make:test CalculatorTest
```

**to execute the test**

```bash
vendor/bin/phpunit tests/CalculatorTest.php
```

-  to execute all tests just emit the test file path