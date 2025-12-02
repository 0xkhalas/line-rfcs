- Feature Name: `File & Struct Implement`
- Start Date: 2025-12-02
- Issue: [url](https://github.com/0xkhalas/line-rfcs/issues/2)

## Summary

Struct & File In Line and how they working and Implemented of it. This RFC proposes a idea of struct implement and how file (module) system working in line.

## Motivation

Every file in `Line` act as Struct you can define & declare with variables, fields and functions with controll Visibility `pub`.

## Detailed design

### File & Definition

Line has Two way to define or implement struct into it.

* Struct Definition, this normal definition you can set inside file or another user-definition
```rs
struct App {
   const APP_ID = "LINE_TEST"

   pub name: *u8,
   age: i32,

   fn new() {}
   fn shutdown() {}
}
```

* Single File Structed, this is normal file in `Line` can be act like struct.
```rs
const APP_ID = "LINE_TEST"

pub name: *u8,
age: i32,

fn new() { }
fn shutdown() {}
```

### Visibility

Line handle Visibility with `pub` keyword, this make you can control visibility all staff inside struct, `pub` keyword inspired from rust with have same effect pub and scope accessibility \[self, parent, root\]:
```rs
pub(self) struct Player {}
pub(root) struct Player {}
pub(parent) struct Player {}

pub(self) const NUMBER = 5
pub(self) let number = 5
```

### Use Keyword

In Line if you went to access another file or imported you will using keyword `use` this keyword can used in two ways to access data.

* Global Scope Declration
```rs
use std; // access in current file
pub use std; // access in current and pass to another file imports the current one

fn main() {
   std::println!("Hello, World!");
}
```

* Expression, `use std` will return value of struct `std` this struct connect with anothers structs to present all library stand for std.

```rs
fn main() {
   const std = use std;

   std::println!("Hello, World!");
}
```

### File System

In Line every file present struct and every folder have main route to access insider files.

* Example Tree

```sh
Project/
├── build.line
└── src
    ├── engine
    │   ├── _.line -> router
    │   ├── graphics
    │   │   ├── _.line -> router
    │   │   ├── shader.line
    │   │   ├── texture.line
    │   │   └── vertex_array.line
    │   ├── render
    │   │   ├── _.line -> router
    │   │   ├── camera.line
    │   │   └── mesh.line
    │   └── window
    │       ├── _.line -> router
    │       └── input.line
    └── main.line
```

In connection with files you need to set `pub` keyword for `use` keyword or variable to access from outside.

* router file `src/engine/_.line`, this file will make connection from insider files\folders to outsider

```rs
pub const Graphics = use graphics;
pub const Renderer = use render;
pub use window;
```

* router file `src/main.line`, this main file show how will use imported files\folders and access staff inside:

```rs
use engine;
use engine::Graphics;

fn main() {
   let main_window = engine::window::new("Example Window", 400, 800);
   let renderer = engine::Rendere::new(&main_window);
   let painter = Graphics::new(&renderer);

   painter.draw_rectangle(0, 0, 25, 25, Graphics::Color::Red);
}
```

