# @deriving(accessors)

### `@deriving(accessors)` with variants
- create accessor functions for variant constructors 
- payload-less constructors generate plain integers

```reasonml
@deriving(accessors)
type rec json =
  | Bool(bool)
  | Float(float)
  | Int(int)
  | String(string)
  | Null
  | Undefined

/* usage */
let b : json = bool(true)
b->Js.log // {TAG: 0, _0: true}
let f : json = float(1.1)
f->Js.log // {TAG: 1, _0: 1.1}
let i : json = int(10)
i->Js.log // {TAG: 2, _0: 10}
let s : json = string("hello")
s->Js.log // {TAG: 3, _0: 'hello'}
null->Js.log // 0 
undefined->Js.log // 1 
```

### `@deriving(accessors)` with records
- create accessors with field names
```reasonml
@deriving(accessors)
type lang = {
  name: string,
  \"type": string,
  version: float,
}

let langs = [
    { name: "ReScript", \"type" : "fp", version : 10.2},
    { name: "OCaml", \"type" : "fp", version : 5.0}
]

/* usage */
Belt.Array.map(langs, name) -> Js.log // ['ReScript', 'OCaml']
Belt.Array.map(langs, \"type") -> Js.log // ['fp', 'fp']
Belt.Array.map(langs, version) -> Js.log // [10.2, 5.0]
```
