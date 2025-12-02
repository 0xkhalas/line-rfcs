- Feature Name: `Implementing 'impl' for struct`
- Start Date: 2025-12-02
- Issue: [url](https://github.com/0xkhalas/line-rfcs/issues/1)

## Summary

Line Now doesn't have way to implement interface to `struct` I trying to inspired by the way of rust impl works
but it does not coming along with `line` syntax. This RFC proposes a new implemenation new way for impl interface funciton for struct.

## Motivation

Line needs way to implement function interface for struct. current has three implements style

* Use impl for `interface only`. you have to tell what implements for struct & impl body outside struct:
```rs
struct Player {
   extend std::Debug, std::Eq;
   impl std::Ops::Eq, std::Fmt, std::Drop;

   pub name: *u8,
   pub age: i32,
   pub health: i32,
   pub inventory: Inventory,

   pub fn new(name: *u8, age: i32) : Player {}
   pub fn attack(self: *Player, damage: i32) : i32 {}
   pub fn shield(self: *Player) {}
}

impl std::Debug::Fmt for Player {}
impl std::Mem::Drop for Player {}
impl std::Ops::Eq for Player {}
```

* Use same as `rust way`. you have to tell what implements for struct & impl body outside struct:
```rs
struct Player {
   extend std::Debug, std::Eq;
   impl std::Ops::Eq, std::Fmt, std::Drop;

   pub name: *u8,
   pub age: i32,
   pub health: i32,
   pub inventory: Inventory,
}

impl Player {
   pub fn new(name: *u8, age: i32) : Player {}
   pub fn attack(self: *Player, damage: i32) : i32 {}
   pub fn shield(self: *Player) {}
}

impl std::Debug::Fmt for Player {}
impl std::Mem::Drop for Player {}
impl std::Ops::Eq for Player {}
```

* Use `impl keyword only` and created methods in struct itself
```rs
struct Player {
   extend std::Debug, std::Eq;
   impl std::Ops::Eq, std::Fmt, std::Drop;

   pub name: *u8,
   pub age: i32,
   pub health: i32,
   pub inventory: Inventory,

   pub fn new(name: *u8, age: i32) : Player {}
   pub fn attack(self: *Player, damage: i32) : i32 {}
   pub fn shield(self: *Player) {}

   pub fn fmt() {}
   pub fn drop() {}
   pub fn eq() {}
}
```

## Drawbacks

`interface only`
* Here problem it `Line` act like every file as struct beacuse this now how we need struct impl itself:

```rs
struct Player {
   impl std::Debug::Fmt for Player {}
}
```

`rust ways`
* this problem is same as above but problem it is adding more way to implement functions for struct. this make confuse about coding and which way you choice to implement function for it:

## Opinion

i think the last one `impl keyword only` is good because is working with way of `Line` files working as all file act as Struct like this.

```rs
extend std::Debug, std::Eq;
impl std::Ops::Eq, std::Fmt, std::Drop;

pub name: *u8,
pub age: i32,
pub health: i32,
pub inventory: Inventory,

pub fn new(name: *u8, age: i32) : Player {}
pub fn attack(self: *Player, damage: i32) : i32 {}
pub fn shield(self: *Player) {}

pub fn fmt() {}
pub fn drop() {}
pub fn eq() {}
```
