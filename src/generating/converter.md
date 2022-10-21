# @deriving(jsConverter)
- create converter functins the allow back and forth conversion between JS integer enum and ReScript variant values

```reasonml
@deriving(jsConverter)
type letter =
  | @as(1) A
  | B
  | @as(4) E
  | F

letterToJs(A)->Js.log // 1
letterToJs(B)->Js.log // 2
letterToJs(E)->Js.log // 4
letterToJs(F)->Js.log // 5

// print A 
switch letterFromJs(1) {
    |Some(A)  => Js.log("A")
    |_ => ()
}

// print None
switch letterFromJs(3) {
    |None => Js.log("None") 
    | _ => ()
}
```
