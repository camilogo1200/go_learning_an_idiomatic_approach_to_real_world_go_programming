# Primitive types and declarations

## Booleans

- The bool type represents Boolean variables.
- Variables of bool type cam have one of two values: `true` or `false`
- The `zero` value for bool is false

```go
var flag bool // no value assigned, set to false
var isAwesome = true
```

## Numeric Types

| Type Name  | value Range                                 |
| ---------- | ------------------------------------------- |
| **int8**   | -128 to 127                                 |
| **int16**  | -32768 to 32767                             |
| **int32**  | -2147483648 to 2147483647                   |
| **int64**  | -9223372036854775808 to 9223372036854775807 |
| **uint8**  | 0 to 255                                    |
| **uint16** | 0 to 65536                                  |
| **uint32** | 0 to 4294967295                             |
| **uint64** | 0 to 18446744073709551615                   |

## Special integer types

- `byte` : is an alias for `uint8`
- `int` : isn't consistent from platform to platform. it is a compile-time errorto assign, compare, or perform mathematical operations between `int` and an `int32` or `int64` without a type conversion
- `uint` : follows the same rules of `int` only its unsigned, the values are always 0 or positive.
- there are two other special names for integer types, `rune` and `uintptr`.

## Choosing which integer to use

### Three simple rules to follow

- If you're working with a binary file format or network protocol that has an integer of a specific size or sign, use the corresponding integer type.
- If you are writing a library function that should work with any integer type, write a pair of functions, one with int64 fir the parameters and variables and the other with uint64
- in all other cases , just use `int`

## Integer operators

- +,-,\*,/, with % for modulus

- integer div by 0 causes a `panic`
- +=, -=, \*=, /=, %=
- You compare integers with ==, !=, >, >=, < and, <=

## Floating point Types

There are two floating point in Go

`float32`
`float64`

- Always use `float64`, unless you have to with compatible with an existing format
- Floating points literals have a default type of float64, so always using `float64` is the simplest option.
- Don't compare floats using `!=` or `==`

## Strings and Runes

Go include strings as a Built-in type.

- The zero value for string is an empty string
- Go supports Unicode.
- strings are compared for equalityusing `==` difference with `!=` or ordering with </, <=, >, >=.
- They are concatenated using the `+` operator.
- String in go are inmutable; you can reassign the valueof a string variable, but you cannot change the value of the string that is assigned to it.
- Go also has a type that represents a single code point. the `rune` type is an alias for the `int32` type, just like `byte` is an alias for uint8.
- If you are referring to a character, use the rune type, not hte int32 type.
  \

## Type conversions

-= as Go intends to be a clarity language and readable. Go does not allow \***\*automatic type promotion\*\***

- you must use a type conbversionwhen variable types do not match, even different-sized integers and floats must be converted to the sametype to interact.

```go
//Type conversions

var x int = 10
var y float64 = 30.2
var z float64 = float64(x) + y
var d int = x + int(y)

```

# Var vs :=

For a small language. Go has a lot of ways to declare variables.

- The most verbose way to declare a variable in Go uses the `var` keyword, an explicit type and an assignment.

```go
   var x int = 10
```

- if the type onthe righthand side of the `=` is the expected type of your variable, you can leave off the type from the left side of the `=`

```go
   var x = 10
```

- You can declare multiple variabels at once with `var`, and they can be of the same type

```go
   var x,y int = 10, 20

// all zero values of the same type
    var x,y int

// or different types
var x,y = 10, "hello"
```
- There is one more way to use `var`. If you are declaring multiple variables at once, you can wrap them in a `declaration list` 

```go
   var (
    x int
    y = 20
    z int = 30
    d,e = 40, "hello"
    f,g string
   )
```

### :=

Go also supports a short declaration format. Whe you are within a function, you can use the `:=` operator to replace a var declaration that use type inference.

```go
   var x = 10
   x := 10

//multiple variables at once
   x, y := 10, "Hello"

```

there is one limitation on `:=`. If you are declaring a variable at package level, you must use `var` because := is not legal outside of functions.


## Notes about := 

There are some situations within functions where you should avoid `:=`
-    When initializing a variable to its zero value, use var x int.This makes clear that the zero value is intended.
-    When assigning an untyped constant or a literal to avariable and the default type for the constant or literail isn't the type you want for the variable, use the `long var form` with the type specified.

```go
   x := byte(10)

   //it is more idiomatic to write 
   var x byte = 10
```
- sometimes := assignation result in `shadowing`.