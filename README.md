# TypescriptIDL

TypescriptIDL is subset of Typescript adapted to be an IDL.

## Using this document
Before reading this document there are a few things to note.

### Dynamics
Many Utf-8 characters are being used to describe different dynamics so make sure your reading device supports them, alternatively you might want to pick up a rendered version.

The corner brackets are used to describe a placeholder; the type of placeholder will be declared within the brackets:
```
『'PlaceholderType'』
```

Double-angle brackets are used to refer to `Optional`s, these aren't required for a definition to be valid.
This is not to be confused with `Optional<『Type』>` which is a type to describe a nullable.
```
《『PlaceholderType』》
```

Sometimes `...` is used within corner brackets, 

### Newlines vs Semi-colons
Typescript, like it's origin is a very flexible language, it allows you to omit semi-colons as seperators in most situations.
As an IDL TypescriptIDL is newline seperated by default, no semi-colons required. And, like typescript semi-colons are allowed if desired.

## Syntax

The syntax is similar to typescript's `.d.ts` files.

### Methods declaration
A method/function follows the Typescript syntax, but doesn't require a keyword (`function`).
```
『Identifier』(《『...Argument』》)《: 『Type』》
```
If no return-type is used it will be assumed void/undefined.

### FunctionType
FunctionTypes are special types the arguments/return-types are restricted.
To delcare a `FunctionType` is similar to a method declaration:
```
(《『...Argument』》) => 『Type』
```

Note that the return-type is required for FunctionTypes but not in Method/Function declarations.

### Arguments
Arugments follow:
```
『...《『Identifier』:》『Type』』
```

Arguments typically have an `Identifier` and `Type`, but Identifiers can be omitted if so desired.

An example of this:
```
Foo(bool, int): int
```

If the last argument is prefixed by `...` it has to be an `Array<『Type』>`; in implementation this will describe a variable number of parameters if `『Type』`.

An example of this:
```
Foo(arg0: bool, arg1: int, ...argN: Array<int>): int
```

When ommitting `Identifier`s:
```
Foo(bool, int, ...Array<int>): int
```

### Fields/Variables
Fields and other Variables can be defined as:
```
『Identifier』: 『Type』
```

### Classes
Classes can be defined as
```
class 『Identifier』{
  《constructor(『Arguments』): 『Type』》
  《『...Functions』》
  《『...Fields』》
}
```

### Struct
Structs can be defined as
```
struc 『Identifier』{
  《『...Fields』》
}
```

### Keywords
The position and syntax of keywords depend on which object it's applied to.
If it's part of the type a generic type:
`『Keyword』<『Type』>`

For example:
```
Volatile<Optional<int>>
```

### Type Algebra
Types can be combined to create new types using various operations.

#### Union
Union can be used with the `|` operator. `『Type』|『Type』`.

This will permit use of all types within the union.

### Intersect
Intersect can be used with the `&` operator. `『Type』&『Type』`.

This will permit the use of deep overlapping types.
This means that if you have intersect 2 map-like types, the resulting type will contain the overlapping key-value pairs.


## Special Non-Primitives
### Shorthand Array
Iterables can be be shortend to `『Type』[]`
An example of this:
```
Foo(arg0: bool, arg1: int, ...argN: int[]): int
```

### Maps/Dictionaries
Maps and Dictionaries can be written as:
```
{『Type|Identifier』: 『Type』}
```` 
or as a generic Type:
```
Map<『Type』,『Type』>
```
Note that using an `Identifier` in a map definition will require the entire map's keys to be the same type depending on your setting.
