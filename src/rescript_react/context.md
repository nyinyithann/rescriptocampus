# Context
- Context provides a way to share values between components in a component tree
- Drawback: it renders all the components under the provider each time the context state changes
    - Should use `React.memo` for components within the provider

```reasonml
module FunContext = {
  let context = React.createContext("")

  module Provider = {
    let provider = React.Context.provider(context)
    @react.component
    let make = (~value, ~children) => {
      React.createElement(provider, {"value": value, "children": children})
    }
  }
}

module Component1 = {
  @react.component
  let make = () => {
    let fun = React.useContext(FunContext.context)
    <div className="flex flex-col items-center justify-center">
      <div> {Js.Date.now()->React.float} </div>
      {React.string(fun)}
    </div>
  }
  let make = React.memo(make) // Foo won't render when provider state changes
}
module Component2 = {
  @react.component
  let make = () => {
    <div className="flex flex-col items-center justify-center">
      <div> {Js.Date.now()->React.float} </div>
      <Component1 />
    </div>
  }
  let make = React.memo(make) // Foo won't render when provider state changes
}
module Component3 = {
  @react.component
  let make = () => {
    <div className="flex flex-col items-center justify-center">
      <div> {Js.Date.now()->React.float} </div>
      <Component2 />
    </div>
  }
  let make = React.memo(make) // Component 3 will be rerendered cause of the state changes
}

module Foo = {
  @react.component
  let make = () => {
    <div className="flex items-center justify-center">
      <span> {"Foo "->React.string} </span>
      <div> {Js.Date.now()->React.float} </div>
    </div>
  }
  let make = React.memo(make) // Foo won't render when provider state changes
}

@react.component
let make = () => {
  let (fun, setFun) = React.useState(_ => "fun")
  <FunContext.Provider value={fun}>
    <div className="flex flex-col items-center justify-center">
      <Component3 />
      <button type_="button" className="bg-300 p-2" onClick={_ => setFun(prev => prev ++ prev)}>
        {"Have Fun"->React.string}
      </button>
    </div>
    <Foo />
  </FunContext.Provider>
}
```


