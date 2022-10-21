# Module
- Module name must begin with an uppercase letter
- Every .res file is a module. The convention is to capitalize file names.
- Every .resi file is a signature.

### Rescript

#### Module definition
```reasonml
module M = {
  let x = 17
  let y = 25
  %%private(let z = 10)
}
```

#### Module definition with signature
```reasonml
module Point: {
  let x: int
  let y: int
} = {
  let x = 10
  let y = 20
  let z = 40
}
```

#### Empty module
```reasonml
module E = {}
```

#### Module nesting
```reasonml
module X = {
  let x = 10
  module Y = {
    let y = 11
  }
  module Z = {
    let z = 12
  }
}
X.Y.y->Js.log
X.Z.z->Js.log
```

#### Extending module
```reasonml
module M1 = {
  let one = 1
}

module M2 = {
  let two = 2
}

module M3 = {
  include M1
  include M2
  let three = 3
}
open Js.Int
Js.log(`${M3.one->toString}, ${M3.two->toString}, ${M3.three->toString}`)

#### Opening module
open M3
one->Js.log
two->Js.log
```

#### Overriding open to turn off shadow warnings
```reasonml
module A = {
  let a = 1
}
module Foo = {
  module A = {
    let a = "one"
  }
}
open A
open! Foo.A
a->Js.log
```

#### Destructuring module
```reasonml
/* types cannot be extracted with module destructuring */
module Point2D = {
  type t = (float, float)
  let make = (x, y) => (x, y)
  let getX = ((x, _)) => x
  let getY = ((_, y)) => y
  let add = ((x1, y1), (x2, y2)) => (x1 +. x2, y1 +. y2)
  let substract = ((x1, y1), (x2, y2)) => (x1 -. x2, y1 -. y2)
}

let {make, add, substract} = module(Point2D)
let p1 = make(1.1, 2.2)
let p2 = make(10.1, 20.2)
add(p1, p2)->Js.log
substract(p2, p1)->Js.log
```

### OCaml
[My OCaml Notes here](https://github.com/nyinyithann/notes_on_ocaml/blob/main/notes/lang/module.ipynb)
