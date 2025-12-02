- Feature Name: `UserDefined Implemention`
- Start Date: 2025-12-02
- Issue: [url](https://github.com/0xkhalas/line-rfcs/issues/3)

## Summary

`Line` user definition can implement in two ways. This RFC proposes a using single way to implement UserDefined.

## Motivation

Making clear coding to choice one way to implementing user definition, and clear confuse for coder.

## Detailed design

### User Definition As Declration

#### Explanation

This Declration is default way to declration user definition in anothers langauges like c#, c++, c, rust, it starting with keyword of kind like \[struct, enum, union\] and name with body of it.

#### Goal

This make clear to another programmer to coding beacues he have knowledge as standared betweens major langauges

#### Example

* example of enum

```rs
enum GameState : i32 {
   Starting,
   Playing,
   Stoping,
}
```

* example of struct

```rs
struct Player {
   name: *u8,
   age: i32
}
```

* example of struct with future ideas

```rs
struct Player {
   extend std::Debug, std::Copy, std::Clone;
   impl std::Ops::Eq, std::Debug::Fmt, std::Mem::Drop;

   name: *u8,
   age: i32,

   pub fn fmt() {}
   pub fn drop() {}
   pub fn eq() {}
}
```

* example of function

```rs
use std;

fn main() {
   std::println("Hello, Word!");
}
```

### User Definition As Expression

#### Explanation

Using user definition act as expression.

#### Goal

Using user definition as expression is moving with idea of `Line`, In Line everything act as expression and can be assignable.

#### Example

* example of enum

```rs
const GameState = enum : i32 {
   Starting,
   Playing,
   Stoping,
}
```

* example of struct

```rs
const Player = struct {
   name: *u8,
   age: i32
}
```

* example of struct with future ideas

```rs
const Player = struct {
   extend std::Debug, std::Copy, std::Clone;
   impl std::Ops::Eq, std::Debug::Fmt, std::Mem::Drop;

   name: *u8,
   age: i32,

   pub fn fmt() {}
   pub fn drop() {}
   pub fn eq() {}
}
```

* example of function

```rs
use std;

const main = fn() {
   std::println("Hello, Word!");
}
```

### Hybrid UserDefinition (UserDefined)

#### Explanation

Combind User Definition and make special case for function.

#### Goal

Making funciton as variable declrartion is confuse programmer when he say data and function in same ways.

#### Example

```rs
use std;

const Player = struct {
   name: *u8,
   age: i32
}

fn main() {
   std::println("Hello, World!");
}
```
