# Variadic Function
#### JavaScript
```JavaScript
/* play.js */
function sum(...args) {
  return Array.from(args).reduce((x, y) => x + y);
}
export { sum };
```

#### Rescript Binding
```reasonml
@module("./play") @variadic external sumInts : array<int> => int = "sum"
@module("./play") @variadic external joinStrings : array<string> => string = "sum"

/* usage */
sumInts([1,2,3,4,5])->Js.log
joinStrings(["abc", "def", "xyz"])->Js.log
```

