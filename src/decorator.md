# Decorator & Extension Points

### Decorator
- To annotate a piece of code to express extra functionality

```reasonml
@inline let nodeEnv = "prod"
let env = nodeEnv

// JS output
let env = "prod"
```

#### @unboxed
To unwrap (aka unbox) the JS object wrappers from the output for records with a single field and variants with a single constructor and single payload. 
```reasonml
type coordinates = {x: float, y: float}
@unboxed type localCoordinates = Local(coordinates)
@unboxed type worldCoordinates = World(coordinates)

let renderDot = (World(coordinates)) => {
  Js.log3("Pretend to draw at:", coordinates.x, coordinates.y)
}

let toWorldCoordinates = (Local(coordinates)) => {
  World({
    x: coordinates.x +. 10.,
    y: coordinates.x +. 20.,
  })
}

let playerLocalCoordinates = Local({x: 20.5, y: 30.5})

renderDot(playerLocalCoordinates->toWorldCoordinates)
```
 
### Extension Point
- Extension points are attributes that don't annotate an item; they are the item. 
- Extension points start with %. A standalone extension point starts with %%.


```reasonml
let add = %raw("(a,b) => a + b")
add(2,2)

let pattern = %re("/^[A-Z]/g")

let f = (x, y) => {
  %debugger
  x + y
}

// standalone extension aka top level raw
%%raw(`import '../style/main.css'`)

%%raw(`
    var message = "hello";
    function greet(m) {
      console.log(m)
    }
`)
```
