# Fire (NoSQL Query Language)

Fire is a Domain Specific Language (DSL), designed for making queries to NoSQL databases such as Firebase Firestore. Drawing inspiration from Rust, Python, Julia, JavaScript, Dart, and MongoDB Shell, Fire simplifies querying by introducing an easy-to-code syntax that is meant to feel intuitive to software engineers.

## Table of Contents

1. [Installation](#installation)
2. [Data types](#data-types)
3. [Variable declaration](#variable-declaration)
4. [Querying](#querying)
5. [Conditional query](#conditional-query)
6. [Updating](#updating)
7. [Creating](#creating)
8. [Removing](#removing)
9. [Filtering with multiple conditions](#filtering-with-multiple-conditions)
10. [Ordering results](#ordering-results)
11. [If statement](#if-statement)
12. [Iteration](#iteration)
14. [See statement](#see-statement)
15. [Function declaration](#function-declaration)
16. [Predefined functions](#predefined-functions)
17. [Math](#math)
18. [Contributing](#contributing)
19. [License](#license)

## Installation

[Instructions for installing and setting up Fire.]

## Syntax

### Data Types

Fire supports several fundamental data types:

```typescript
data_type = {
    num: 'number',
    str: 'string',
    bool: 'boolean',
    list: 'list / array',
    map: 'map / JSON',
    any: 'dynamic',
    time: 'timestamp',
    db: 'database object'
};
```

### Variable Declaration

Variables in Fire are declared by specifying the variable name, followed by a colon, the type, and an optional initial value.

```typescript
let $population = 123123123; // number type
let $country = 'USA'; // string type
let $xis_active = true; // boolean type
let $cities = []; // list type
let $capital_coordinates = {}; // map type
let $current_date = Time.now(); // time type
let $countryiesCollection = countries; // this is a database object, which can be either a collection, doc, or a field.
```

### Querying

Fire queries are simple and straightforward.

```typescript
// Fetches all documents in a collection.
collect(countries);

// Fetches all the fields in the Japan document. 
collect(countries).doc(Japan); 

// Fetches specific documents from the countries collection by their ids.
collect(countries).doc([Japan, USA, UK]);

// Fetches specific fields of certain documents from the countries collection by their ids.
collect(countries).doc([Japan, USA, UK]).field([population, region]);
```

### Conditional Query

Filter documents based on conditions with Fire. Apply conditions to specific fields in the documents.

```typescript
collect(countries).doc(USA).field(gender_ratio).but(gender_ratio >= 1.2) ?? 0; 
// Selects the gender_ratio field in the USA document where the gender_ratio field is greater than or equal to 1.2
// , but if the field value is null `0` will be returned.

collect(countries).but((population >= 1_000_000 and continent == 'Asia') or region == 'East Asia'); 
// Selects all documents where the 'population' field is greater than or equal to 1,000,000 
// and continent field is equal to 'Asia', or meanwhile if the region field is equal to 'East Asia'.
// but method takes in a SQL-like syntax.
```

### Updating

Update the fields in a document with Fire easily.

```typescript
collect(countries).doc(Japan).set({phone:81}); // Updates the phone field in the 'Japan' document to 81.
collect(countries).set({is_active:true}); // Update a field in all docs
collect(countries).field(is_active).set(false); // Update a field in all docs
collect(countries).doc(Japan).field(population).set(1_000_000); // Update a specific field in a doc of a collection.
```

### Creating

```typescript
let $new_country = {phone: 386, population: 1000};
collect(countries).add({id: 'Kingdom of Apple', data: $new_country}); // with a predefined id
collect(countries).add($new_country); // with an auto-generated id
```

### Deleting

```typescript
collect(countries).delete(); // Delete an entire collection
collect(countries).doc(USA).delete(); // Delete a doc of a collection
collect(countries).doc(USA).field(population).delete(); // Delete a specific field in a certain doc of a collection
```

### Ordering results

```typescript
collect(countries).ascend(population);
collect(countries).descend(population);
collect(countries).first(5);
collect(countries).last(5);
```

## Control flow statements

Fire also supports essential control flow statements like `if`, `for`, `while`, and `see` to provide more flexibility and control over your operations.

### If statement

The `if` statement in Fire can be used to execute a block of code only if a specified condition is true.

```typescript
let $x = 10;
if ($x > 5) {
  log('x is greater than 5');
} else {
  log('incorrect')
}

if ($x > 5) => log('x is greater than 5');
else => log('incorrect');
```

### Iteration

```typescript
let $fruits = ['Banana', 'Apple', 'Orange'];

// Iterate over the indexes of fruits and log them.
$fruits.index($i) => log($i);

// Iterate over the elements of fruits and log them.
$fruits.each($fruit) => log($fruit);
```

### See Statement

The `see` statement is used to select one of many code blocks to be executed. It works similar to Match in Rust and Switch in JavaScript.

```typescript
let $x = 'banana';
$x = see($x) => {
    123: sum(1, $x);
    456: abs($x) - 1;
    'what': 'omg';
    default: null;
}; 
```

### Function Declaration

Functions in Fire are declared using the `fn` keyword, followed by the function name, parameters, return type, and the function body enclosed in curly braces `{}`. 

For example, a function to add two numbers would look like this:

```typescript
fn add(a, b) => return a + b;
```

```typescript
fn add(a, b) {
  let $result = sum(a, b);  
  return $result;
}
```

## Predefined Functions

### Sum

The `sum()` function is used to calculate the sum of all numbers in a given list.

Example:

```typescript
let $numbers = [1, 2, 3, 4, 5];
let $total = sum($numbers);  // total will be 15
```

### Length

The `len()` function is used to get the length of a given list or string.

Example:

```typescript
let $name = 'Fire';
let $length = len($name);  // length will be 4
```

### Average

The `avg()` function is used to calculate the average of all numbers in a given list.

Example:

```typescript
let $numbers = [1, 2, 3, 4, 5];
let $average = avg($numbers);  // average will be 3
```

### Absolute

The `abs()` function is used to get the absolute value of a number.

Example:

```typescript
let $negativeNumber = -10;
let $absolute = abs($negativeNumber);  // absolute will be 10
```

### Integer

The `int()` function is used to convert a value into an integer.

Example:

```typescript
let $number = 3.14;
let $integer = int($number);  // integer will be 3
```

### Number

The `num()` function is used to convert a value into a number.

Example:

```typescript
let $string = '3.14';
let $number = num($string);  // integer will be 3.14
```

### String

The `str()` function is used to convert a value into a string.

Example:

```typescript
let $number = 123;
let $string = str($number);  // string will be '123'
```

### Max

The `max()` function is used to get the maximum value in a list of numbers.

Example:

```typescript
let $numbers = [1, 2, 3, 4, 5];
let $maximum = max($numbers);  // maximum will be 5
```

### Min

The `min()` function is used to get the minimum value in a list of numbers.

Example:

```typescript
let $numbers = [1, 2, 3, 4, 5];
let $minimum = min($numbers);  // minimum will be 1
```

### Med

The `med()` function is used to get the median value in a list of numbers.

Example:

```typescript
let $numbers = [-1, 12, 30, 49, 105];
let $median = med($numbers);  // median will be 30
```

### Round

The `round()` function is used to round off a floating-point number to its nearest integer.

Example:

```typescript
let $number = 3.14;
let $rounded_number = round($number, -1);  // roundedNumber will be 3.1
```

### Type

The `type()` function is used to get the data type of a value.

Example:

```typescript
let $name = 'Fire';
let $type = type($name);  // typeOfName will be 'str'
```

### Pi
```typescript
log(pi(3)); // fetch the three digits of pi, which is 3.141
```

### Rename
```typescript
collect(countries).rename('nations');
collect(countries).doc(UK).rename('United Kingdom');
collect(countries).doc(USA).field(nation_code).rename('country_number');
```

### Duplicate 
```typescript
collect(countries).duplicate('countries_2');
collect(countries).doc(UK).duplicate('Canada');
collect(countries).doc(USA).field(nation_code).duplicate('telephone_number');
```

### Move
```typescript
collect(countries).doc(UK).moveTo('internations');
collect(countries).doc(USA).field(nation_code).moveTo(Asia, 'India');
```

### Merge
```typescript
collect(countries).merge(nations); //this merges all documents in the `nations` collection, remove `nations` collection.
```

### Copy
```typescript
collect(countries).copy('nations'); //this copies all documents in the `nations` collection, but the `nations` collection remains.
```

## Math
```typescript
    //addition
    let $x = 7 + 4;
    
    //subtraction
    let $x = 6 - 2
    
    //mutiplication
    let $x = 3 * 2
    
    //division
    let $x = 3 / 4
    
    //base
    let $x = $x^5
 ```
## Contributing

This is a new project. Feel free to file a pull request.

## License
MIT License



# Not Yet Implementated
1. count()
2. increment() & decrement() a field
3. enumerate() collections, docs, and fields
4. Conditional update or delete or create
