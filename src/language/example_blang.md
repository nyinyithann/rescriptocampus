# Example(blang)
Example from [RealWorldOCaml](https://dev.realworldocaml.org/variants.html)
```reasonml
type rec expr<'a> =
  | Base('a)
  | Const(bool)
  | And(list<expr<'a>>)
  | Or(list<expr<'a>>)
  | Not(expr<'a>)

let and_ = l => {
    if Belt.List.some(l, (x) => switch x { 
        | Const(false) => true 
        | _ => false }) { 
        Const(false) 
    }
    else {
        switch Belt.List.keep(l, x => switch x { 
            | Const(true) => false 
            | _ => true}) {
                | list{} => Const(true)
                | list{x} => x
                | l => And(l)
        }
    }
}

let or_ = l => {
   open Belt
   if List.some(l, x => switch x { | Const(true) => true | _ => false}) { Const(true) }
   else {
       switch List.keep(l, x => switch x { | Const(false) => false | _ => true }) {
           | list{} => Const(false)
           | list{x} => x
           | l => Or(l)
       }
   }
}

let not_ = (expr) => {
    switch expr {
        | Const(x) => Const(!x)
        | e => Not(e)
    }
}

let rec simplify = (expr) => {
    open Belt
    switch expr {
        | (Base(_) | Const(_)) as x => x
        | And(l) => and_ (List.map(l, x => simplify(x)))
        | Or(l) => or_ (List.map(l, x => simplify(x)))
        | Not(e) => not_ (simplify(e))
    }
}

let rec eval = (expr, base_eval) => {
  let eval' = expr => eval(expr, base_eval)
  switch expr {
  | Base(base) => base_eval(base)
  | Const(b) => b
  | And(exprs) => Belt.List.every(exprs, eval')
  | Or(exprs) => Belt.List.some(exprs, eval')
  | Not(expr) => !eval'(expr)
  }
}

type mail_field = To | From | CC | Date | Subject
type mail_predicate = {field: mail_field, contains: string}
let test = (field, contains) => Base({field, contains})

let base_eval = ({field, contains}) => {
  switch field {
  | To => contains == "Ryan"
  | Subject => contains == "Maths"
  | _ => true
  }
}

let expr = And(list{
        Or(list{test(To, "Ryan"), test(Subject, "Maths"), Const(false)}), 
        Const(true), 
        Not(Const(true))
    })

let result = eval(simplify(expr), base_eval)
Js.log(result) // false
```

