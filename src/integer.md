# Integer

#### Rescript
- 32-bits, truncated when necessary
- Much smaller range than JS numbers. Use float if bigger number needed.
- [Js.Int Doc](https://rescript-lang.org/docs/manual/latest/api/js/int)
- [Js.Int Source](https://github.com/rescript-lang/rescript-compiler/blob/master/jscomp/others/js_int.ml)


```reasonml
let n = 1_234_456
let m = n + n * n - n / n
let x = mod(10, 3) // remainder

Js.log(Js.Int.max) //  2147483647
Js.log(Js.Int.min) // -2147483648
Js.log(Js.Int.toFloat(10))
```

#### OCaml
- 31-bits or 63-bits depends on platform. [Why?](https://ocaml-tutorial.org/performance_and_profiling)
- [Int module](https://v2.ocaml.org/api/Int.html)

```OCaml
let n = 1_234_456 ;;
let m = n + n * n - n / n ;;
let x = 10 mod 3 ;; 
let x = (mod) 10 3 ;;

Int.add 1 1 (* 2 *)
Int.of_float 10.2 (* 10 *)
```
