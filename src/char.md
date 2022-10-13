# Char

#### Rescript
- Char doesn't support Unicode or UTF-8 and is therefore not recommended.
```reasonml
let ch = 'a'
// convert char to string
let s = String.make(1, ch)
// convert string to char
let x = String.get("a",0)
```

#### OCaml
```OCaml
let ch = 'a' ;;
(* convert char to string *)
let s = String.make 1 ch ;;
let s = Char.escaped ch ;;
let s = Printf.sprintf "%c" ch ;;
(* convert string to char *)
let ch = String.get "a" 0 ;;
```
