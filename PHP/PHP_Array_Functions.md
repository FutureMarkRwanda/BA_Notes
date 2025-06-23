# PHP Array Functions

## Summary

This topic covers PHP array functions, which manipulate, inspect, and transform arrays. These functions enable tasks like searching, sorting, merging, and modifying arrays, enhancing data handling in PHP applications. Key functions include `in_array()`, `array_diff()`, `array_sum()`, `compact()`, and more, categorized by their purpose.

- **Searching and Checking Arrays**: Functions to find values, keys, or check existence (e.g., `in_array()`, `array_search()`, `array_key_exists()`).
- **Modifying Arrays**: Functions to add, remove, or replace elements (e.g., `array_push()`, `array_pop()`, `array_shift()`, `array_replace()`).
- **Sorting Arrays**: Functions to order arrays by value or key (e.g., `sort()`, `asort()`, `ksort()`, `arsort()`, `krsort()`).
- **Combining and Comparing Arrays**: Functions to merge or find differences/intersections (e.g., `array_merge()`, `array_diff()`, `array_intersect()`).
- **Inspecting Arrays**: Functions to view or compute array properties (e.g., `print_r()`, `var_dump()`, `sizeof()`, `array_sum()`, `array_product()`).
- **Navigating Arrays**: Functions to manage array pointers (e.g., `current()`, `next()`, `prev()`, `end()`, `reset()`, `each()`).
- **Miscellaneous Array Functions**: Other utilities like random selection, unique values, or value extraction (e.g., `array_rand()`, `array_unique()`, `array_values()`).

---

## Searching and Checking Arrays

These functions search arrays for values or keys, check existence, or return corresponding indices, useful for validation and data retrieval.

### In_Array

**Explanation**: The `in_array()` function checks if a value exists in an array, returning `TRUE` if found, `FALSE` otherwise. It’s case-sensitive for strings and accepts an optional type parameter for strict type checking.

**Example**: Check if car brands exist in an array.

**CODES**:
```php
<?php
$cars = ["benz", "bmw", "audi", "bugatti"];
if (in_array("Benzi", $cars)) {
    echo "Got Benzi<br>";
}
if (in_array("bmw", $cars)) {
    echo "Got bmw";
}
?>
```

**Output**: `Got bmw`

### Array_Search

**Explanation**: The `array_search()` function returns the key of a value in an array if found, or `FALSE` otherwise. It’s case-sensitive for strings.

**Example**: Find the key of a color in an array.

**CODES**:
```php
<?php
$colors = array("First-color" => "red", "Second-color" => "green", "Third-color" => "blue");
echo array_search("red", $colors);
?>
```

**Output**: `First-color`

### Array_Key_Exists

**Explanation**: The `array_key_exists()` function checks if a key or index exists in an array, returning `TRUE` if found, `FALSE` otherwise.

**Example**: Verify if a key exists in an array.

**CODES**:
```php
<?php
$search_array = array("first" => 1, "second" => 4);
if (array_key_exists("first", $search_array)) {
    echo "The 'first' element is in the array";
}
?>
```

**Output**: `The 'first' element is in the array`

**Scenario**: A web app uses `in_array()` to validate user input against allowed options and `array_search()` to retrieve a user’s ID from a name-keyed array.

---

## Modifying Arrays

These functions add, remove, or replace array elements, enabling dynamic array manipulation.

### Array_Push

**Explanation**: The `array_push()` function adds one or more elements to the end of an array, updating its length.

**Example**: Add fruits to an array.

**CODES**:
```php
<?php
$stack = array("orange", "banana");
array_push($stack, "apple", "raspberry");
print_r($stack);
?>
```

**Output**:
```
Array
(
    [0] => orange
    [1] => banana
    [2] => apple
    [3] => raspberry
)
```

### Array_Pop

**Explanation**: The `array_pop()` function removes and returns the last element of an array, shortening it by one.

**Example**: Remove the last fruit from an array.

**CODES**:
```php
<?php
$stack = array("orange", "banana", "apple", "raspberry");
$fruit = array_pop($stack);
print_r($stack);
echo "<br>Popped: $fruit";
?>
```

**Output**:
```
Array
(
    [0] => orange
    [1] => banana
    [2] => apple
)
Popped: raspberry
```

### Array_Shift

**Explanation**: The `array_shift()` function removes and returns the first element of an array, reindexing numeric keys and shortening the array.

**Example**: Remove the first fruit from an array.

**CODES**:
```php
<?php
$stack = array("orange", "banana", "apple", "raspberry");
$fruit = array_shift($stack);
print_r($stack);
echo "<br>Shifted: $fruit";
?>
```

**Output**:
```
Array
(
    [0] => banana
    [1] => apple
    [2] => raspberry
)
Shifted: orange
```

### Array_Replace

