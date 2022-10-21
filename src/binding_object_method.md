# Object Method

#### JavaScript
```JavaScript
/* play.js */
let funcObj = {
  id: (x) => x,
};

export { funcObj };
```

#### Rescript Binding
```reasonml
type fobj 
@module("./play") external funcObj : fobj = "funcObj"
@send external id : (fobj, int) => int = "id" 

/* usage */
funcObj-> id (25)->Js.log
```

