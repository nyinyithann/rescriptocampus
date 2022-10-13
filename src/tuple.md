# Tuple

#### Rescript
- immutable 
- ordered
- fixed-sized at creation time
- heterogeneous
```reasonml
let pair: (string, int) = ("Number", 1)
Js.log(pair) // ['Number', 1]
let (n, _) = pair
Js.log(n) // Number
let (x, y, z) = (1, 2, 3)
```

#### OCaml
```OCaml
let pair = ("Number", 1) ;;
let (n, _) = pair ;;
let (x, y, z) = (1, 2, 3) ;;
```
