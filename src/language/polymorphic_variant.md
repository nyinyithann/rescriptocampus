# Polymorphic Variant

##### Rescript
- explicit type declaration is optional
- type will be inferred automatically
- structural typing
- have leading hash e.g. `#A`
- `>` at the beginning of the variant type means the type is open to combination with other variant types
- `>` means lower bound, `<` means upper bound. If the same set of tags are both an upper and a lower bound, we end up with an exact polymorphic variant type, which has neither marker.

##### Basic
```reasonml
let b = #Red
let l = #"aria-hidden"
let x = #"I am ❌"
Js.log(b) // Red
Js.log(l) // aria-hidden
```

##### Type Declaration (optional)
```reasonml
type color = [#red | #green | #blue]
let r: color = #red
```
##### Inline
```reasonml
let show = (v: [ #int(int) | #float(float) | #string(string) ]) => {
  switch v {
  | #int(i) => Js.log(i)
  | #float(f) => Js.log(f)
  | #string(s) => Js.log(s)
  }
}
show(#float(1.1))
```

##### structual sharing
```reasonml
type bool_or_char = [#bool(bool) | #char(char)]
let bc: bool_or_char = #bool(true)

let display = x => {
  switch x {
  | #bool(b) => Js.log(b)
  | #char(c) => Js.log(c)
  | #unit => Js.log("unit")
  }
}
display(bc)
display(#unit)
display(#char('a'))
```

##### lower bound poly variant with array
```reasonml
let three = #Int(3)
let four = #Float(4.)
let nan = #Not_a_number
Js.log([three, four, nan])

// list is immutable, so both open & close poly variant are allowed
let lst: list<[> #Int(int) | #Float(float) | #Not_a_number]> = list{three, four, nan}
Js.log(lst)
let lst: list<[< #Int(int) | #Float(float) | #Not_a_number]> = list{three, four, nan}
Js.log(lst)

// Rescript won't compile the following line 
let arr: array<[> #Int(int) | #Float(float) | #Not_a_number]> = [three, four, nan] // compilation error


let arr: array<[< #Int(int) | #Float(float) | #Not_a_number]> = [three, four, nan]
Js.log(arr)
```

##### Combine Types and Pattern match
```reasonml
type abc = [#a | #b | #c]
type def = [#d | #e | #f]
let show = x => {
  switch x {
  | #...abc => Js.log("abc")
  | #...def => Js.log("def")
  }
}
show(#a)
show(#f)
```

##### Constraints lower bound
```reasonml
type basic_color<'a> = [> #Red | #Green | #Blue] as 'a
type advanced_color = basic_color<[#Red | #Green | #Blue | #Pink]>
let bc: basic_color<[> #Red | #Green | #Blue]> = #Blue
let ac: advanced_color = bc
Js.log(ac)
```

##### Constraints upper bound
```reasonml
type xyz<'t> = [< #A | #B | #C] as 't
type omega = xyz<[#A]>
let x: xyz<[< #A | #B | #C]> = #A
let o: omega = x
Js.log(o)
```

##### Subtyping
```reasonml
type choice = [ #Yes | #No | #Maybe ]
let yes = #Yes
let ch1 : choice = yes :> choice

let color : [> #Red ] = #Green
Js.log(color) // green
```

#### OCaml
[My note on OCaml poly-variant](https://github.com/nyinyithann/notes_on_ocaml/blob/main/notes/lang/polymorphic%20variants.ipynb)


