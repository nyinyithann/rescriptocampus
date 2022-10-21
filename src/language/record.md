# Record

#### Rescript
- Immutable by default
- Have fixed fields - not extensible, 
- Nominal typing

##### Type declaration, mutable/immutable update, destructuring
```reasonml
module Model = {
  type person = {
    name: string,
    age: float,
  }
}

let ryan: Model.person = {name: "Ryan", age: 6.5}
let zan = {Model.name: "Zan", age: 6.5}

// destructuring
let show = ({Model.name: name, age}) => {
  Js.log(j`Name: $name, Age : $age`)
}

// immutable update
let joe = {...zan, name: "Joe"}
Js.log(joe)

// mutable update
module MutableModel = {
  type person = {
    name: string,
    mutable age: float,
  }
}
let ryan: MutableModel.person = {name: "Ryan", age: 6.5}
ryan.age = 7.
```

##### Optional record fields
```reasonml
module OpModel = {
  type person = {
    name: string,
    nickName?: string,
    age: float,
  }
}

// None , if optional field is not set
let p1: OpModel.person = {name: "Ryan", age: 6.5}
Js.log(p1.nickName == None) // true

// use ? to set value
let p1: OpModel.person = {name: "Ryan", nickName: ?Some("Horn"), age: 6.5}
Js.log(p1.nickName) // Horn

// no need to use ? in immutable update
let p2 = {...p1, nickName: "kcin"}
Js.log(p2.nickName) // kcin

// if pattern match directly on optional record field, it's an optional
let hasNickName = switch p2.nickName {
	| Some(_) => true
	| None => false
}
Js.log(hasNickName) // true

// if matching on the field as part of general record structure, it's non-optional value
let nick = switch p2 {
	| {nickName: n} if String.length(n) > 0 => n
	| _ => ""
}
Js.log(nick) // "kcin"

// check if optional record field has value or not
let hasNickName = switch p2 {
	| {nickName: ?None} => false
	| {nickName: ?Some(_)} => true
}
Js.log(hasNickName) // true

// destructuring
let show = ({OpModel.name: name, age, _}) => {
  Js.log(j`=> { Name: $name, Age : $age }`)
}
show(p2) // => { Name: Ryan, Age: 6.5 }

// paramaterized record
module ParamaterizedModel = {
  type point<'a> = {x: 'a, y: 'a}
}
let p1: ParamaterizedModel.point<int> = {
  x: 1,
  y: 2,
}
Js.log(p1) // { x : 1, y : 2}
```

##### OCaml
[My Note on OCaml record](https://github.com/nyinyithann/notes_on_ocaml/blob/main/notes/lang/record.ipynb)<br/>
OCaml doesn't have optional record field feature.

```ocaml
type car = {
  mutable color : string ;
  mutable weight : float ;
  kind : string ;
} ;;

let c1 = { color = "black" ; weight = 100.; kind = "sport"} ;;

let c2 = { c1 with color = "pink"} ;;

let show { color = c; weight = w; _ } = Printf.sprintf "color=%s wight=%F" c w ;;
show c1 ;;
show c2 ;;

(* mutate color field *)
c1.color <- "blue" ;;
show c1 ;;
```
