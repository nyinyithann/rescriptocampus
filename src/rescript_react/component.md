# Component

A component is `('props) => React.element` or `React.component<'props>`

Component definition in [RescriptReact](https://github.com/rescript-lang/rescript-react/blob/v0.10.3/src/React.res)
```reasonml
type componentLike<'props, 'return> = 'props => 'return
type component<'props> = componentLike<'props, element>
```

### JSX component interface
- A component is a module with: 
  - `make : props => React.element`
  - `makeProps: 'a => props`
```reasonml
module Movie = {
  type props = {"title": string, "desc": string}
  
  @obj
  external makeProps: (~title: string, ~desc: string, ~children: React.element=?, unit) => props 
  = ""
  
  let make = (props: props) => {
    <div>
      <h1> {props["title"]->React.string} </h1>
      <p> {props["desc"]->React.string} </p>
    </div>
  }
}

@react.component
let make = () => {
  <div>
    <Movie title="Dark" desc="The best sifi movie." />
  </div>
}
```

### `@react.component` Decorator
- `@react.component` decorator helps to create component more easily
```reasonml
module Movie = {
  @react.component
  let make = (~title: string, ~desc: string) => {
    <div>
      <h1> {title->React.string} </h1>
      <p> {desc->React.string} </p>
    </div>
  }
}

@react.component
let make = () => {
  <div>
    <Movie title="Looper" desc="The best sifi movie." />
  </div>
}
```
No need to write `let make = (~title: string, ~desc: string, unit)` cause `@react.component` helps to add it.

