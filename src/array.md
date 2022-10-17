# Array
- same as JavaScript Array
- ramdom access
- dynamically resized, updated

### Rescript
```reasonml
/*
need to open Belt to use subscript operator
Array subscript operator ([]) is just a sugar over Belt.Array.get and Belt.Array.set
get: (array<'a>, int) => option<'a>
set: (array<'a>, int, 'a) => bool
*/
open Belt

let arr = ["a", "b"]
let a : option<string> = arr[0]
(arr[1] = "z") -> ignore
arr[1]->Js.log
```

#### shellshort
```reasonml
let shellShort = (arr, n) => {
    let interval = ref (n / 2)
    while interval.contents > 0 {
        for i in interval.contents to n - 1 {
            let temp = Array.getExn(arr, i)
            let j = ref(i)
            while j.contents >= interval.contents && Array.getExn(arr,j.contents - interval.contents) > temp {
                Array.setExn (arr, j.contents, Array.getExn (arr,j.contents - interval.contents))
                j := j.contents - interval.contents 
            }
            Array.setExn(arr, j.contents, temp)
        }
        interval := interval.contents / 2 
    }
}

let nums = [ 1, 2, 10, 11, 23, 45, 93, 20, 30, 93]
shellShort(nums, Array.length( nums))
Array.forEach(nums, Js.log)
```
```reasonml
/* Belt.Array.blit */
let arr1 = [1, 2, 3, 4, 5]
let arr2 = [10, 20, 30, 40, 50]
Belt.Array.blit(~src=arr1, ~srcOffset=1, ~dst=arr2, ~dstOffset=0, ~len = 3)
arr2->Js.log // [2, 3, 4, 40, 50]
```

### OCaml
```OCaml
let arr = [| 1; 2; 3|];;
print_int arr.(0) ;;
arr.(0) <- 10 ;;
arr |> Array.iter print_int ;;

let shell_sort arr n =
  let interval = ref (n / 2) in
  while !interval > 0 do
    for i = !interval to n - 1 do
     let temp = arr.(i) in
     let j = ref i in
     while !j >= !interval && arr.(!j - !interval) > temp do
       arr.(!j) <- arr.(!j - !interval);
       j := !j - !interval;
     done;
     arr.(!j) <- temp;
    done;
    interval := !interval / 2;
  done
;; 
let nums = [| 1; 2; 34; 11; 34; 29; 93; 293; 2020; 22; 43; 2; 0; 11|];;
shell_sort nums (Array.length nums);;
nums |> Array.iter (Printf.printf "%d ") ;;
```
