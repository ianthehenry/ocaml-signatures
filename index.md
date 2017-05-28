---
layout: default
title: OCaml Function Signatures
---

Annotated return type:

```ocaml
val foo : int -> int

let foo x : int = 123
```

Annotated positional argument:

```ocaml
val foo : int -> int

let foo (x : int) = 123
```

Annotated return type and positional argument:

```ocaml
val foo : int -> int

let foo (x : int) : int = 123
```

Named argument:

```ocaml
val foo : x : int -> int

let foo ~x = 123
```

Annotated named argument:

```ocaml
val foo : x : int -> int

let foo ~(x : int) = 123
```

Optional argument:

```ocaml
val foo : ?x : int -> int

let foo ?x = 123
```

Optional argument with a default value:

```ocaml
val foo : ?x : int -> int

let foo ?(x = 0) = 123
```

Annotated optional argument:

```ocaml
val foo : ?x : int -> int

let foo ?(x : int) = 123
```

Annotated optional argument with a default value:

```ocaml
val foo : ?x : int -> int

let foo ?(x : int = 0) = 123
```

Universally quantified type:

```ocaml
val foo : 'a -> int

let foo (type a) (x : a) = 123
```

You will usually see type variables introduced like this so that a GADT's phantom can vary over different branches of a match statement:

```ocaml
val foo : 'a My_gadt.t -> int

let foo (type a) (x : a My_gadt.t) = 123
```

Sometimes you want to recurse within such a function with your type variable unifying with a different type in the recursive call. For some reason that is not allowed with the above signature. You must write instead:

```ocaml
val foo : 'a My_gadt.t -> int

let rec foo : type a. a My_gadt.t -> int =
  fun x -> 123
```

This is useful when you have recursive GADTs where the "fields" in a value do not necessarily have the same type (with regard to the phantom) as the value itself.
