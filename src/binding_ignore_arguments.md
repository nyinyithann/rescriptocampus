# Ignore Arguments

#### From [Docs](https://rescript-lang.org/docs/manual/latest/bind-to-js-function#ignore-arguments)
You can also explicitly "hide" external function parameters in the JS output, which may be useful if you want to add type constraints to other parameters without impacting the JS side:

#### Rescript
```reasonml
@val external doSomething: (@ignore 'a, 'a) => unit = "doSomething"

doSomething("this only shows up in ReScript code", "test")
```

#### JavaScript Output
```JavaScript
doSomething("test");
```
