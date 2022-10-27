# Styling

### Inline style
```reasonml

let style1 = ReactDOM.Style.make(
    ~backgroundColor="blue",
    ~fontSize="2rem",
    ~color=?Some("yellow"),
    ~padding="0.5rem 1rem",
    (),
)

let roundedStyle = ReactDOM.Style.make(~borderRadius="50px 50px", ())

let combined = ReactDOM.Style.combine(style1, roundedStyle)

let unsafeStyle =
ReactDOM.Style.make(~color="red", ~padding="10px", ())
 ->ReactDOM.Style.unsafeAddProp(
  "-webkit-animation-name",
  "moveit")
```

### Global CSS
```reasonml
// in a CommonJS setup
%%raw("require('./styles/main.css')")

// or with ES6
%%raw("import './styles/main.css'")
```

### CSS Modules
```reasonml
// {..} means we are handling a JS object with an unknown
// set of attributes
@module external styles: {..} = "./styles.module.css"

// Use the obj["key"] syntax to access any classname within our object
let app = <div className={styles["root"]} />
```
