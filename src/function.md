# Function

#### Basic
```reasonml
open Js
let add = (a, b) => a + b
log(add(1, 2))

let add_float: (float, float) => float = (x, y) => x +. y
log(add_float(1., 2.))
```

#### Recursive function
```reasonml
open Js
let rec neverTerminate = () => neverTerminate()

let fold = (l, acc, f) => {
  let rec loop = (l, acc) => {
    switch l {
    | list{} => acc
    | list{h, ...t} => loop(t, f(acc, h))
    }
  }
  loop(l, acc)
}
fold(list{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}, 0, add)->log // 55
```

#### Mutually recursive function
```reasonml
open Js
let rec isOdd = n =>
  if n == 0 {
    false
  } else {
    isEven(n - 1)
  }
and isEven = n =>
  if n == 0 {
    true
  } else {
    isOdd(n - 1)
  }
isOdd(10)->log
isOdd(11)->log
```

#### Curried vs uncuried function
```reasonml
// Functions in Rescript are curried by default.
open Js
let mul = (x, y) => x * y
let curried_mul = mul(10)
curried_mul(10)->log

// uncurried
let mulU = (. x, y) => x * y
mulU(. 10, 10)->log

// with type annotation
let addU: (. float, float) => float = (. x, y) => x +. y
addU(. 1., 2.)->log

// with placeholders
let add = (x, y, z) => x + y + z
let addX = add(_, 2, 3)
let addY = add(1, _, 3)
let addZ = add(1, 2, _)
addX(1)->Js.log // 6
addY(2)->Js.log // 6
addZ(3)->Js.log // 6
10->addX->Js.log // 15
10->addY->Js.log // 14
10->addZ->Js.log // 13

let addXY = add(_, _, 3)
addXY(2)->Js.log // 7
10->addXY->Js.log // 23

let addXYZ = add(_, _, _)
addXYZ(10)->Js.log // 30
100->addXYZ->Js.log // 300
```

#### ignore() function to ignore the return value of a function
```reasonml
mySideEffect()->Promise.catch(handleError)->ignore
Js.Global.setTimeout(myFunc, 1000)->ignore
```


#### Label arguments
```reasonml
open Js
let range = (~start, ~end) => Belt.Array.makeBy(end - start, x => x + start)
range(~start=0, ~end=10)->log

/* alias */
let range = (~start as s, ~end as e) => Belt.Array.makeBy(e - s, x => x + s)
range(~start=0, ~end=10)->log
```

#### Labels and type inference
labeled and optional arguments cannot be inferred completely 
```reasonml
open Js
let bump = (~step=?, x) =>
  switch step {
  | Some(s) => x + s
  | None => x
  }

/* 
this will get compiler error, bump's signature should be provided

let bumpIt = (bump, x) => bump(~step=2, x)
bumpIt(bump, 10)->log
*/

let bumpIt = (bump: (~step: int=?, int) => int, x) => bump(~step=2, x)
bumpIt(bump, 10)->log


/* paramaters order */
let add = (~x, ~y, ()) => x + y
let f = g => g(~x=1, ~y=2, ())
f(add)->log // 3

// this won't work, paramaters should be applied in the same order as declaration site
let f = g => g(~y=1, ~x=2, ())
```
