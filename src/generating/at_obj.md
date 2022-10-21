# @obj
Use `@obj` on an external binding to create a function that, when called, will evaluate to a JS object with fields corresponding to the function's parameter labels.

```reasonml
@obj
external route: (
  ~\"type": string,
  ~path: string,
  ~action: list<string> => unit,
  ~options: {..}=?,
  unit,
) => _ = ""

/* usage */

let homeRoute = route(~\"type"="GET", ~path="/", ~action=_ => Js.log("Home"), ())
homeRoute->Js.log // {type: 'GET', path: '/', action: ƒ}
```
