# Bind null or undefined return value to Option
#### JavaScript
```JavaScript
function getValue(key) {
  if (key) {
    return 'value';
  } else {
    return undefined;
  }
}
export { getValue };
```
#### Rescript
```reasonml
@module("./play") @return(nullable) external getValue: string => option<string> = "getValue"

/* usage */
let v = getValue("")
switch v {
  | Some(v') => Js.log(v')
  | None => Js.log("undefined")
}

type doc
type elm
@val external document: doc = "document"
@send @return(nullable) external getElementById: (doc, string) => option<elm> = "getElementById"

/* usage */
let element = getElementById(document, "lesson")
switch element {
    |Some(e) => Js.log(e)
    |None => Js.log("Not Found")
}
```
