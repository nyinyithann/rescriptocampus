# Optional Arguments(Rescript)

- labeled arguments can be made optional
- optional arguments can be omitted when calling the function
- if omitted, the optional argument is set `None`
- if provided, the optional argument will be wrapped with a `Some`
- whenever you have an optional argument, you need to ensure that there's also at least one positional argument (aka non-labeled, non-optional argument) after it. If there's none, provide a dummy unit (aka ()) argument.


#### Optional arguments
```reasonml
open Js
let concat = (~sep=?, x, y) => {
  let sep = switch sep {
    | Some(s) => s
    | None => ""
  }
  x ++ sep ++ y
}
concat(~sep=",", "hello", "world")->log // hello,world
concat("hello", "world", ~sep=",")->log // hello,world
```

#### Need to add "()" if optional argument is the last
```reasonml
open Js
let concat = (x, y, ~sep=?, ()) => {
  let sep = switch sep {
  | Some(s) => s
  | None => ""
  }
  x ++ sep ++ y
}
concat(~sep=":", "hello", "world", ())->log // hello:world
concat("hello", "world", ~sep=":", ())->log // hello:world
```

#### With function type signature and paramater type annotation
```reasonml
open Js
let concat: (string, string, ~sep: string=?, unit) => string = (
  x,
  y,
  ~sep: option<string>=?,
  (),
) => {
  let sep = switch sep {
  | Some(s) => s
  | None => ""
  }
  x ++ sep ++ y
}
concat("hello", "world", ~sep="-", ())->log // hello-world
```

#### Passing value of option type to optional paramater
```reasonml
open Js
let separator = Some("/")
concat("hello", "world", ~sep=?separator, ())->log // hello/world
let sep = None
concat("hello", "world", ~sep?, ())->log // helloworld
```

#### Optioanl paramater with default value
if default value is provided, the optional argument is not wrapped in an option type.
```reasonml
open Js
let concat = (~sep=", ", x, y) => x ++ sep ++ y
concat("hello", "world")->log // hello, world
concat("hello", "world", ~sep="<>")->log // hello<>world
```

#### Partial Application
```reasonml
open Js
let concat = (x, y, ~sep=?, ()) => {
  let sep = switch sep {
  | Some(s) => s
  | None => ""
  }
  x ++ sep ++ y
}

let concatP = concat("Hello")
concatP("World", ~sep="~", ())->log
let concatP = concat("Hello", "World")
concatP(~sep="@", ())->log
let concatP = concatP(~sep="/\\")
concatP()->log
let concatP = concat(~sep="&")
concatP("Hello", "World", ())->log

let test: (
  ~x: int=?,
  ~y: int=?,
  unit,
  ~z: int=?,
  unit,
) => (option<int>, option<int>, option<int>) = (~x=?, ~y=?, (), ~z=?, ()) => (x, y, z)
test(~z=3)()()->log // [ undefined, undefined, 3]
test()()->log // [ undefined, undefined, undefined ]
test(~x=1, ~y=2, (), ())->log // [ 1, 2, undefined ]
test(~y=2, (), ~z=3, ())->log // [ undefined, 2, 3 ]
test((), (), ~y=2, ~x=1, ~z=3)->log // [ 1, 2, 3 ]
```
