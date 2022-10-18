# Functor
### Rescript
- Functors use the `module` keyword 
- Functors take modules as arguments and return a module
- Funcotrs require annotating arguments
- Functors must start with a capital letter

```reasonml
module type X = {
  let x: int
}
module type Y = {
  let y: int
}

module MX = {
  let x = 10
}
module MY = {
  let y = 10
}

module type TXY = {
  let xy: int
}

module F = (M1: X, M2: Y): TXY => {
  let xy = M1.x + M2.y
}

module XY = F(MX, MY)
XY.xy->Js.log
```

#### sample code
```reasonml
module type POINT = {
  type item
  type t
  let make: (item, item) => t
  let getX: t => item
  let getY: t => item
  let add: (t, t) => t
  let substract: (t, t) => t
}

module type ADD_SUB = {
  type t
  let add: (t, t) => t
  let substract: (t, t) => t
}

module MakePoint = (MP: ADD_SUB): (POINT with type item := MP.t) => {
  type item = MP.t
  type t = (item, item)
  let make = (x, y) => (x, y)
  let getX = ((x, _)) => x
  let getY = ((_, y)) => y
  let add = ((x1, y1), (x2, y2)) => (MP.add(x1, x2), MP.add(y1, y2))
  let substract = ((x1, y1), (x2, y2)) => (MP.substract(x1, x2), MP.substract(y1, y2))
}

module Int = {
  type t = int
  let add = (x: t, y: t) => x + y
  let substract = (x: t, y: t) => x - y
}

module Float = {
  type t = float
  let add = (x: t, y: t) => x +. y
  let substract = (x: t, y: t) => x -. y
}

module IntPoint = MakePoint(Int)
let ip1 = IntPoint.make(10, 10)
let ip2 = IntPoint.make(11, 11)
IntPoint.add(ip1, ip2)->Js.log

module FloatPoint = MakePoint(Float)
let ip1 = FloatPoint.make(10., 10.)
let ip2 = FloatPoint.make(11., 11.)
FloatPoint.add(ip1, ip2)->Js.log
```

### OCaml
[My Ocaml Notes here](https://github.com/nyinyithann/notes_on_ocaml/blob/main/notes/lang/functor.ipynb)
