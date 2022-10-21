# JSON

#### Parsing JSON string via binding to JSON.parse (unsafe)
Convenient but dangerous cuase not guarantee the data is correctly shaped or even syntactically valid!
```reasonml

type lang = {
  name: string,
  @as("type") type_: string,
  version: float,
}
@val @scope("JSON") external parseToLang: string => lang = "parse"

let l: lang = parseToLang(`{"name" : "rescript", "type_" : "fp", "version" : 10.1}`)
l->Js.log // output: {name: 'rescript', type_: 'fp', version: 10.1}
l.name->Js.log // output : rescript

/* NOTE: It's not type safe. lang doesn't have name_ or version_ */   
let l: lang = parseToLang(`{"name_" : "rescript", "type_" : "fp", "version_" : 10.1}`)
l->Js.log /* this gives {name_: 'rescript', type_: 'fp', version_: 10.1}

/* but this will give you undefined */
l.name->Js.log 
```

#### JSON.stringify
```reasonml
let re = Js.Json.stringifyAny({name : "rescript", type_ : "fp", version: 10.1})
re->Js.log
```

#### My favourite JSON encode/decode lib
[https://github.com/glennsl/rescript-json-combinators](https://github.com/glennsl/rescript-json-combinators)
