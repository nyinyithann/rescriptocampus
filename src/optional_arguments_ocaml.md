# Optional Arguments(OCaml)

[Run the following code at sketch.sh](https://sketch.sh/s/CPiIIfDvGRm4evCGM73TbH/)

#### Optional arguments
```ocaml
let concat ?sep x y =
  let sep = match sep with None -> "" | Some s -> s in
  x ^ sep ^ y ;;
concat ~sep:"," "Hello" "World";;
```

#### Need to add "()" if optional argument is the last
```ocaml
let concat x y ?sep () =
  let sep = match sep with None -> "" | Some s -> s in
  x ^ sep ^ y ;;
concat ~sep:"," "hello" "world" () ;;
```

#### With function type signature and paramater type annotation
```ocaml
(* val concat: string -> string -> ?sep:string -> unit -> string *)
let concat (x: string) (y: string) ?(sep:string option) () =
  let sep = match sep with None -> "" | Some s -> s in
    x ^ sep ^ y ;;
concat ~sep:"," "hello" "world" () ;;
```

#### Passing value of option type to optional paramater
```ocaml
let concat ?sep x y =
  let sep = match sep with None -> "" | Some s -> s in
  x ^ sep ^ y ;;
let separator = Some("/") in
concat ?sep:separator "hello" "world" ;;
let sep = None in
concat ?sep "hello" "world" ;;
```

#### Optional paramater with default value
```ocaml
let bump ?(step=1) x = x + step ;;  
bump 10;;
```

#### Partial application
```ocaml
let test ?x ?y () ?z () = (x, y, z) ;;
test () () ~x:1 ~y:2 ~z:3 ;;
test ()() ;;
test ~x:1 ~y:2 () () ;;
```
