# Rabbit Form Helpers #

Rabbit Forms come with a helper file that provides little helper functions, this page describes these functions.

| **Function** | **Description** |
|:-------------|:----------------|
| array rabbit\_array\_merge(array $array1, array $array2) | Recursive array merge function, if the array keys conflict, the second argument array will has precedence |
| array rabbit\_filter\_fields(string $table, array $data) | This function get the fields of table in first argument, and use this to filter elements of array passed in second argument, this results in array containing only valid field names that passed into second argument |
| array rabbit\_filter\_db\_data(string $table, array $data) | This function work as above, but this function filter a associative array data and maintains only valid rows |
| string rabbit\_attributes\_build(array $data) | This function helper you to build a html attributes list, you give one associative array containing attributes data and this method returns a string containing html attributes |
| string rabbit\_json\_encode(mixed $data) | Create a JSON notation based on data passed |
| string rabbit\_pathinfo($path[, $options]) | Get information about path (this method works like php **pathinfo** but supports filename for php versions before 5.2) |