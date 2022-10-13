# Float

#### Rescript
- [Js.Float Doc](https://rescript-lang.org/docs/manual/latest/api/js/float)
- [Js.Float Source](https://github.com/rescript-lang/rescript-compiler/blob/master/jscomp/others/js_float.ml)

```reasonml
let n = 1_23.45_56
let m = n +. n *. n -. n /. n
Js.log(m) // 15363.74077136


Js.Float.fromString("123.23")->Js.log // 123.23
```


#### OCaml
- [Float Module](https://v2.ocaml.org/api/Float.html)

```OCaml
let n = 1_23.45_56 ;;
let m = n +. n *. n -. n /. n ;; (* 15363.74077136 *)
```
