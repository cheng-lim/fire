# Fire Query Language

Fire is a Domain Specific Language (DSL), designed for making queries to NoSQL databases such as Firebase Firestore. Drawing inspiration from TypeScript and Dart, Fire simplifies querying by introducing an easy-to-learn syntax that is meant to feel intuitive to software engineers.

## Table of Contents

1. [Installation](#installation)
2. [Data Types](#data-types)
3. [Variable Declaration](#variable-declaration)
4. [Querying](#querying)
5. [Conditional Query](#conditional-query)
6. [Updating](#updating)
7. [Contributing](#contributing)
8. [License](#license)

## Installation

[Instructions for installing and setting up Fire.]

## Data Types

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

## Variable Declaration

Variables in Fire are declared by specifying the variable name, followed by a colon, the type, and an optional initial value.

```fire
x: str = '123'; // variable x is assigned the string value of '123'
```

## Querying

Fire queries are simple and straightforward. Use the `collect` function followed by the `doc` function to fetch a document from a collection.

```fire
x: map<str, any> = collect('countries').doc('Japan'); // Fetches all the fields in the 'Japan' document.
```

## Conditional Query

Filter documents based on conditions with Fire. Apply conditions to specific fields in the documents.

```fire
x: list<map<str, any>> = collect('countries').field('phone') >= 12 ?? null; // Selects all documents where the 'phone' field is greater than or equal to 12.
```

## Updating

Update the fields in a document with Fire easily.

```fire
collect('countries').doc('Japan').update({'phone':81}); // Updates the 'phone' field in the 'Japan' document to 81.
```

## Additional Syntax Examples

### Filtering with multiple conditions

```fire
x: list<map<str, any>> = collect('countries').where(('population') > 1000000 && ('continent') == 'Asia');
```

### Ordering results

```fire
x: list<map<str, any>> = collect('countries').orderBy('population', descending: true).limit(10);
```

### Creating a new document

```fire
newCountry: map<str, any> = {'name': 'New Country', 'population': 1000};
collect('countries').add(newCountry);
```

## Contributing

[Information about how to contribute to the project.]

## License

[License information.]