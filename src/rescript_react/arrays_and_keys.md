# Arrays and Keys
Keys help React identify which elements have been changed, added, or removed throughout each render.
```reasonml
type movie = {title: string, desc: string}
let movies = [{title: "Dark", desc: "scifi"}, {title: "Looper", desc: "scifi"}]

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
    {
        movies
        ->Belt.Array.map(({title, desc}) => <Movie key={title} title desc />)
        ->React.array
    }
  </div>
}
```
