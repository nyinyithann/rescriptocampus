# if else

#### Rescript
if statements are expression.
```reasonml
let max = (x, y) =>
  if x > y {
    x
  } else {
    y
  }

let f = (x, y) =>
  x + if y > 0 {
    y
  } else {
    0
  }
f(11, 0)->Js.log // 11

let rec range = (x, y) => {
  if x > y {
    list{}
  } else {
    list{x, ...range(x + 1, y)}
  }
}
range(1, 10)->Js.log

// unit aka () is return for implicit else branch
let a = if true {
  ()
}
```

```reasonml
/* error here cause if branch returns integer whereas else branch returns unit
let a = if true {
  10
}
*/
```

```reasonml
// ternary operator
let abs = (x: float) => x >= 0. ? x : x *. -1.
abs(-99.9)->Js.log
```

#### OCaml
