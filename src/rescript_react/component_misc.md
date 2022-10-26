# Misc

### Optional Props
```reasonml
// Greeting.res
@react.component
let make = (~name: option<string>=?) => {
  let greeting = switch name {
    | Some(name) => "Hello " ++ name ++ "!"
    | None => "Hello stranger!"
  }
  <div> {React.string(greeting)} </div>
}

let name = Some("Andrea")

<Greeting ?name /> // <== just ?name
```

### Special Props `key` and `ref`
- `key` and `ref` are special props, cannot define them like `~key` or `~ref`

### Invalid Prop Names
- Reserved keywords like `type` should be used like `type_`
- `aria-*` should be like `ariaLabel`
- `data-` attributes can be added using `React.cloneElement`

### Children
`children` is treated as a `React.Element`.
#### Component that must have children
```reasonml
module Comp = {
 @react.component
 let make = (~children: React.element) => { ...... }
}
```

#### Component that doesn't have children
```reasonml
module Comp = {
 @react.component
 let make = () => { ...... }
}
```
#### Component with optional children
```reasonml
module Comp = {
 @react.component
 let make = (~children: option<React.element>=?) => { ...... }
}
```

### Component Naming
```reasonml
// File.res

// will be named `File` in dev tools
@react.component
let make = ...

// will be named `File$component` in dev tools
@react.component
let component = ...

module Nested = {
  // will be named `File$Nested` in dev tools
  @react.component
  let make = ...
};
```

