# Lazy

- defer and cache
- can't re-trigger the computation after the first `Lazy.force`
- it's not shared data type between Rescript and JavaScript

```reasonml
let rec fib = n => {
  switch n {
  | 0 | 1 => n
  | _ => fib(n - 1) + fib(n - 2)
  }
}

/* using Lazy.force */
let lfib = lazy(fib(20))
lfib->Lazy.force->Js.log

/* pattern match with switch */
switch lfib {
    | lazy(result) => Js.log(result)
}

/* pattern match with let binding */
let lazy(n) = lfib
n->Js.log

/* with exception handling */
let n = try {
        Lazy.force(lazy(fib(22)))
    } catch {
     |Some_error => 0
    }
```
