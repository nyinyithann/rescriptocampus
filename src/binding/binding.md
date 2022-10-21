# Binding

`external` is like a let binding, but:
- The right side of = isn't a value; it's the name of the JS value you're referring to.
- The type for binding is mandatory.
- Can only exist at the top level of a file or module.

[Binding to JS global functions - Js.Global](https://rescript-lang.org/docs/manual/latest/api/js/global)

#### Refs
- [rescript-js](https://github.com/bloodyowl/rescript-js)
- [rescript-webapi](https://github.com/tinymce/rescript-webapi)

#### Illegal identifier
Illegal identifiers can be created by prefixing `\`.
```reasonml
let \"orange 🍊" = "🍊"
\"orange 🍊"->Js.log

type element = {
  \"aria-label": string
}

let myElement = {
  \"aria-label": "close"
}

let label = myElement.\"aria-label"

let calculate = (~\"Props") => {
  \"Props" + 1
}
```

