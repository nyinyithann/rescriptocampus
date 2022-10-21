# Module Type

### Rescript

#### Module type declaration
```reasonml
module type T = {
  let x: int
}

module M = {
  let x = 10
}

module MT1: T = M // same as module MT1 = (M : T)
MT1.x->Js.log
```

#### Sealing module with Module Type
```reasonml
module M2: T = {
  let x = 10
}
module MT2: T = M2
MT2.x->Js.log

module Z = {
  let z = 11.11
}
module M3: module type of Z = {
  let z = 22.22
}
```

#### Sharing constraint with "with" operator
```reasonml
module type TPair = {
  type t
  let pair: t
}

module Pair: TPair = {
  type t = (float, float)
  let pair: t = (11., 22.)
}

let p = Pair.pair // this is ok
let p': Pair.t = Pair.pair // this is ok
/* this will throw error cause TPair.t is abstrat type and not compitable with (float, float) */
// let p: (float, float) = Pair.pair

// use "with" operator
module APair: TPair with type t = (int, int) = {
  type t = (int, int)
  let pair = (1, 2)
}
let pp: (int, int) = APair.pair

module type TP = TPair with type t = (float, float)
module TPPair: TP = {
  type t = (float, float)
  let pair = (1.1, 2.2)
}
let pt: (float, float) = TPPair.pair
```

#### Destructive Substitution (:=) replace abstract type with the concrete type provided in constraint
```reasonml
module type List = {
  type item
  type t
  let data: t
}

module MList: List with type item := int and type t := list<int> = {
  type item = int
  type t = list<item>
  let data: t = Belt.List.makeBy(10, x => x + 1)
}
let lst: list<int> = MList.data
```

#### Module constraint with the "with" operator
```reasonml
module type TXY = {
  type x
  type y
}

module type MType = {
  module A: TXY
}

module B = {
  type x = int
  type y = int
  let x = 101
}

module C: MType with module A = B = {
  module A = {
    type x = int
    type y = int
    let x = B.x
  }
}
C.A.x->Js.log // 101
```
##### [realworld code from darklang editor](https://github.com/darklang/dark/blob/main/client/src/prelude/Belt_extended.res) 
```reasonml
module Belt = {
  include (Belt: module type of Belt with module Map := Belt.Map and module Result := Belt.Result)

  module Result = {
    include Belt.Result

    let pp = (
      okValueFormatter: (Format.formatter, 'okValue) => unit,
      errValueFormatter: (Format.formatter, 'errValue) => unit,
      fmt: Format.formatter,
      value: t<'okValue, 'errValue>,
    ) => {
      switch value {
      | Ok(value) =>
        Format.pp_print_string(fmt, "Ok")
        okValueFormatter(fmt, value)
      | Error(value) =>
        Format.pp_print_string(fmt, "Error")
        errValueFormatter(fmt, value)
      }
    }
  }

  module Map = {
    include (Belt.Map: module type of Belt.Map with module String := Belt.Map.String)

    module String = {
      include Belt.Map.String

      let pp = (
        valueFormatter: (Format.formatter, 'value) => unit,
        fmt: Format.formatter,
        map: t<'value>,
      ) => {
        Format.pp_print_string(fmt, "{ ")
        Belt.Map.String.forEach(map, (key, value) => {
          Format.pp_print_string(fmt, key)
          Format.pp_print_string(fmt, ": ")
          valueFormatter(fmt, value)
          Format.pp_print_string(fmt, ",  ")
        })
        Format.pp_print_string(fmt, "}")
        ()
      }
    }
  }
}
```

#### Extendng module type
```reasonml
module type TCounter = {
  type t
  let counter: t
}
module type TUpDown = {
  include TCounter
  let up: t => t
  let down: t => t
}
module Counter: TUpDown with type t = int = {
  type t = int
  let counter = 0
  let up = c => c + 1
  let down = c => c - 1
}
let count = 0
Counter.up(count)->Js.log
Counter.down(count)->Js.log
```

#### Recovering the type of a module
```reasonml
module Pi = {
  let pi = 3.14
}

module type TMaths = {
  include module type of Pi
}

module Maths: TMaths = {
  let pi = 3.141576
}
Maths.pi->Js.log
```

#### Empty module type
Empty module type is mainly used to hide the implementation of a module.
```reasonml
/* foo.mli */
module type S = {}

/* foo.ml */
module type S = {
  type t
  let unsafe_op: t => t
}

module M: S = {
  type t = int
  let unsafe_op = x => x + x
}

module Make = (X: S) => {
  let safe_op = x => X.unsafe_op(x)
}
```

### OCaml
[My OCaml Notes here](https://github.com/nyinyithann/notes_on_ocaml/blob/main/notes/lang/module%20type.ipynb)
