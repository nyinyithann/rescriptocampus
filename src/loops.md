# loops

#### Rescript
```reasonml
for i in 1 to 10 {
  i->Js.log
}

for i in 10 downto 1 {
  i->Js.log
}

let i = ref(1)
while i.contents <= 10 {
  i->Js.log
  incr(i)
}

/* breaking loop */
exception Break_the_loop
let break_loop = () => {
  try {
    for i in 1 to 100 {
      if i > 10 {
        raise(Break_the_loop)
      }
      i->Js.log
    }
  } catch {
  | Break_the_loop => ()
  }
}
break_loop()

let break = ref(false)
let i = ref(10)
while !break.contents {
  if i.contents <= 20 {
    i->Js.log
    incr(i)
  } else {
    break := true
  }
}

```

#### OCaml
```ocaml
for i = 1 to 10 do print_int i done ;;

for i = 10 downto 1 do print_int i done ;;

let i = ref 1 in
while !i <= 10 do 
  print_int !i;
  incr i
done ;;

exception Break_the_loop
let break_loop = 
try 
 for i = 1 to 100 do
   if i <= 10 then print_int i
   else raise Break_the_loop
 done;
 with Break_the_loop -> () ;;
 ```
