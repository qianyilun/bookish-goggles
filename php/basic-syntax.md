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

// string to upper/lower/captal case
strtoupper($s);
strtolower($s);
ucfirst($s);

// Reference

// For loop
for ($index = 0; $index < 10; $index++) {
	echo $index;    
}

// Array
$bestFriends = array('Alex', 'Bob', 'Chair');

// Print out, printf
echo 'My first friend is ' . bestFriends[0];
$date = "2018/9/1";
printf("Today is %s", $date);

// Add element to array
$bestFriends[4] = 'Steve';

// Enhanced loop of array
foreach($bestFriends as $friend) {
    echo $friend;
}

// Map
$customer = array('Name' => $userName, 'Street' => $streetName, 'City' => cityName);

// Enhanced loop for map
foreach($customer as $key => $value) {
    echo $key . ' : ' . $value;
}

// 2-D array
$customers = array(array('Derek', '123 Main Street'),
                  array('Sally', '124 Main Street'),
                  array('Bob', '125 Main Street'));

// For loop for 2D array
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

echo '3 + 2 = ' . addNumbers(3, 2);

```

#### reference

* [PHP Programming](https://youtu.be/7TF00hJI78Y) 