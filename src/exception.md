# Exception
#### Rescript
```reasonml
/* rescript exception */
exception Empty(string)

type rec series<'a> = [#Nil | #Cons('a, series<'a>)]

let getHeadExn = s => {
  switch s {
  | #Nil => raise(Empty("list is empty"))
  | #Cons(h, _) => h
  }
}

let showFirstItem = s => {
  try {
    let hd = getHeadExn(s)
    Js.log(hd)
  } catch {
  | Empty(e) => Js.log(e)
  }
}

let s = #Cons(0, #Cons(1, #Cons(2, #Cons(3, #Nil))))
showFirstItem(s) // 0
showFirstItem(#Nil) // list is empty

/* exception can be pattern-matched */
switch getHeadExn(#Nil) {
| #Cons(h, _) => Js.log(h)
| exception Empty(e) => Js.log(e)
}
```

#### Catching Rescript Exception from JS
##### Raising an exception from Rescript
```reasonml
exception BadArgument({myMessage: string})

let myTest = () => {
  raise(BadArgument({myMessage: "Oops!"}))
}
```
##### Catching it from JavaScript
```javascript
// after importing `myTest`...
try {
  myTest()
} catch (e) {
  console.log(e.myMessage) // "Oops!"
  console.log(e.Error.stack) // the stack trace
}
```

#### OCaml Exception
```OCaml
exception Empty of string ;;
type 'a series = [ `Nil | `Con of 'a * 'a series ] ;;

let se = `Con (1, `Con(2, `Con(3, `Con (4, `Con (5, `Nil))))) ;; 

let hd = function
    | `Nil -> raise (Empty "list is empty") 
    | `Con (h, _) -> h ;;  

let show_hd s =
  try
    let fst = hd s in
    print_int fst
  with
   | Empty e -> print_string e ;;
   
show_hd se ;;
show_hd `Nil ;;

match hd `Nil with | `Con(h, _) -> print_int h | exception Empty e -> print_string e ;;
```
