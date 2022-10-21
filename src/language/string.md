# String
#### Rescript
- [Js.String2 Doc](https://rescript-lang.org/docs/manual/latest/api/js/string-2)
- [Js.String2 Source](https://github.com/rescript-lang/rescript-compiler/blob/master/jscomp/others/js_string2.ml)
```reasonml
let name = "Ryan"

/* string concatenation */
let name = name ++ " Zan"

/* string interpolation */
let greeting1 = `Hello ${name}`
let greeting2 = j`Hola $name`

/* multiline string */
let greeting3 = `hello
${name},
sup?`

/* Js.String2 module to deal with String type */
let replaced = "testing".Js.String2.replate("t", "R")
let len = Js.String2.length("abc")
let sub = "hello world"->Js.String2.substring(~from=0, ~to_=5) // hello
```
#### OCaml
```OCaml
let name = "Ryan" ;;

(* string concatenation *)
let name = name ^ " Zan" ;;

(* string interpolation *)
let greeting = Printf.sprintf "hello, %s" name ;;

(* multiline string *)
let greeting3 = {|hello
Baloo
sup?|} ;;
(* same as *)
let greeting3 = "hello\nBaloo\nsup?"

(* wrapped long line *)
let wrapline = "hello \
Baloo \
sup?" ;;
(* same as *)
let wrapline = "hello Baloo sup?"

(* String, StringLabels module to deal with string *)
String.sub "Hello World" 0 5 (* hello *)
```
