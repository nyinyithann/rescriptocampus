# Manage a list of Refs using a ref callback
- `React.Ref.callbackDomRef()`
```reasonml
@send external scrollIntoView: (Dom.element, {..}) => unit = "scrollIntoView"

let getCatList = () => {
  let cats = []
  for i in 0 to 10 {
    cats->Belt.Array.push({
      "id": i,
      "url": "https://placekitten.com/250/200?image=" ++ Js.Int.toString(i),
    })
  }
  cats
}

module CatList = {
  let cats = getCatList()
  @react.component
  let make = () => {
    let itemsRef = React.useRef(Belt.MutableMap.Int.make())
    let scrollToId = id => {
      let m = itemsRef.current
      switch Belt.MutableMap.Int.get(m, id) {
      | Some(e) =>
        scrollIntoView(
          e,
          {
            "behavior": "smooth",
            "block": "nearest",
            "inline": "center",
          },
        )
      | None => ()
      }
    }
    <>
      <div className="flex flex-col p-4 items-start justify-center">
        <nav className="flex gap-2 pb-2">
          <button type_="button" className="p-2 bg-slate-200" onClick={_ => scrollToId(1)}>
            {"Tome"->React.string}
          </button>
          <button type_="button" className="p-2 bg-slate-200" onClick={_ => scrollToId(5)}>
            {"Remy"->React.string}
          </button>
          <button type_="button" className="p-2 bg-slate-200" onClick={_ => scrollToId(9)}>
            {"Jack"->React.string}
          </button>
        </nav>
      </div>
      <div className="flex p-4 overflow-x-auto">
        <ul className="flex gap-2">
          {cats
          ->Belt.Array.map(cat => {
            <li
              className="flex-none"
              ref={ReactDOM.Ref.callbackDomRef(element => {
                let m = itemsRef.current
                switch element->Js.Nullable.toOption {
                | Some(e) => Belt.MutableMap.Int.set(m, cat["id"], e)
                | None => Belt.MutableMap.Int.remove(m, cat["id"])
                }
              })}>
              <img src={cat["url"]} className="w-[20rem] h-[16rem]" />
            </li>
          })
          ->React.array}
        </ul>
      </div>
    </>
  }
}

@react.component
let make = () => {
  <CatList />
}
```