**Explanation**: The `array_replace()` function replaces values in the first array with values from subsequent arrays, preserving keys. For associative arrays, later arrays’ values overwrite earlier ones for matching keys.

**Example**: Replace colors in one array with another.

**CODES**:
```php
<?php
$a1 = array("a" => "red", "b" => "green");
$a2 = array("a" => "orange", "b" => "burgundy");
print_r(array_replace($a1, $a2));
?>
```

**Output**:
```
Array
(
    [a] => orange
    [b] => burgundy
)
```

### Array_Slice

**Explanation**: The `array_slice()` function extracts a portion of an array, starting at a specified position, with an optional length. A boolean `preserve_keys` parameter retains original keys if `TRUE`.

**Example**: Extract a single element from an array.

**CODES**:
```php
<?php
$array = [1, 2, 3, 4, 5, 6];
print_r(array_slice($array, 2, 1, true));
?>
```

**Output**:
```
Array
(
    [2] => 3
)
```

**Scenario**: A shopping cart app uses `array_push()` to add items, `array_pop()` to remove the last item, and `array_slice()` to display a subset of items.

---

## Sorting Arrays

These functions sort arrays by values or keys in ascending or descending order, useful for organizing data.

### Sort

**Explanation**: The `sort()` function sorts an indexed array in ascending order, reindexing numeric keys. It handles numbers numerically and strings alphabetically.

**Example**: Sort numbers in ascending order.

**CODES**:
```php
<?php
$arr = array(21, 19, 20, 16, 25);
sort($arr);
print_r($arr);
?>
```

**Output**:
```
Array
(
    [0] => 16
    [1] => 19
    [2] => 20
    [3] => 21
    [4] => 25
)
```

### Asort

**Explanation**: The `asort()` function sorts an associative array in ascending order by value, preserving keys.

**Example**: Sort ages by value.

**CODES**:
```php
<?php
$age = array("Gizo" => 11, "Saad" => 13, "Joe" => 23);
asort($age);
foreach ($age as $key => $value) {
    echo "Key=$key, Value=$value<br>";
}
?>
```

**Output**:
```
Key=Gizo, Value=11
Key=Saad, Value=13
Key=Joe, Value=23
```

### Arsort

**Explanation**: The `arsort()` function sorts an associative array in descending order by value, preserving keys.

**Example**: Sort ages in descending order.

**CODES**:
```php
<?php
$age = array("Peter" => "35", "Ben" => "37", "Joe" => "43");
arsort($age);
foreach ($age as $key => $value) {
    echo "Name: $key and Age: $value<br>";
}
?>
```

**Output**:
```
Name: Joe and Age: 43
Name: Ben and Age: 37
Name: Peter and Age: 35
```

### Ksort

**Explanation**: The `ksort()` function sorts an associative array in ascending order by key, preserving key-value pairs.

**Example**: Sort ages by key.

**CODES**:
```php
<?php
$age = array("Peter" => "35", "Ben" => "37", "Joe" => "43");
ksort($age);
foreach ($age as $key => $value) {
    echo "Key=$key, Value=$value<br>";
}
?>
```

**Output**:
```
Key=Ben, Value=37
Key=Joe, Value=43
Key=Peter, Value=35
```

### Krsort

**Explanation**: The `krsort()` function sorts an associative array in descending order by key, preserving key-value pairs.

**Example**: Sort ages in descending order by key.

**CODES**:
```php
<?php
$age = array("Peter" => "35", "Ben" => "37", "Joe" => "43");
krsort($age);
foreach ($age as $key => $value) {
    echo "Key=$key, Value=$value<br>";
}
?>
```

**Output**:
```
Key=Peter, Value=35
Key=Joe, Value=43
Key=Ben, Value=37
```

**Scenario**: A leaderboard app uses `sort()` for scores, `asort()` for user rankings by points, and `ksort()` for alphabetical user lists.

---

## Combining and Comparing Arrays

These functions merge arrays or find differences/intersections, useful for data aggregation and comparison.

### Array_Merge

**Explanation**: The `array_merge()` function combines two or more arrays, appending elements. For associative arrays, later arrays overwrite earlier ones for duplicate keys.

**Example**: Merge two arrays.

**CODES**:
```php
<?php
$array1 = array(2, 3, 4, 5, 6);
$array2 = array(2, 3, 4, 5, 6, "key" => "data");
$result = array_merge($array1, $array2);
print_r($result);
?>
```

**Output**:
```
Array
(
    [0] => 2
    [1] => 3
    [2] => 4
    [3] => 5
    [4] => 6
    [5] => 2
    [6] => 3
    [7] => 4
    [8] => 5
    [9] => 6
    [key] => data
)
```

### Array_Diff

**Explanation**: The `array_diff()` function returns elements in the first array not present in subsequent arrays, based on values.

