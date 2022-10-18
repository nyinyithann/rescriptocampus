# Patterns

#### Variable pattern: binding the name to the value
```reasonml
let (x, y, z) = (1, 2, 3)
let (x, _, _) = (1, 2, 3)
let is_sorted = nums => {
  switch nums {
  | (x, y, z) if (x <= y && y <= z) || (x >= y && y >= z) => true
  | _ => false
  }
}
is_sorted((1, 2, 3))->Js.log
is_sorted((3, 2, 1))->Js.log
is_sorted((3, 11, 1))->Js.log
```

#### Constant pattern
```reasonml
exception Invalid_argument(string)
let isOn = x => {
  switch x {
  | "On" => true
  | "Off" => false
  | _ => raise(Invalid_argument("isOn"))
  }
}
isOn("On")->Js.log
```

#### Alias pattern
```reasonml
let sortPair = ((x, y) as p) =>
  if x < y {
    p
  } else {
    (y, x)
  }
sortPair((1, 2))->Js.log

let greaterOne = ((x1, y1) as p1, (x2, y2) as p2) =>
  if x1 > x2 || y1 > y2 {
    p1
  } else {
    p2
  }
greaterOne((11, 2), (2, 2))->Js.log

type rect = {width: float, height: float}
let r = {width: 1.1, height: 2.2}
let {width} = r
let {width: w} = r
```

#### Or pattern
```reasonml
let isVowel = v =>
  switch v {
  | 'a' | 'e' | 'i' | 'o' | 'u' => true
  | _ => false
  }
isVowel('a')->Js.log

let rects = [{width: 1.1, height: 2.2}, {width: 10.1, height: 2.2}, {width: 2.1, height: 2.2}]
let smallRects = rects => {
  rects->Belt.Array.keep(x =>
    switch x {
    | {width: 1.1 | 2.1} => true
    | _ => false
    }
  )
}
smallRects(rects)->Js.log

rects
->Belt.Array.keep(x => {
  switch x {
  | {width: w} if w > 10. => true
  | _ => false
  }
})
->Js.log
```

#### Variant pattern
```reasonml
type kg = Kg(float)
let weight = Kg(100.)
let Kg(w) = weight
let test = (Kg(w)) => Js.log(w)

type rec expr = Int(int) | Add(expr, expr)
let rec eval = expr =>
  switch expr {
  | Int(i) => i
  | Add(e1, e2) => eval(e1) + eval(e2)
  }
eval(Add(Int(10), Int(20)))->Js.log

type either<'a, 'b> = Left('a) | Right('b)
let left = Left(10)
let Left(l) | Right(l) = left
let choice = (Left(x) | Right(x)) => Js.log(x)
choice(Right(100))
```

#### Polymorphic variant pattern
```reasonml
let check = s =>
  switch s {
  | #Ok(x) => x
  | #Error(e) => e
  }
check(#Ok("hello"))->Js.log
check(#Error(404))->Js.log
```

#### Polymorphic variant abbreviation pattern
```reasonml
type color = [#Red(int) | #Green(int) | #Blue(int)]
type more_color = [color | #Pink(int) | #Gray(int)]
type much_more_color = [more_color | #Slate(int)]

let display = c =>
  switch c {
  | #...color => Js.log("Basic Color ")
  | #...more_color => Js.log("Advanced Color")
  | #...much_more_color => Js.log("Fantastic Color")
  }
display(#Green(10))
display(#Slate(10))
display(#Gray(10))
```

#### tuple pattern
```reasonml
let choose = ((0, x, _) | (_, _, x)) => x
choose((0, 2, 3))->Js.log // 2
choose((1, 2, 3))->Js.log // 3
let choose = ((x, None) | (_, Some(x))) => x
choose((1, None))->Js.log // 1
choose((1, Some(10)))->Js.log // 10
```

#### record pattern
```reasonml
type person = {name: string}
let blonde = {name: "Blondie"}
let tuco = {name: "Tuco"}
let eyes = {name: "Eyes"}
type gunslinger =
  | Good(person)
  | Bad(person)
  | Ugly(person)
  | TheJazz({name: string})

let who = gs =>
  switch gs {
  | Good({name: n}) => Js.log(n)
  | Bad({name: n}) => Js.log(n)
  | Ugly({name: n}) => Js.log(n)
  | TheJazz({name: "Jazz" | "Taltos"} as j) => Js.log(j.name)
  | _ => Js.log("NPC")
  }
who(TheJazz({name: "Jazz"}))
who(TheJazz({name: "Taltos"}))
who(Good(blonde))

```
#### Optional record field pattern
```reasonml
type person = {
    name: string,
    nickName?: string,
    age: float,
}
let p1 = { name : "jack", age ; 14 }
let hasNickName = switch p1 {
	| {nickName: ?None} => false
	| {nickName: ?Some(_)} => true
}
```

#### array pattern
```reasonml
let arr = Belt.Array.makeBy(3, x => Belt.Array.makeBy(3, _ => (x + 1) * 2))
let dig = arr =>
  switch arr {
  | [[x, _, _], [_, y, _], [_, _, z]] => (x, y, z)
  | _ => (0, 0, 0)
  }
dig(arr)->Js.log
```

#### range pattern
```reasonml
let classify = ch =>
  switch ch {
  | 'A' .. 'Z' => "uppercase"
  | 'a' .. 'z' => "lowercase"
  | '0' .. '9' => "digit"
  | _ => "other"
  }
classify('H')->Js.log
classify('3')->Js.log
```

#### lazy pattern
```reasonml
let l = Lazy.from_fun(() => 1000 * 100)
let lazy r = l
Js.log(r)

switch Lazy.from_fun(() => 1000 * 1000) {
| lazy l => Js.log(l)
}

switch Some(Lazy.from_fun(() => 5000 * 1000)) {
| Some(lazy l) => Js.log(l)
| None => Js.log(0)
}
```

#### exception pattern
```reasonml
switch Belt.List.headExn(list{}) {
| exception _ => Js.log("empty error")
| n => Js.log(n)
}
```

#### module destructuring pattern
```reasonml
module M = {
    type t = { name : string}
    let godot = { name : "godot"}
}
let gname = ({M.name : n}) => n
gname(M.godot)->Js.log
```

### OCaml
[My OCaml Notes here](https://github.com/nyinyithann/notes_on_ocaml/blob/main/notes/lang/patterns.ipynb)
