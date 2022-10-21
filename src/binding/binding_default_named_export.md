# Binding to default or named export

#### JavaScript
```javascript
/* utils.js */

function fib(n) {
  if (n === 0 || n === 1) {
    return n;
  }
  if (n < 0) {
    return 0;
  }
  return fib(n - 1) + fib(n - 2);
}

function max(x, y) {
  return x > y ? x : y;
}

function min(x, y) {
  return x < y ? x : y;
}

const lang = {
  name: 'Rescript',
  type: 'FP',
  version: 10.2,
};

export default lang;
export { lang, fib, max, min };
```

#### Rescript Binding
```reasonml
type lang = {
  name: string,
  @as("type") type_: string,
  version: float,
}

@module("./utils") external lang: lang = "default"
@module("./utils") external fib: int => int = "fib"
@module("./utils") external min: (int, int) => int = "min"
@module("./utils") external max: (int, int) => int = "min"

/* usage */
lang.name->Js.log
fib(10)->Js.log
min(1,2)->Js.log
max(2,3)->Js.log
```
