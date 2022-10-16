# Rescript Function Cheatsheet

#### Anonymous function
```reasonml
(x, y) => x + y 
((x, y) => x + y)(1, 2)->Js.log // 3

/* with type annotation */
(x: int, y: int): int => x + y 
((x: int, y: int): int => x + y)(1, 2)->Js.log // 3
```

#### Bind a function to a name
```JavaScript
let add = (x, y) => x + y
add(1, 2)->Js.log

/* with function signature */
let add: (int, int) => int = (x, y) => x + y
add(1, 2)->Js.log

/* with paramater type annotation */
let add = (x: int, y: int): int => x + y
add(1, 2)->Js.log 

/* with both function signature and paramater type annotation */
let add: (int, int) => int = (x: int, y: int): int => x + y
add(1, 2)->Js.log
```

#### Labeled Arguments
```JavaScript
let add = (~first, ~second) => first + second
add(~first=2, ~second=2)->Js.log
add(~first=(2: int), ~second=(2: int))->Js.log

/* with punning */
let first = 100
let second = 200
add(~first, ~second)->Js.log
add(~first: int, ~second: int)->Js.log

/* with function signature */
let add: (~first: int, ~second: int) => int = (~first, ~second) => first + second
add(~first=2, ~second=2)->Js.log

/* with paramater type annotation */
let add = (~first: int, ~second: int): int => first + second
add(~first=2, ~second=2)->Js.log

/* with both function signature and paramater type annotation */
let add: (~first: int, ~second: int) => int = (~first: int, ~second: int): int => first + second
add(~first=2, ~second=2)->Js.log
```

#### Labeled Arguments with alias
```JavaScript
let add = (~first as x, ~second as y) => x + y
add(~first=2, ~second=2)->Js.log

/* with function signature */
let add: (~first: int, ~second: int) => int = (~first as x, ~second as y) => x + y
add(~first=2, ~second=2)->Js.log

/* with paramater type annotation */
let add = (~first as x: int, ~second as y: int): int => x + y
add(~first=2, ~second=2)->Js.log

/* with both function signature and paramater type annotation */
let add: (~first: int, ~second: int) => int = (~first as x: int, ~second as y: int): int => x + y
add(~first=2, ~second=2)->Js.log
```

#### labeled arguments with default value
```JavaScript
let add = (~first=111, ~second=222, ()) => first + second
add()->Js.log
let add = (~first as x=11, ~second as y=22, ()) => x + y
add()->Js.log
```

#### Optional arguments
```JavaScript
let bump = (~step=?, x) =>
  switch step {
  | Some(s) => x + s
  | None => x
  }
bump(~step=10, 1)->Js.log
bump(~step=(10: int), 1)->Js.log
bump(~step=?Some(111), 1)->Js.log
bump(~step=?(Some(111): option<int>), 1)->Js.log
bump(~step=?None, 1)->Js.log

/* with signature and type annotation */
let bump: (~step: int=?, int) => int = (~step: option<int>=?, x: int): int =>
  switch step {
  | Some(s) => x + s
  | None => x
  }
bump(~step=10, 1)->Js.log
bump(~step=(10: int), 1)->Js.log
bump(~step=?Some(111), 1)->Js.log
bump(~step=?(Some(111): option<int>), 1)->Js.log
bump(~step=?None, 1)->Js.log

/* with alias */
let bump = (~step as s=?, x) =>
  switch s {
  | Some(i) => x + i
  | None => x
  }
bump(~step=11, 1)->Js.log
bump(~step=(11: int), 1)->Js.log

/* with punning */
let step = 1111
bump(~step, 1)->Js.log
let step = Some(1111)
bump(~step?, 1)->Js.log
```
