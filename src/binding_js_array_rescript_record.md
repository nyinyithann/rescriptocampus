# Bind JS array to Rescript record

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

let langs = [ocaml, rust, rescript];

export { langs };

```
##### Rescript Binding
```reasonml
type lang = {
  name: string,
  @as("type") type_: string,
  version: float,
}

type langMap = {
  @as("0") ocaml: lang,
  @as("1") rust: lang,
  @as("2") rescript: lang,
}

@module("./languages") external langs: langMap = "langs"

/* usage */
langs.ocaml.name->Js.log
langs.rust.name->Js.log
langs.rescript.name->Js.log
```
