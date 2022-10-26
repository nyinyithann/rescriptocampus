# Refs and the DOM

`React.ref: type t<'value> = { mutable current: 'value }`

When to use Refs:
- Managing state that should not trigger any re-render.
- Managing focus, text selection, or media playback.
- Triggering imperative animations.
- Integrating with third-party DOM libraries.

### Managing state that should not trigger an re-render
- clicking will not update `click_count` span althought it updates document title.
```reasonml
@val external document: Dom.element = "document"
@set external setTitle: (Dom.element, string) => unit = "title"

@react.component
let make = () => {
  let clicks = React.useRef(0)
  let onClick = _ => {
      clicks.current = clicks.current + 1
      setTitle(document, Js.Int.toString(clicks.current))          
  }
  <div>
    <button className="flex flex-col" type_="button" onClick>
      <span name="click_count"> {clicks.current->React.int} </span>
      <span>{"click me"->React.string}</span>
    </button>
  </div>
}
```

### Adding Ref to DOM Element
```reasonml
@send external select: Dom.element => unit = "select"
@send external focus: Dom.element => unit = "focus"

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
    <input type_="text" ref={ReactDOM.Ref.domRef(inputRef)} className="w-full border-400" />
    <button type_="button" className="p-1 bg-200" onClick={focus}> 
        {"Focus"->React.string} 
    </button>
    <button type_="button" className="p-1 bg-200" onClick>
        {"Select Text"->React.string}
    </button>
  </div>
}
```

