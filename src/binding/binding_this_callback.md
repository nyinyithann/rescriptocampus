# Modeling this-based callbacks
#### JavaScript
```JavaScript
x.onload = function(v) {
  console.log(this.response + v)
}
```
#### Rescript Binding
```reasonml
type x
@val external x: x = "x"
@set external setOnload: (x, @this ((x, int) => unit)) => unit = "onload"
@get external resp: x => int = "response"
setOnload(x, @this ((o, v) => Js.log(resp(o) + v)))
```
