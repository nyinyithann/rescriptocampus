# @deriving({jsConverter: newType})
- create converter functins the allow back and forth conversion between generated abstract type and ReScript variant values
- `newType` hides the fact that JS enum are ints 

```reasonml
@deriving({jsConverter: newType})
type letter =
  | @as(1) A
  | B
  | @as(4) E
  | F

/* usage */

letterToJs(A)->Js.log // 1
letterToJs(B)->Js.log // 2
letterToJs(E)->Js.log // 4
letterToJs(F)->Js.log // 5

let f = letterFromJs(letterToJs(F))
f->Js.log // print 3 here, that's OK we don't care the value as long as we can check the type
(f === F)->Js.log // true
```

