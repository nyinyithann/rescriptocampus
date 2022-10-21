# Bind using Rescript object

#### 
##### JavaScript 
```JavaScript
/* languages.js */
const rescript = {
  name: 'Rescript',
  type: 'FP',
  version: 10.2,
};
export { rescript };
```
##### Rescript Binding
```reasonml
type langobj = {
  "name": string,
  "type": string,
  "version": float,
}
@module("./languages") external rescript: langobj = "rescript"

/* usage */
rescript["name"]->Js.log
```
