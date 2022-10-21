# Polymorphic Variant (@unwrrap)
#### JavaScript
```JavaScript
/* play.js */
function config(option) {
  if (typeof option === 'string') {
    return `set ${option}`;
  }
  if (typeof option === 'number') {
    return `set ${option}`;
  }
  if (typeof option === 'object') {
    return `set ${option.option}`;
  }
  if (typeof option === 'function') {
    return `set ${option()}`;
  }

  throw new Error('unexpected value');
}

export { config };
```

#### Rescript Binding
```reasonml
/* usage */
type optType = {option: string}
@module("./play")
external config: @unwrap
[
  | #Int(int)
  | #String(string)
  | #Object(optType)
  | #Function(unit => string)
  | #Null(unit) /* this is just for testing error catching */
] => string = "config"

/* usage */
config(#Int(10))->Js.log
config(#String("ten"))->Js.log
config(#Object({option: "obj option"}))->Js.log
config(#Function(() => "func option"))->Js.log
try {
  config(#Null())->Js.log
} catch {
| Js.Exn.Error(obj) =>
  switch Js.Exn.message(obj) {
  | Some(e) => Js.log(e)
  | None => ()
  }
}
```
