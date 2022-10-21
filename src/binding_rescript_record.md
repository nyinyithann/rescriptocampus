# Bind using Rescript record

##### JavaScript 
```JavaScript
/* languages.js */
const rescript = {
  name: 'Rescript',
  type: 'FP',
  version: 10.2,
};

const ocaml = {
  name: 'OCaml',
  type: 'FP',
  version: 5.0,
};

const rust = {
  name: 'Rust',
  type: 'ML Family',
  version: 1.5,
};

export { rescript, ocaml, rust };
```
##### Rescript Binding
```reasonml
type lang = {
  name: string,
  @as("type") type_: string,
  version: float,
}
@module("./languages") external rescript: lang = "rescript"
@module("./languages") external ocaml: lang = "ocaml"
@module("./languages") external rust: lang = "rust"

/* usage */
rescript.name->Js.log
ocaml.name->Js.log
rust.name->Js.log
```
