# Bind with getter/setter

##### Rescript Binding
```reasonml
@set external setValue: (Dom.element, string) => unit = "value"
@get external getValue: Dom.element => string = "value"

/* @get_index/@set_index to access dynamic property or an index */
type t
@new external create: array<float> => t = "Int32Array"
@get_index external get: (t, int) => float = ""
@set_index external set: (t, int, float) => unit = ""

/* usage */
let arr = create([1.,2.,3.])
arr->get(0)->Js.log
arr->set(0, 77.7)
```
