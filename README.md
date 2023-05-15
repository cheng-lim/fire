# Fire (NoSQL Query Language)

Fire is a Domain Specific Language (DSL), designed for making queries to NoSQL databases such as Firebase Firestore. Drawing inspiration from Rust, Python, Julia, JavaScript, Dart, and MongoDB Shell, Fire simplifies querying by introducing an easy-to-code syntax that is meant to feel intuitive to software engineers.

## Table of Contents

1. [Installation](#installation)
2. [Data types](#data-types)
3. [Variable declaration](#variable-declaration)
4. [Querying](#querying)
5. [Conditional query](#conditional-query)
6. [Updating](#updating)
7. [Creating a new document](#creating-a-new-document)
8. [Filtering with multiple conditions](#filtering-with-multiple-conditions)
9. [Ordering results](#ordering-results)
10. [If statement](#if-statement)
11. [For loop](#for-loop)
12. [While loop](#While-Loop)
13. [See statement](#see-statement)
14. [Function declaration](#function-declaration)
15. [Predefined functions](#predefined-functions)
16. [Math](#math)
17. [Contributing](#contributing)
18. [License](#license)

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
};
```

### Variable Declaration

Variables in Fire are declared by specifying the variable name, followed by a colon, the type, and an optional initial value.

```typescript
x = 123; // number type
x = '123'; // string type
x = true; // boolean type
x = []; // list type
x = {}; // map type
x = Time.now(); // time type
```

### Querying

Fire queries are simple and straightforward.

```typescript
collect('countries').doc('Japan'); // Fetches all the fields in the 'Japan' document. 
collect(countries).doc(Japan); // If the variables are not declared, they will be converted into strings like 'countries' and 'Japan'.
```

### Conditional Query

Filter documents based on conditions with Fire. Apply conditions to specific fields in the documents.

```typescript
collect('countries').doc('USA').field('gender_ratio').but('gender_ratio' >= 1.2) ?? 0; 
// Selects the 'gender_ratio' field in the 'USA' document where the 'gender_ratio' field is greater than or equal to 1.2
// , but if the field value is null `0` will be returned.

collect('countries').but(('population' >= 1,000,000 and 'continent' == 'Asia') or 'region' == 'East Asia'); 
// Selects all documents where the 'population' field is greater than or equal to 1,000,000 
// and 'continent' field is equal to 'Asia', or meanwhile if the 'region' field is equal to 'East Asia'.
// but method takes in a SQL-like syntax.
```

### Updating

Update the fields in a document with Fire easily.

```typescript
collect('countries').doc('Japan').set({'phone':81}); // Updates the 'phone' field in the 'Japan' document to 81.
collect('countries').set({'is_active':true}); // Update a field in all docs
```

### Creating a new collection and document

```typescript
new_country = {'phone': 386, 'population': 1000};
collect('countries').add({'id': 'Kingdom of Apple', 'data': new_country}); // with a predefined id
collect('countries').add(new_country); // with an auto-generated id
```

### Ordering results

```typescript
collect('countries').ascend('population');
collect('countries').descend('population').limit(10);
```

### Fetch multiple collections and documents
```typescript
collect(['countries', nations]); //this fetches and concates 2 collections.
```

## Control flow statements

Fire also supports essential control flow statements like `if`, `for`, `while`, and `see` to provide more flexibility and control over your operations.

### If statement

The `if` statement in Fire can be used to execute a block of code only if a specified condition is true.

```typescript
x = 10;
if (x > 5) {
  log('x is greater than 5');
} else {
  log('incorrect')
}

if (x > 5) => log('x is greater than 5');
else => log('incorrect');
```

### For Loop

`for` loop in Fire allows you to execute a block of code a number of times.

```typescript
for (i = 0 < 5) => log(i);
for (i = 10 > 5) => log(i);
```

Fire's additional `for` loop syntax makes looping over lists a breeze.

```typescript
fruits = ['Banana', 'Apple', 'Orange'];

// Iterate over the indexes of fruits and log them.
for(i in fruits) => log(i);

// Iterate over the elements of fruits and log them.
for(fruit of fruits) => log(fruit);
```


These `for` loop examples demonstrate how Fire makes it easy to work with lists, providing intuitive syntax for both index-based and element-based iterations.

### While Loop

`while` loop can be used to execute a block of code as long as a specified condition is true.

```typescript
while (i = 0 < 5) {
  log(i);
  i += 1;
}
while (i = 20 > 5) {
  log(i);
  i -= 1;
}
```

### See Statement

The `see` statement is used to select one of many code blocks to be executed.

```typescript
x = 'banana';
x = see(x) {
  'apple' => true;
  'banana' => false;
  else => null;
};
```
Please note that these are the basic syntax examples. Depending on the exact capabilities and features of Fire, there might be variations and additional options available.

### Function Declaration

Functions in Fire are declared using the `fn` keyword, followed by the function name, parameters, return type, and the function body enclosed in curly braces `{}`. 

For example, a function to add two numbers would look like this:

```typescript
fn add(a, b) => return a + b;
```

```typescript
fn add(a, b) {
  result = sum(a, b);  
  return result;
}
```

## Predefined Functions

### Sum

The `sum()` function is used to calculate the sum of all numbers in a given list.

Example:

```typescript
numbers = [1, 2, 3, 4, 5];
total = sum(numbers);  // total will be 15
```

### Length

The `len()` function is used to get the length of a given list or string.

Example:

```typescript
name = 'Fire';
length = len(name);  // length will be 4
```

### Average

The `avg()` function is used to calculate the average of all numbers in a given list.

Example:

```typescript
numbers = [1, 2, 3, 4, 5];
average = avg(numbers);  // average will be 3
```

### Absolute

The `abs()` function is used to get the absolute value of a number.

Example:

```typescript
negativeNumber = -10;
absolute = abs(negativeNumber);  // absolute will be 10
```

### Integer

The `int()` function is used to convert a value into an integer.

Example:

```typescript
number = 3.14;
integer = int(number);  // integer will be 3
```

### String

The `str()` function is used to convert a value into a string.

Example:

```typescript
number = 123;
string = str(number);  // string will be '123'
```

### Max

The `max()` function is used to get the maximum value in a list of numbers.

Example:

```typescript
numbers = [1, 2, 3, 4, 5];
maximum = max(numbers);  // maximum will be 5
```

### Min

The `min()` function is used to get the minimum value in a list of numbers.

Example:

```typescript
numbers = [1, 2, 3, 4, 5];
minimum = min(numbers);  // minimum will be 1
```

### Round

The `round()` function is used to round off a floating-point number to its nearest integer.

Example:

```typescript
number = 3.14;
rounded_number = round(number, -1);  // roundedNumber will be 3.1
```

### Type

The `type()` function is used to get the data type of a value.

Example:

```typescript
name = 'Fire';
type = type(name);  // typeOfName will be 'str'
```

### Pi
```typescript
pi(3) = 3.141 // fetch the three digits of pi
```

### Rename
```typescript
collect('countries').rename('nations');
collect('countries').doc('UK').rename('United Kingdom');
collect('countries').doc('USA').field('nation_code').rename('country_number');
```

### Duplicate 
```typescript
collect('countries').duplicate('countries_2');
collect('countries').doc('UK').duplicate('Canada');
collect('countries').doc('USA').field('nation_code').duplicate('telephone_number');
```

### Move
```typescript
collect('countries').doc('UK').moveTo('internations');
collect('countries').doc('USA').field('nation_code').moveTo('Asia', 'India');
```

### Merge
```typescript
collect('countries').merge('nations'); //this merges all documents in the `nations` collection, remove `nations` collection.
```

### Copy
```typescript
collect('countries').copy('nations'); //this copies all documents in the `nations` collection, but the `nations` collection remains.
```

## Math
```typescript
    //addition
    x = 7 + 4;
    
    //subtraction
    x = 6 - 2
    
    //mutiplication
    x = 3 * 2
    
    //division
    x = 3 / 4
    
    //base
    x = x^5
 ```
## Contributing

This is a new project. Feel free to file a pull request.

## License
MIT License



