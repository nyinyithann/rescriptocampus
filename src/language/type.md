# Type
Rescript type system is strong, static, sound, fast and inferred.

#### Rescript

##### Type Inference
```reasonml
let a = 10
let f = 10.
let add = (a, b) => a + b
```
##### Type annotation
```reasonml
let a: int = 10
let f: float = 10.
let add: (int, int) => int = (a, b) => a + b
Js.log(add(a, a)) // 20
// or
let add = (a: int, b: int): int => a + b
Js.log(add(a, a)) // 20
```
##### Type alias
```reasonml
type kg = float
let weight: kg = 88.

type pair = (string, int)
let kv: pair = ("Key", 100)
Js.log(kv) // [ 'key', 100 ]
```

##### Mutually recursive type
```reasonml
type rec person = {
  name: string,
  friends: list<person>,
}

type rec room = {building: building}
and building = {rooms: array<room>}
```
##### Generic type 
```reasonml
type gpair<'a, 'b> = ('a, 'b)
let x: gpair<string, int> = ("Counter", 128)
Js.log(x) // [ 'Counter', 128 ]

type result<'a, 'e> = 
    | Ok('a) 
    | Error('e)
let v = Ok(100)
let e = Error("Not Found Error")
```
##### Type escape hatch
```reasonml
external convertToString: char => string = "%identity"
let ch = 'a'
let str = convertToString(ch) ++ "bc"
Js.log(str) // 97bc
```

#### OCaml
```OCaml
(* type inference *)
let a = 10 ;;
let b = ("hello", 123) ;;
let add a b = a + b ;;

(* type annotation *)
let add (a:int) (b:int) : int = a + b ;;

(* type alias *)
type kg = float ;;
let weight : kg = 88.3 ;;
type pair = (string * int)
let p : pair = ("hello", 123) ;;

(* mutually recursive types *)
type person = {
  name: string;
  friends: person list;
}

type room = {building: building}
and building = {rooms: room array}

(* type paramater *)
type ('a, 'b) t = ('a * 'b) ;;
let p : (string, int) t = ("hello", 123) ;; 

type ('a, 'b) either = Left of 'a | Right of 'b ;;
```
