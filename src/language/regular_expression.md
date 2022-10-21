# Regular Expression

#### Rescript
- ReScript regular expressions compile cleanly to their JavaScript counterpart:
- [Js.Re Doc](https://rescript-lang.org/docs/manual/latest/api/js/re)
- [Js.Re Source](https://github.com/rescript-lang/rescript-compiler/blob/master/jscomp/others/js_re.ml)

```reasonml
let re = %re("/^ryan.*myat$/i") // starts with ryan .. ends with myat
Js.log(Js.Re.test_(re, "Ryanzanthumyat")) // true
```

#### OCaml

```ocaml
(* using Re package *)
let re = Re.Perl.re {|^ryan.*myat$|} |> Re.no_case |> Re.compile ;;
Re.execp re "RyanzanthumyaT" (* true *)
```
