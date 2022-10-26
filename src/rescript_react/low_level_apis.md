# Low level APIs to create components
The following APIs are used by JSX itself to create elements.
```reasonml 
React.createElement: (React.component<'props>, 'props) => React.elements

React.createElementVariadic: 
(React.component<'props>, 'props, array<React.element>) => React.element

React.cloneElement: (React.element, 'props) => React.element
```
### `React.createElement`
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
    {React.createElement(Movie.make, {"title": "Lopper", "desc": "One of the best sifi movies."})}
  </div>
}
```

### `React.createElementVariadic`
```reasonml
module Stack = {
    @react.component
    let make = (~width: option<string>=?, ~height: option<string>=?, ~children: option<React.element>=?) => {
        let ms = ReactDOM.Style.make
        let style = switch (width, height) {
            |(Some(w), Some(h)) => ms(~width=w, ~height=h, ())
            |(Some(w), None) => ms(~width=w, ~height="auto", ())
            |(None, Some(h)) => ms(~width="auto",~height=h, ())
            |(None, None) => ms(~width="auto", ~height="auto", ())
        }
       <div className="flex flex-col flex-wrap" style>
       { switch children { |Some(c) => c |None => React.null } }
       </div> 
    }
}

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
    {React.createElementVariadic(Stack.make, {"width": Some("100%"), "height": Some("50%") , "children": None}, [
        <div>{"My List"->React.string}</div>,
        <Stack width="50%" height="50%">
            <div>{"Scifi Movies"->React.string}</div> 
            <Movie title="Dark" desc="The best scifi series I've ever watched"/>
        </Stack> 
    ])}
  </div>
}
```

### `React.cloneElement`
Useful to add additional attributes to the original element - like data- attributes
```reasonml
let hello = <div className="text-slate-900"> {"Hello"->React.string} </div>
@react.component
let make = () => {
  <div>
    {React.cloneElement(hello, 
     {"className": "text-red-900 text-xl", "data-theme": "red"})}
  </div>
}
```
generated `<div class="text-red-900 text-xl" data-theme="red">Hello</div>`
