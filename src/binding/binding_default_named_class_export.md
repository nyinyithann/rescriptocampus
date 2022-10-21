# Binding to default or named exported JS Class

#### Binding to default exported JS class 
##### JavaScript 
```JavaScript
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
##### Rescript Binding
```reasonml
type rect = {
  area: float,
}
@new @module("./rectangle") external createRect: (float, float) => rect = "default"
@send external calcArea: rect => float = "calcArea"

/* usage */
let r = createRect(1.1, 2.2)
r.area->Js.log
r->calcArea->Js.log
```

#### Binding to named exported JS class
##### JavaScript 
```JavaScript
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

##### Rescript Binding
```reasonml
type rect
@new @module("./rectangle")  external createRect: (float, float) => rect = "Rectangle"
@get external area: rect => float = "area"
@send external calcArea: rect => float = "calcArea"

/* usage */
let r = createRect(1.1, 2.2)
r->area->Js.log
r->calcArea->Js.log
```

