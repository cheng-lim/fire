# Fire (NoSQL Query Language)

Fire is a Domain Specific Language (DSL), designed for making queries to NoSQL databases such as Firebase Firestore. Drawing inspiration from Rust, Python, TypeScript and Dart, Fire simplifies querying by introducing an easy-to-learn syntax that is meant to feel intuitive to software engineers.

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
13. [Switch statement](#switch-statement)
14. [Function declaration](#function-declaration)
15. [Sum](#sum)
16. [Length](#length)
17. [Average](#average)
18. [Absolute](#absolute)
19. [Integer](#integer)
20. [String](#string)
21. [Max](#max)
22. [Min](#min)
23. [Round](#round)
24. [Type](#type)
25. [Error handling](#error-handling)
26. [Contributing](#contributing)
27. [License](#license)

## Installation

[Instructions for installing and setting up Fire.]

## Syntax

### Data Types

Fire supports several fundamental data types:

```typescript
// Number (both integers and floats)
let x: num = 123.45;

// String
let x: str = 'Hello, Fire!';

// Boolean
let x: bool = true;

// List
let x: list<num> = [1, 2, 3, 4, 5];

// Map
let x: map<str, num> = {'one': 1, 'two': 2, 'three': 3};

// Dynamic
let x: any = 'I can be anything!';

// Time
let x: time = Time.now();
```

### Variable Declaration

Variables in Fire are declared by specifying the variable name, followed by a colon, the type, and an optional initial value.

```typescript
let x: str = '123'; // variable x is assigned the string value of '123'
```

### Querying

Fire queries are simple and straightforward. Use the `collect` function followed by the `doc` function to fetch a document from a collection.

```typescript
let x: map<str, any> = collect('countries').doc('Japan'); // Fetches all the fields in the 'Japan' document.
```

### Conditional Query

Filter documents based on conditions with Fire. Apply conditions to specific fields in the documents.

```typescript
let x: int = collect('countries').doc('USA').field('gender_ratio').but('gender_ratio' >= 1.2) ?? 0; // Selects the 'gender_ratio' field in the 'USA' document where the 'gender_ratio' field is greater than or equal to 1.2, but if the field value is null `0` will be returned.

let x: list<map<str, any>> = collect('countries').but(('population' >= 1,000,000 and 'continent' == 'Asia') or 'region' == 'East Asia'); // Selects all documents where the 'population' field is greater than or equal to 1,000,000 and 'continent' field is equal to 'Asia', or meanwhile if the 'region' field is equal to 'East Asia'.
```

### Updating

Update the fields in a document with Fire easily.

```typescript
collect('countries').doc('Japan').set({'phone':81}); // Updates the 'phone' field in the 'Japan' document to 81.
```

### Creating a new document

```typescript
let newCountry: map<str, any> = {'name': 'New Country', 'population': 1000};
collect('countries').add(newCountry);
```

### Ordering results

```typescript
let x: list<map<str, any>> = collect('countries').sort('population', method: Sort.descending).limit(10);
```

## Control flow statements

Fire also supports essential control flow statements like `if`, `for`, `while`, and `see` to provide more flexibility and control over your operations.

### If statement

The `if` statement in Fire can be used to execute a block of code only if a specified condition is true.

```typescript
let x: num = 10;
if (x > 5) {
  log('x is greater than 5');
}

if (x > 5) => log('x is greater than 5');
```

### For Loop

`for` loop in Fire allows you to execute a block of code a number of times.

```typescript
for (let i:num = 0 < 5) => log(i);
```

Fire's additional `for` loop syntax makes looping over lists a breeze.

```typescript
let fruits: list<str> = ['Banana', 'Apple', 'Orange'];

// Iterate over the indexes of fruits and log them.
for(let i: num in fruits) => log(i);

// Iterate over the elements of fruits and log them.
for(let fruit: str of fruits) => log(fruit);
```


These `for` loop examples demonstrate how Fire makes it easy to work with lists, providing intuitive syntax for both index-based and element-based iterations.

### While Loop

`while` loop can be used to execute a block of code as long as a specified condition is true.

```typescript
while (let i: num = 0 < 5) {
  log(i);
  i += 1;
}
```

### See Statement

The `see` statement is used to select one of many code blocks to be executed.

```typescript
let x: str = 'banana';
see (x) {
  case ('apple') => log('Apple is $1');
  case ('banana') => log('Banana is $2');
  log('Unknown fruit');
}
```
Please note that these are the basic syntax examples. Depending on the exact capabilities and features of Fire, there might be variations and additional options available.

### Function Declaration

Functions in Fire are declared using the `fn` keyword, followed by the function name, parameters, return type, and the function body enclosed in curly braces `{}`. 

For example, a function to add two numbers would look like this:

```typescript
fn add(a: num, b: num): num => return a + b;
```

```typescript
fn add(a: num, b: num): num {
  let result: num = sum(a+b);  
  return result;
}
```

## Predefined Functions

### Sum

The `sum()` function is used to calculate the sum of all numbers in a given list.

Example:

```typescript
let numbers: list<num> = [1, 2, 3, 4, 5];
let total: num = sum(numbers);  // total will be 15
```

### Length

The `len()` function is used to get the length of a given list or string.

Example:

```typescript
let name: str = 'Fire';
let length: num = len(name);  // length will be 4
```

### Average

The `avg()` function is used to calculate the average of all numbers in a given list.

Example:

```typescript
let numbers: list<num> = [1, 2, 3, 4, 5];
let average: num = avg(numbers);  // average will be 3
```

### Absolute

The `abs()` function is used to get the absolute value of a number.

Example:

```typescript
let negativeNumber: num = -10;
let absolute: num = abs(negativeNumber);  // absolute will be 10
```

### Integer

The `int()` function is used to convert a value into an integer.

Example:

```typescript
let number: num = 3.14;
let integer: num = int(number);  // integer will be 3
```

### String

The `str()` function is used to convert a value into a string.

Example:

```typescript
let number: num = 123;
let string: str = str(number);  // string will be '123'
```

### Max

The `max()` function is used to get the maximum value in a list of numbers.

Example:

```typescript
let numbers: list<num> = [1, 2, 3, 4, 5];
let maximum: num = max(numbers);  // maximum will be 5
```

### Min

The `min()` function is used to get the minimum value in a list of numbers.

Example:

```typescript
let numbers: list<num> = [1, 2, 3, 4, 5];
let minimum: num = min(numbers);  // minimum will be 1
```

### Round

The `round()` function is used to round off a floating-point number to its nearest integer.

Example:

```typescript
let number: num = 3.14;
let roundedNumber: num = round(number);  // roundedNumber will be 3
```

### Type

The `type()` function is used to get the data type of a value.

Example:

```typescript
let name: str = 'Fire';
let typeOfName: str = type(name);  // typeOfName will be 'str'
```

This documentation provides a basic understanding of predefined functions in Fire. For more detailed information, please refer to the official Fire documentation.

### Rename
```typescript
collect('countries').rename('nations');

collect('countries').doc('UK').rename('United Kingdom');

collect('countries').doc('USA').field('nation_code').rename('country_number');
```

### Duplicate 
```typescript
collect('countries').copyAs('countries_2');

collect('countries').doc('UK').copyAs('Canada');

collect('countries').doc('USA').field('nation_code').copyAs('telephone_number');
```

### Move
```typescript

collect('countries').doc('UK').moveTo('internations');

collect('countries').doc('USA').field('nation_code').moveTo('Asia', 'India');
```

## Error Handling

Error handling in Fire is done using the `throw` and `try-catch` statements. 

- The `throw` statement is used to raise an exception.
- The `try-catch` block is used to catch and handle exceptions.

Here is an example of a function that throws an exception if the denominator is zero:

```typescript
func divide(numerator: num, denominator: num): num {
    if (denominator == 0) => throw Exception('Denominator cannot be zero');
    else => return numerator / denominator;
}
```

To catch and handle this exception, you would use a `try-catch` block:

```typescript
try => let result:num = divide(10, 0);
catch(e) => log(e);
}
```

In this example, if an exception is thrown in the `try` block, the control is passed to the `catch` block, where the exception is handled by printing the error message.

## Contributing

[Information about how to contribute to the project.]

## License
MIT License



