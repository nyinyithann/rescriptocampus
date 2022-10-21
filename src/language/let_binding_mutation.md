# let Binding
#### Rescript
```reasonml
let a = 10
let b = 10
let c = a + b

let x = 1 and y = 2
Js.log(x + y) // 3

// block scope
// z = 3
let z = {
  let x = 1
  let y = 2
  x + y
}

// shadow
let x = 1
let x = 2
let x = 3
Js.log(x) // 3
```

#### OCaml
```ocaml
let z = let x = 1 and y = 2 in x + y ;;
let z = let x = 1 in let y = 2 in x + y;;
```

# Mutable binding
#### Rescript
```reasonml
let x = ref (10)
x := x.contents + 1
x.contents = x.contents + 1 /* x is 12 */


type box<'a> = {mutable contents: 'a}
let box = v => {contents: v}

let r = box(10)
r.contents = r.contents + 1
```

#### OCaml
```ocaml
let x = ref 10 in
x := !x + 1 ;;
x.contents <- x.contents + 1;;
!x ;; (* x is 12 *)
```
