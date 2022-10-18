# First-class Module

### Rescript

#### Packing a module as a first-class value and unpacking it into a module
```reasonml
module type T = {
  let x: int
}
module M = {
  let x = 77
}
let packed = module(M: T)
module Unpacked = unpack(packed)
```

#### Passing first-class module to a function and unpacking it using pattern match
```reasonml
let show = (m: module(T)) =>
  switch m {
  | (module(UM: T)) => UM.x->Js.log
  }
show(packed)
```

#### Returning a first-class module from a function
```reasonml
let getM = (x: int): module(T) => {
  module(
    {
      let x = x
    }
  )
}

module UM = unpack(getM(10))
UM.x->Js.log
```

#### With locally abstract type
```reasonml
module type DOUBLE = {
  type t
  let double: t => t
}

let doubleList = (type a, nums: array<a>, mb: module(DOUBLE with type t = a)) => {
  module D = unpack(mb)
  Belt.Array.map(nums, D.double)
}

module DInt: DOUBLE with type t = int = {
  type t = int
  let double = x => x * 2
}

module DFloat: DOUBLE with type t = float = {
  type t = float
  let double = x => x *. 2.
}

doubleList([1, 2, 3], module(DInt))->Js.log
doubleList([4.3, 3.2, 32.2], module(DFloat))->Js.log
```

#### With module type having abstract type
```reasonml
module type Comparable = {
  type t
  let compare: (t, t) => int
}

type comparable<'a> = module(Comparable with type t = 'a)

let compare = (type a, x, y, c: comparable<a>) => {
  module C = unpack(c)
  C.compare(x, y)
}

module IntCmp: Comparable with type t = int = {
  type t = int
  let compare = (x, y) => x - y
}

module FloatCmp: Comparable with type t = float = {
  type t = float
  let compare = (x, y) => x > y ? 1 : y > x ? -1 : 0
}

compare(1, 2, module(IntCmp))->Js.log
compare(1., 2., module(FloatCmp))->Js.log
```

#### Functor as first-class module
```reasonml
module type Stringable = {
  type t
  let toString: t => string
}

module type MakePrinterType = (Item: Stringable) =>
{
  let print: Item.t => string
}

module MakePrinter = (Item: Stringable) => {
  let print = x => "Printer: " ++ Item.toString(x)
}

module StringableInt = {
  type t = int
  let toString = Js.Int.toString
}

module StringableFloat = {
  type t = float
  let toString = Js.Float.toString
}

let f = module(MakePrinter: MakePrinterType)
module IntPrinter = unpack(f)(StringableInt)
IntPrinter.print(45322)->Js.log

module FloatPrinter = MakePrinter(StringableFloat)
FloatPrinter.print(112.211)->Js.log
```

### OCaml
[My OCaml Notes here](https://github.com/nyinyithann/notes_on_ocaml/blob/main/notes/lang/first-class%20module.ipynb)
