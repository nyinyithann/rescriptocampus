# Unit

#### Rescript
- has a single value `()`
- compiles to JS's `undefined`

```reasonml
let x = ()
Js.log(x) // undefined in js
```

#### OCaml
- [Unit Module](https://v2.ocaml.org/api/Unit.html)
```Ocaml
let x = () ;;
Unit.equal x x ;; (* true *)
```

