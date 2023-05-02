# Fire Query Language

Fire is a Domain Specific Language (DSL), designed for making queries to NoSQL databases such as Firebase Firestore. Drawing inspiration from Python, TypeScript and Dart, Fire simplifies querying by introducing an easy-to-learn syntax that is meant to feel intuitive to software engineers.

## Table of Contents

1. [Installation](#installation)
2. [Data Types](#data-types)
3. [Variable Declaration](#variable-declaration)
4. [Querying](#querying)
5. [Conditional Query](#conditional-query)
6. [Updating](#updating)
7. [Creating a new document](#creating-a-new-document)
8. [Filtering with multiple conditions](#filtering-with-multiple-conditions)
9. [Ordering results](#ordering-results)
10. [If statement](#if-statement)
11. [For loop](#for-loop)
12. [While Loop](#While-Loop)
13. [Switch statement](#switch-statement)
14. [Function Declaration](#function-declaration)
15. [Error Handling](#error-handling)
16. [Contributing](#contributing)
17. [License](#license)

## Installation

[Instructions for installing and setting up Fire.]

## Syntax

### Data Types

Fire supports several fundamental data types:

```fire
// Numbers (both integers and floats)
exampleNum: num = 123.45;

// String and character data
exampleStr: str = 'Hello, Fire!';

// Boolean values
exampleBool: bool = true;

// Lists (arrays) of values
exampleList: list<num> = [1, 2, 3, 4, 5];

// Maps (dictionaries or objects) of key-value pairs
exampleMap: map<str, num> = {'one': 1, 'two': 2, 'three': 3};

// Dynamic type
exampleAny: any = 'I can be anything!';
```

### Variable Declaration

Variables in Fire are declared by specifying the variable name, followed by a colon, the type, and an optional initial value.

```fire
x: str = '123'; // variable x is assigned the string value of '123'
```

### Querying

Fire queries are simple and straightforward. Use the `collect` function followed by the `doc` function to fetch a document from a collection.

```fire
x: map<str, any> = collect('countries').doc('Japan'); // Fetches all the fields in the 'Japan' document.
```

### Conditional Query

Filter documents based on conditions with Fire. Apply conditions to specific fields in the documents.

```fire
x: list<map<str, any>> = collect('countries').field('phone') >= 12 ?? null; // Selects all documents where the 'phone' field is greater than or equal to 12.
```

### Updating

Update the fields in a document with Fire easily.

```fire
collect('countries').doc('Japan').update({'phone':81}); // Updates the 'phone' field in the 'Japan' document to 81.
```

### Creating a new document

```fire
newCountry: map<str, any> = {'name': 'New Country', 'population': 1000};
collect('countries').add(newCountry);
```

### Filtering with multiple conditions

```fire
x: list<map<str, any>> = collect('countries').where(('population') > 1000000 && ('continent') == 'Asia');
```

### Ordering results

```fire
x: list<map<str, any>> = collect('countries').order('population', descending: true).limit(10);
```

## Control flow statements

Fire also supports essential control flow statements like `if`, `for`, `while`, and `switch` to provide more flexibility and control over your operations.

### If statement

The `if` statement in Fire can be used to execute a block of code only if a specified condition is true.

```fire
x: num = 10;
if (x > 5) {
  print('x is greater than 5');
}
```

### For Loop

`for` loop in Fire allows you to execute a block of code a number of times.

```fire
for (i:num from 0 to 5) {
  print(i);
}
```

Fire's additional `for` loop syntax makes looping over lists a breeze.

```fire
x: fruits<str> = ['Banana', 'Apple', 'Orange'];

// Iterate over the indexes of fruits and print them.
for(i: num in fruits){
   print(i);
}

// Iterate over the elements of fruits and print them.
for(fruit: str of fruits){
    print(fruit);
}
```


These `for` loop examples demonstrate how Fire makes it easy to work with lists, providing intuitive syntax for both index-based and element-based iterations.

### While Loop

`while` loop can be used to execute a block of code as long as a specified condition is true.

```fire
i: num = 0;
while (i < 5) {
  print(i);
  i += 1;
}
```

### Switch Statement

The `switch` statement is used to select one of many code blocks to be executed.

```fire
x: str = 'banana';
switch (x) {
  case 'apple':
    print('Apple is $1');
    break;
  case 'banana':
    print('Banana is $2');
    break;
  default:
    print('Unknown fruit');
}
```
Please note that these are the basic syntax examples. Depending on the exact capabilities and features of Fire, there might be variations and additional options available.

### Function Declaration

Functions in Fire are declared using the `fn` keyword, followed by the function name, parameters, return type, and the function body enclosed in curly braces `{}`. 

Here is the general syntax:

```fire
fn function_name(parameter: type, ...) -> return_type {
    // Function body
}
```

For example, a function to add two numbers would look like this:

```fire
fn add(a: num, b: num) -> num {
    return a + b;
}
```

### Error Handling

Error handling in Fire is done using the `throw` and `try-catch` statements. 

- The `throw` statement is used to raise an exception.
- The `try-catch` block is used to catch and handle exceptions.

Here is an example of a function that throws an exception if the denominator is zero:

```fire
fn divide(numerator: num, denominator: num) -> num {
    if (denominator == 0) {
        throw Exception('Denominator cannot be zero');
    } else {
        return numerator / denominator;
    }
}
```

To catch and handle this exception, you would use a `try-catch` block:

```fire
try {
    var result = divide(10, 0);
} catch(e) {
    print(e);
}
```

In this example, if an exception is thrown in the `try` block, the control is passed to the `catch` block, where the exception is handled by printing the error message.

## Contributing

[Information about how to contribute to the project.]

## License

[License information.]



