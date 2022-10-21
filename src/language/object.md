# Object
##### Rescript
- Structural typing
- No type declaration needed
- Not supporting updates unless it comes from JS site
- No support for pattern matching

```reasonml
// optional type declaration
type person = {"name": string, "age": int}
let ryan = {"name": "Ryan", "age": 6.5}
Js.log(ryan)
Js.log(ryan["age"])

// spread object type but not object values
type point2D = {"x": float, "y": float}
type pooint3D = {...point2D, "z": float}

// binding to Dom
@val external document : 'a = "document"
let loc = document["location"]
let href = loc["href"]
```

##### OCaml
- [RealworldOCaml Chapter](https://dev.realworldocaml.org/objects.html)
- [My notes on OCaml Object](https://github.com/nyinyithann/notes_on_ocaml/blob/main/notes/lang/objects.ipynb)

```ocaml
let ryan = object
    val name : string = "Ryan"
    val mutable age : float = 6.5
    method get_age = age
    method set_age n = age <- n
    method to_string = Printf.sprintf "Name = Ryan, Age = %f" age
end ;;

let show o = print_string o#to_string ;;
show ryan ;;
```
