# Import from/Export to JS

Rescript supports 2 JS import/export formats.
- Common JS: `require("MyFile")` and `module.exports = ...`
- ES6 modules: `import * from MyFile` and `export let ...`

It can be configured via `bsconfig.json`
```json
{
  "package-specs": {
    "module": "commonjs",
    "in-source": true
  }
}
```
```"module": "es6``` resolves `node_modules` using relative paths.

### Import from JavaScript
#### Binding to default and named export
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

#### Binding to default exported JS class 
```reasonml
type rect = {
  area: float,
}
@new @module("./rectangle") external createRect : (float, float) => rect = "default"
@send  external calcArea : rect => float = "calcArea"
/* usage */
let r = createRect(1.1, 2.2)
r.area->Js.log
r->calcArea->Js.log

/* rectangle.js */
class Rectangle {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }

  get area() {
    return this.calcArea();
  }

  calcArea() {
    return this.width * this.height;
  }
}
export default Rectangle;
```
#### Binding to named exported JS class
```reasonml
type rect = {area: float}
@new @module("./rectangle")  external createRect: (float, float) => rect = "Rectangle"
@send external area : rect => float = "area"
@send external calcArea: rect => float = "calcArea"

/* usage */
let r = createRect(1.1, 2.2)
r.area->Js.log
r->calcArea->Js.log

/* rectangle.js */
class Rectangle {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }

  get area() {
    return this.calcArea();
  }

  calcArea() {
    return this.width * this.height;
  }
}
export { Rectangle };
```

### Export to JavaScript
- named exporting is already there
- for default export, just `let default = 123`. 

A JavaScript default export is really just syntax sugar for a named export implicitly called `default`.
