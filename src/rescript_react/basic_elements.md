# Basic Elements

### Creating elements from `string, int, float, array` & Null element `React.null`
```reasonml
let {string, int, float, array} = module(React)
let strElement = <p key="hello"> {"Hello"->string} </p>
let intElement = <p key="t5"> {25->int} </p>
let floatElement = <p key="pi"> {3.14->float} </p>
let elements = [strElement, intElement, floatElement]

let isTired = false

let basicElement = <div> {"I'm a basic element. 😁"->string} </div>

@react.component
let make = () => {
  <div>
    <div> {elements->array} </div>
    {switch isTired {
    | true => <p> {"Omg!"->string} </p>
    | false => React.null
    }}
    basicElement
  </div>
}
```
