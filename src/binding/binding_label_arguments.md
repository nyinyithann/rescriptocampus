# Labeled Arguments

#### JavaScript
```JavaScript
/* play.js */
function drawCircle(x, y, color) {
  const s1 = `drawing circle at (${x},${y})`;
  return color ? `${s1} with ${color} color.` : s1;
}
export { drawCircle };
```

#### Rescript Binding
```reasonml
@module("./play") external drawCircle: 
(~x: float, ~y: float, ~color: string=?, unit) => string = "drawCircle"

/* usage */
drawCircle(~x=11.11, ~y=12.12, ())->Js.log
drawCircle(~x=11.11, ~y=12.12, ~color=?Some("Red"), ())->Js.log
drawCircle(~x=11.11, ~y=12.12, ~color="Blue", ())->Js.log
```
