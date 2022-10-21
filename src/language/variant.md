# Variant

#### Rescript
```reasonml
type rec json =
  | Assoc(list<(string, json)>)
  | Bool(bool)
  | Float(float)
  | Int(int)
  | List(list<json>)
  | String(string)
  | Null

let boy = Assoc(list{("name", String("Ryan")), ("age", Float(6.5))})
```

##### Paramaterised Variant
```reasonml
type maybe<'a> = Nothing | Just('a)

// list
type rec list<'a> = Nil | Cons('a, list<'a>)

let lst = Cons(1, Cons(2, Cons(3, Nil)))
let length = l => {
  let rec loop = (l, acc) => {
    switch l {
    | Nil => acc
    | Cons(_, t) => loop(t, acc + 1)
    }
  }
  loop(l, 0)
}
Js.log(length(lst)) // 3

// peano number
type rec peano = Zero | Succ(peano)

let count = p => {
  let rec loop = (p, a) => {
    switch p {
    | Zero => a
    | Succ(t) => loop(t, a + 1)
    }
  }
  loop(p, 0)
}

Js.log(count(Succ(Succ(Succ(Succ(Zero)))))) // 4
```

##### Variant with inline vs free standing records
```reasonml
type circle = {radius: float, x: float, y: float}
let c = {radius: 1.1, x: 10., y: 20.2}
type shape =
  | Square(float)
  | Rectangle({width: float, height: float})
  | Circle(circle)
let display_shape = s => {
  open Js.Float
  switch s {
  | Circle({radius, x, y}) =>
    Js.log(
      `radius:${toString(radius)}, x:${toString(x)}, y:${toString(y)}`,
    )
  | Square(x) => Js.log(`Square of ${toString(x)}`)
  | Rectangle({width, height}) =>
    Js.log(`width:${toString(width)}, height:${toString(height)}`)
  }
}
display_shape(Rectangle({width: 1.1, height: 2.2}))
display_shape(Circle(c))

/* 
 Limitation of inline record.
 The following code will get compile time error - 
 'This form is not allowed as the type of the inlined record could escape.'
*/
let get_shape = s => {
  switch s {
  | Rectangle(r) => Some(r)
  | _ => None
  }
}
```

##### Variant with multiple arguments vs tuple
```reasonml
type point = Point(float, float)
let p = Point(1.1, 2.2)
let Point(x, y) = p

/* varint with tuple can be grabbed as a whole */
type point = Point((float, float))
let p = Point((1.1, 2.2))
let Point(p') = p
Js.log(p') // [ 1.1, 2.2]
```

##### OCaml
[My Note Here](https://github.com/nyinyithann/notes_on_ocaml/blob/main/notes/lang/variants.ipynb)
