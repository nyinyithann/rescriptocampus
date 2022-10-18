# Pipe

### Rescript

- pipe "->" is just a syntactic sugar not like "|>" which is an infix operator
- pipe "->" is for data-first APIs

```reasonml
// [ 2, 3, 1 ] cause JS.Array is designed for data-last APIs
[1]->Js.Array.concat([2, 3])->Js.log 

// [ 1, 2, 3 ] cause JS.Array2 is designed for data-first APIs
[1]->Js.Array2.concat([2, 3])->Js.log 
```

#### pipe-placeholder
```reasonml

let add = (x, y, z) => x + y + z
let addX = add(_, 2, 3)
let addY = add(1, _, 3)
let addZ = add(1, 2, _)
10->addX->Js.log // 15
10->addY->Js.log // 14
10->addZ->Js.log // 13

let addXY = add(_, _, 3)
10->addXY->Js.log // 23

let addXYZ = add(_, _, _)
100->addXYZ->Js.log // 300

open Belt
let filter = (f, arr) => {
  let r = []
  for i in 0 to Array.length(arr) - 1 {
    let item = Array.getExn(arr, i) 
    if f(item) {
        Belt.Array.push(r, item)
    }
  }
  r
}

let nums = [1, 2, 3, 4, 5, 9 , 10, 1001]
filter(x => mod(x, 2) > 0, nums)->Js.log

// using pipe-placeholder
nums -> filter(x => mod(x, 2) > 0, _ ) -> Js.log
```

#### with labeled-arguments
```reasonml
let add = (x, ~y, ~z, ()) => x + y + z
10 -> add(10,~y=_,~z=10, ())->Js.log // 30
10 -> add(10,~y=10,~z=_, ())->Js.log // 30
10 -> add(10,~y=_,~z=_, ())->Js.log // 30
10 -> add(_,l~y=_,~z=_, ())->Js.log // 30
() -> add(10,~y=10,~z=10, _)->Js.log // 30
```


