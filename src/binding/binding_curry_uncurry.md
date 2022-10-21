# Curry and Uncurry

#### uncurry syntax
```reasonml
type timerId
@val external setTimeOut: (((. unit) => unit), int) => timerId = "setTimeOut"

setTimeOut((.) => Js.log("hello"), 100)->Js.log
```

#### extra solution (@uncurry)
- you're using external
- the external function takes in an argument that's another function
- you want the user not to need to annotate the call sites with the dot


```reasonml
@val external setTimeOut:(@uncurry (unit => unit), int) => timerId = "setTimeOut"

@send external keep: (array<int>, @uncurry (int => bool)) => array<int> = "filter"
[1,2,3]->keep(x => mod(x,2) === 0)->Js.log
```


