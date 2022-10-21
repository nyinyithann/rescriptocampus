# Global JS Values

#### [@val](https://rescript-lang.org/docs/manual/latest/bind-to-global-js-values#global-modules), [@scope](https://rescript-lang.org/docs/manual/latest/bind-to-global-js-values#global-modules)
- [Docs](https://rescript-lang.org/docs/manual/latest/bind-to-global-js-values#global-modules)
- [Playground Link](https://rescript-lang.org/try?code=C4TwDgpgBAlgtnCATGBDYECSSBQABAN1QBsoIAPDAJwDsSoBnCYTBZNDALigAoAzYgHt0UALwA+KAFcaMYABooA4cACUYyfEQp0WJGKgAiJizY6Mh-EVIVqdUgGNiEVFVbaOEblva7sG6VlgA0MnFzczT0tnYJgDE3dfDB5yAIApBgA6IQBzFNVFAEYABkLMksLVHGrCejwGB0FIHkMAWXQAC0Mq2whaejA47mURUSMABUxLQYBacQzswRyrel7+0jAQKGGhUaN24A7MyemQOYXcmusoesbmwyRBBylEGmBunDX7KGA5Z23GMAqDAaDkQr9gM5LBDnOcspcVqRbk0IDwWgB3EGPdGGRSGIQOEgAZWAgioqByEG6PUofW+YVc3BkcgCzOCY1CzlclgZVB4VURZFp6ygBOJpPJlIAwlyqEygqyFRyxcQSWSKRBMrzok9xerpbL+dVBV96DAGNweAByVCKK0AI3UEig9sEglIHIA8vaAFYQBzATLmyzmniFeQAJlUcMWy0FyPu3r9AY+ptI5stNrtjoCrvdIWDOFDCwAYrtAwB9AByqCrilL5cy1dr0fm8KW1QYmOADg6UAApGmeBWKwARACiADUR+oAN44AA+UCJgkQw6dkguSxaSAgBCgcEEu4+S6rgho0GdW7yhjAVCPUgDMHPB6PVKqAF9O93ewOhyO+BgZw6EQOdF2XVdUT4DcoGvfgqlPc9L03dsbxoc8ZnQ3cyBoAgYHvGhXneT8AG4gA)

```reasonml
type immediateId
@val external setImmediate: (float => unit, float) => immediateId = "setImmediate"
@val external clearImmediate: immediateId => unit = "clearImmediate"
// usage
let id = setImmediate(x => Js.log(x), 101.101)
clearImmediate(id)

@val @scope("Math")
external pi : float = "PI"
pi->Js.log
// or
@val external py : float = "Math.PI"
py->Js.log

@val @scope(("window", "localStorage"))
external clear: unit => unit = "clear"
clear()
// js => window.localStorage.clear()
// Or 
@val external localStorageClear: unit => unit = "localStorage.clear"
localStorageClear()
// js => localStorage.clear()

@val external is: ('a, 'b) => bool = "Object.is"
is(1,2)->Js.log
// Or
@val @scope("Object")
external is: ('a, 'b) => bool = "is"
is(Js.Float._NaN, Js.Float._NaN)->Js.log
```

#### Special global values [%external](https://rescript-lang.org/docs/manual/latest/bind-to-global-js-values#special-global-values)
```reasonml
switch %external(__DEV__) {
| Some(_) => Js.log("dev mode")
| None => Js.log("production mode")
}

switch %external(__filename) {
| Some(f) => Js.log(f)
| None => Js.log("non-node environment")
};
```
