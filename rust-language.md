# Rust

- [Install Rust](https://www.rust-lang.org/tools/install)

## Overview

- `rustc` is the rust compiler. You don't often have to interact with it directly.
- `cargo` is the Rust package manager. Think of it like `npm`/`pip`/`rake`.
- `rustup` helps you manage your Rust install.

### Features

- Variables are immutable by default.
- Block scoped language.
- Variables defined with underscores by convention: `my_variable_here`

## Tooling

```shell
# update your version of rust
rustup update

# see all of cargo's options
cargo --list

# get detailed info about your rust compiler version
rustc --version --verbose

# create an optimized version of your project
cargo build --release
```

## Language Features

```rust
pub fn run() {
  //...
}
```

### Primitive types

[See documentation here](https://doc.rust-lang.org/std/index.html#primitives).

- Integers: u8, i8, u16, i16, u32, i32 (default), u64, i64, u128, i128
- Floats: f32, f64 (default)
- Boolean
- Characters
- Tuples
- Arrays

- [ ] Functions
- [ ] Variables
  - [ ] Combining types
- [ ] Arrays (vectors)
  - [ ] Initialize
  - [ ] Push
  - [ ] Pop
  - [ ] Shift
  - [ ] Unshift

### Variables

```rust
// Immutable
let name = "John";
println!("{} is a cool dude", name);

// Mutable
let mut age = 27;
println!("I am {} years old", age);
age = 33;
println!("I am {} years old now", age);

```

### Strings

```rust
// Positional:
println!("{} + {} = {}", 1, 2, 3);

// Math
println!("5 + 7 = {}", 5 + 7);

// Array indexes:
println!("{2} is {1} minus {0} ", 1, 2, 3);

// Named parameters:
println!("{name} is {age} years old.", name = "John", age = 35);

// Debug data:
println!("{:#?}", json);


let str = "Hello";
println!("Hello is {} characters long", str.len());

// Pushing characters
let mut str = String::from("Hello");
str.push(' '); // Push single character
str.push_str("World!"); // Push a string
println!("'{}' is {} characters long", str, str.len());


// Empty
let str = "Foo";
println!("Empty: {}", str.is_empty());

// Contains text
let str = "Foobar";
println!("Has bar: {}", str.contains("bar"));

// Replace
let str = "World!";
println!("Hello {}", str.replace("World!", "Universe!"));

// Split and iterate:
for word in "Hello World!".split_whitespace() {
  println!("{}", word);
}
```

### Tuples

Lists of items of a mix of types.

```rust
let person: (&str, &str, i8) = ("John", "Smith", 35);
println!("{} {} is {} years old", person.0, person.1, person.2);
```

### Arrays

Fixed length lists of data of a given type.

```rust
let mut ages: [i32; 5] = [22, 35, 83, 19, 45];
ages[2] = 51; // [22, 35, 51, 19, 45]
ages.len(); // 5
ages[1..3] = // [35, 51, 19]
```

### Vectors

Resizable arrays.

```rust
let mut ages: Vec<i32> = vec![22, 35, 83, 19, 45];
ages[2] = 51; // [22, 35, 51, 19, 45]
let slice: &[i32] = &ages[1..3];
println!("Slice: {:?}", slice); // [35, 51]
println!("Length: {}", ages.len()); // 5
```

## Useful Libraries

- [clap](https://github.com/clap-rs/clap) - Command line library
- [reqwest](https://github.com/seanmonstar/reqwest) - An HTTP client.
