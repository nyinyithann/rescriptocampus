# Forwarding Refs

### Pass down via props (recommended)
```reasonml
@send external select: Dom.element => unit = "select"
@send external focus: Dom.element => unit = "focus"

module CoolInput = {
  @react.component
  let make = (~inputRef: ReactDOM.domRef) => {
    <div className="w-full border-[1px] border-300 rounded bg-100 p-2 text-lg">
      <input type_="text" ref={inputRef} className="w-full border-0 bg-50" />
    </div>
  }
}

@react.component
let make = () => {
  let inputRef = React.useRef(Js.Nullable.null)

  let onClick = _ => {
    switch inputRef.current->Js.Nullable.toOption {
    | Some(e) => select(e)
    | None => ()
    }
  }

  let focus = _ => {
    switch inputRef.current->Js.Nullable.toOption {
    | Some(e) => focus(e)
    | None => ()
    }
  }

  <div className="flex flex-col p-4 gap-2">
    <CoolInput inputRef={ReactDOM.Ref.domRef(inputRef)} />
    <button type_="button" className="p-1 bg-200" onClick={focus}> {"Focus"->React.string} </button>
    <button type_="button" className="p-1 bg-200" onClick> {"Select Text"->React.string} </button>
  </div>
}
```

### React.forwardRef (Not recommended, will be removed from React in future)
```reasonml
module FancyInput = {
  @react.component
  let make = React.forwardRef((~className=?, ~children, ref_) =>
    <div>
      <input
        type_="text"
        ?className
        ref=?{Js.Nullable.toOption(ref_)->Belt.Option.map(
          ReactDOM.Ref.domRef,
        )}
      />
      children
    </div>
  )
}

@send external focus: Dom.element => unit = "focus"

@react.component
let make = () => {
  let input = React.useRef(Js.Nullable.null)

  let focusInput = () =>
    input.current
    ->Js.Nullable.toOption
    ->Belt.Option.forEach(input => input->focus)

  let onClick = _ => focusInput()

  <div>
    <FancyInput className="fancy" ref=input>
      <button onClick> {React.string("Click to focus")} </button>
    </FancyInput>
  </div>
}
```