**Example**: Find colors in one array not in another.

**CODES**:
```php
<?php
$array1 = array("a" => "green", "red", "blue", "red");
$array2 = array("b" => "green", "yellow", "red", "pink");
$result = array_diff($array1, $array2);
print_r($result);
?>
```

**Output**:
```
Array
(
    [1] => blue
)
```

### Array_Intersect

**Explanation**: The `array_intersect()` function returns an array of values common to all input arrays, preserving the first array’s keys.

**Example**: Find common colors in two arrays.

**CODES**:
```php
<?php
$array1 = array("red", "green", "blue");
$array2 = array("red", "black", "green");
print_r(array_intersect($array1, $array2));
?>
```

**Output**:
```
Array
(
    [0] => red
    [1] => green
)
```

**Scenario**: A data analysis tool uses `array_merge()` to combine datasets, `array_diff()` to identify unique entries, and `array_intersect()` to find shared values.

---

## Inspecting Arrays

These functions compute properties or display array contents, aiding debugging and data processing.

### Array_Sum

**Explanation**: The `array_sum()` function calculates the sum of numeric values in an array, supporting integers and floats.

**Example**: Sum values in two arrays.

**CODES**:
```php
<?php
$a = array(2, 4, 6, 8);
$b = array("a" => 1.2, "b" => 2.3, "c" => 3.4);
echo "Sum(a)= " . array_sum($a) . "<br>";
echo "Sum(b)= " . array_sum($b);
?>
```

**Output**:
```
Sum(a)= 20
Sum(b)= 6.9
```

### Array_Product

**Explanation**: The `array_product()` function calculates the product of numeric values in an array, returning 0 if strings are present.

**Example**: Compute products of arrays.

**CODES**:
```php
<?php
$products = array(12, 3, 4, 2);
echo array_product($products) . "<br>";
echo array_product(array(12, "ru", 4, 2));
?>
```

**Output**:
```
288
0
```

### Sizeof (Count)

**Explanation**: The `sizeof()` function (alias for `count()`) returns the number of elements in an array.

**Example**: Count elements in an array.

**CODES**:
```php
<?php
$score = array(12, 1, 45, 6, 7);
echo sizeof($score);
?>
```

**Output**: `5`

### Print_R

**Explanation**: The `print_r()` function displays human-readable array contents, useful for debugging. Use `<pre>` tags for formatted HTML output.

**Example**: Display an array’s structure.

**CODES**:
```php
<?php
$age = array("Peter" => "35", "Ben" => "37", "Joe" => "43");
echo "<pre>";
print_r($age);
echo "</pre>";
?>
```

**Output**:
```
Array
(
    [Peter] => 35
    [Ben] => 37
    [Joe] => 43
)
```

**Note**: `var_dump()` is covered in the **Arrays** topic and omitted here to avoid redundancy.

**Scenario**: A developer uses `array_sum()` for cart totals, `sizeof()` to check form input count, and `print_r()` to debug array data.

---

## Navigating Arrays

These functions manage the array’s internal pointer, accessing or moving to specific elements.

### Current

**Explanation**: The `current()` function returns the value of the current element, where the internal pointer resides, without moving the pointer.

**Example**: Access the current element.

**CODES**:
```php
<?php
$score = [1, 2, 3, 4];
echo current($score);
?>
```

**Output**: `1`

### Next

**Explanation**: The `next()` function advances the pointer and returns the next element’s value.

**Example**: Move to and access the next element.

**CODES**:
```php
<?php
$people = array("Peter", "Joe", "Glenn", "Cleveland");
echo current($people) . "<br>";
echo next($people);
?>
```

**Output**:
```
Peter
Joe
```

### Prev

**Explanation**: The `prev()` function rewinds the pointer and returns the previous element’s value.

**Example**: Move back to the previous element.

**CODES**:
```php
<?php
$people = array("Peter", "Joe", "Glenn", "Cleveland");
echo current($people) . "<br>";
echo next($people) . "<br>";
echo prev($people);
?>
```

**Output**:
```
Peter
Joe
Peter
```

### End

**Explanation**: The `end()` function moves the pointer to the last element and returns its value, or `FALSE` for an empty array.

**Example**: Access the last element.

**CODES**:
```php
<?php
$scores = [23, 44, 65, 33];
echo end($scores);
?>
```

**Output**: `33`

### Reset

**Explanation**: The `reset()` function moves the pointer to the first element and returns its value.

**Example**: Reset the pointer to the first element.

**CODES**:
```php
<?php
$provinces = ["Eastern", "Western", "Southern", "Northern", "Kigali City"];
echo current($provinces) . "<br>";
next($provinces);
echo current($provinces) . "<br>";
reset($provinces);
echo current($provinces);
?>
```

**Output**:
```
Eastern
Western