# Basic Syntax

```php
// Variable
$number = 10;

// String
$s = "   dollars   ";
echo 'This costs a lot of $s.'; // This costs a lot of $s.
echo "This costs a lot of $s."; // This costs a lot of dollars.

// strlen, trim
strlen($s);
strlen(trim($s));

// String to Upper/Lower/Captal Case
strtoupper($s);
strtolower($s);
ucfirst($s);

// For Loop
for ($index = 0; $index < 10; $index++) {
	echo $index;    
}

// Array
$bestFriends = array('Alex', 'Bob', 'Chair');

// Print out, printf
echo 'My first friend is ' . bestFriends[0];
$date = "2018/9/1";
printf("Today is %s", $date);

// Add Element to Array
$bestFriends[4] = 'Steve';

// Enhanced Loop of Array
foreach($bestFriends as $friend) {
    echo $friend;
}

// Map
$customer = array('Name' => $userName, 'Street' => $streetName, 'City' => cityName);

// Access Associated Array (i.e map)
$customer['Name'];

// Enhanced Loop for Map
foreach($customer as $key => $value) {
    echo $key . ' : ' . $value; // . means attaching
}

// 2-D Array
$customers = array(array('Derek', '123 Main Street'),
                  array('Sally', '124 Main Street'),
                  array('Bob', '125 Main Street'));

// For Loop for 2D Array
for ($row = 0; $row < 3; $row++) {
    for ($col = 0; $col < 2; $col++) {
        echo customers[$row][$col];
    }
    echo '</br>';
}

// Sorting
sort(yourArray); // in alphabetical order
sort(yourArray, SORT_NUMERIC); // in numeric order
sort(yourArray, SORT_STRING); // in string
asort(yourArray); // sort array with keys
ksort(yourArray); // sort array	by the key

// Function
function addNumbers($var1, $var2) {
    return $var1 + $var2;
}

// Invoke a Function
echo '3 + 2 = ' . addNumbers(3, 2);

// Import 'class'
import("another_file.php"); // only if you need some variables or functions
// vs.
require("another_file.php"); // if php cannot find another_file.php, then it will crash

// invoke the cross-php variable & function -- just directly call the variable or function name

// Super Globals - "arrays" that keep variable which can be accessed throughout ALL your applications
$GLOBALS ['user'] = 'user_name';

session_start(); // <-- need to start at the very beginning
$_SESSION['user_info'] = "Allen";

$_SERVER['PHP_SELF']; // keeps paths and headers

// $_FILES - is used to collect files from forms 

// Try and Catch Exceptions
try {
    throw new Exception("Some error occured");
} catch(Exception $errormsg) {
    echo $errormsg->getMessage(); 
}

// Connect to MySql
$connection = mysqli_connect($server, $username, $password, $database);

// Close Connection
mysqli_close($connection);

// Execute a Query
$run_query = mysqli_query($connection, $query);
$result = mysqli_fetch_assoc($run_query);

// Count Number of Rows 
$size = mysqli_num_rows($run_query);
```



## Validation and Sanitization

```php
$raw_email = trim($_GET['email']);
$clean_email = filter_var($raw_email, FILTER_VALDATE_EMAIL);
```

For more information, check [W3C](https://www.w3schools.com/php/php_ref_filter.asp). 



## Double Quote vs Single Quote

```php
// String
$s = "   dollars   ";
echo 'This costs a lot of $s.'; // This costs a lot of $s.
echo "This costs a lot of $s."; // This costs a lot of dollars.
```



#### reference

* [PHP Programming](https://youtu.be/7TF00hJI78Y) 