# Option, Null, Undefined

#### option
- Use option type to deal with nonexistent value
- Use mostly [Js.Belt.Option](https://rescript-lang.org/docs/manual/latest/api/belt/option), 
  or [Js.Option](https://rescript-lang.org/docs/manual/latest/api/js/option) 

#### Interoperate with JS `undefined` and `null`

- **Never, EVER, pass a nested option value (e.g. Some(Some(Some(5)))) into the JS side.**
- **Never, EVER, annotate a value coming from JS as `option<'a>`. Always give the concrete, non-polymorphic type.**

- **Use `Js.Nullable.null` or `Js.Nullable.undefined` if expecting `null` or `undefined` from JS side**
```reasonml
// consuming JS null 
@module("MyConstant") external myId: Js.Nullable.t<string> = "myId"

// passing Nullable from Rescript to JS
@module("MyIdValidator") external validate: Js.Nullable.t<string> => bool = "validate"
let personId: Js.Nullable.t<string> = Js.Nullable.return("abc123")
let result = validate(personId)

```
