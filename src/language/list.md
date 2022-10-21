# List

### Rescript
- immutable
- fast at prepending items
- fast at getting the head
- slow at everything else

- **Use Array for**
    - accessing random element
    - better interop with JavaScript
    - better memory usage and performance

```reasonml
let numList = list{1, 2, 3}
let numList2 = list{0, ...numList}

/* multiple spread is not allowed */
let numList2 = list{0, numList, ...numList2}

let foldLeft = (lst, acc, f) => {
  let rec loop = (l, acc) => {
    switch l {
    | list{} => acc
    | list{h, ...t} => loop(t, f(acc, h))
    }
  }
  loop(lst, acc)
}

let nums = Js.List.init(10, (. x) => x + 1)
foldLeft(nums, 0, (x, y) => x + y)->Js.log

let letters = Js.List.init(26, (. x) => String.make(1, Char.chr(x + 65)))
foldLeft(letters, "", (x, y) => x ++ "," ++ y)->Js.log

let foldRight = (lst, acc, f) => {
  let rec loop = (l, acc) => {
    switch l {
    | list{} => acc
    | list{h, ...t} => f(h, loop(t, acc))
    }
  }
  loop(lst, acc)
}
foldRight(letters, "", (x, y) => x ++ "," ++ y)->Js.log
```
