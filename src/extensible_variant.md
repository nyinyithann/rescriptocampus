# Extensible Variant

#### Rescript
```reasonml
module Expr = {
  type t = ..

  type t += Int(int)
  type t += Float(float)
}

type Expr.t += String(string)

let toString = e => {
  switch e {
  | Expr.Int(i) => Js.log(i)
  | Expr.Float(f) => Js.log(f)
  | String(s) => Js.log(s)
  | _ => Js.log("other")
  }
}

toString(Expr.Int(10))
toString(Expr.Float(3.14))
toString(String("Hello"))
```

##### exceptios are extensible variant
```reasonml
exception ConnectionError(string)
// is equivalent to
type exn += ConnectionError(string)
```

#### OCaml
[My Notes here](https://github.com/nyinyithann/notes_on_ocaml/blob/main/notes/lang/variants.ipynb)
```OCaml
module Expr = struct
    type t = ..
    
    type t += Int of int
    
    type t += Float of float 
      
end ;;

type Expr.t += String of string ;;

let to_string = function
    | Expr.Int x -> Int.to_string x
    | Expr.Float x -> Float.to_string x
    | String x -> x 
    | _ -> "?" ;;
```
