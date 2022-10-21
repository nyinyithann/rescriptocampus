# JS Exception
- [Js.Exn Doc](https://rescript-lang.org/docs/manual/latest/api/js/exn)
- [Js.Exn Source](https://github.com/rescript-lang/rescript-compiler/blob/master/jscomp/others/js_exn.ml)

#### Catching a JS Exception in Rescript
```reasonml
@new external make: float => Js.Array2.t<int> = "Array"
try {
  let a = make(111111111111111111111111111.1)
} catch {
| Js.Exn.Error(obj) =>
  switch Js.Exn.message(obj) {
  | Some(e) => Js.log(e)
  | None => Js.log("No message")
  }
}
// Invalid array length
```

#### Raise a JS Exception from Rescript
##### Raising from Rescript site
```reasonml
let myTest = () => {
  Js.Exn.raiseError("Hello!")
}
```

##### Catching it from JS side
```reasonml
// after importing `myTest`...
try {
  myTest()
} catch (e) {
  console.log(e.message) // "Hello!"
}
```

