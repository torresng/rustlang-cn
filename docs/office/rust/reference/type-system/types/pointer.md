# 指针类型

All pointers in Rust are explicit first-class values. They can be moved or
copied, stored into data structs, and returned from functions.

## Shared references (`&`)

> **<sup>Syntax</sup>**\
> _ReferenceType_ :\
> &nbsp;&nbsp; `&` [_Lifetime_]<sup>?</sup> `mut`<sup>?</sup> [_TypeNoBounds_]

These point to memory _owned by some other value_. When a shared reference to
a value is created it prevents direct mutation of the value. [Interior
mutability] provides an exception for this in certain circumstances. As the
name suggests, any number of shared references to a value may exist. A shared
reference type is written `&type`, or `&'a type` when you need to specify an
explicit lifetime. Copying a reference is a "shallow" operation: it involves
only copying the pointer itself, that is, pointers are `Copy`. Releasing a
reference has no effect on the value it points to, but referencing of a
[temporary value] will keep it alive during the scope of the reference itself.

## Mutable references (`&mut`)

These also point to memory owned by some other value. A mutable reference type
is written `&mut type` or `&'a mut type`. A mutable reference (that hasn't been
borrowed) is the only way to access the value it points to, so is not `Copy`.

## Raw pointers (`*const` and `*mut`)

> **<sup>Syntax</sup>**\
> _RawPointerType_ :\
> &nbsp;&nbsp; `*` ( `mut` | `const` ) [_TypeNoBounds_]

Raw pointers are pointers without safety or liveness guarantees. Raw pointers
are written as `*const T` or `*mut T`, for example `*const i32` means a raw
pointer to a 32-bit integer. Copying or dropping a raw pointer has no effect
on the lifecycle of any other value. Dereferencing a raw pointer is an
[`unsafe` operation], this can also be used to convert a raw pointer to a
reference by reborrowing it (`&*` or `&mut *`). Raw pointers are generally
discouraged in Rust code; they exist to support interoperability with foreign
code, and writing performance-critical or low-level functions.

When comparing pointers they are compared by their address, rather than by
what they point to. When comparing pointers to [dynamically sized types] they
also have their addition data compared.

## Smart Pointers

The standard library contains additional 'smart pointer' types beyond references
and raw pointers.

[Interior mutability]: interior-mutability.html
[_Lifetime_]: trait-bounds.html
[_TypeNoBounds_]: types.html#type-expressions
[`unsafe` operation]: unsafety.html
[dynamically sized types]: dynamically-sized-types.html
[temporary value]: expressions.html#temporary-lifetimes
