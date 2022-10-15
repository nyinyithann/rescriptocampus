# Conversion

##### Rescript

```js
open Js

// string to bool
bool_of_string("true")->log // true
bool_of_string("false")->log // false
bool_of_string_opt("maybe")->log // undefined
// error
// bool_of_string("maybe")->log

string_of_bool(true)->log // true
string_of_bool(false)->log // false
// string to int
int_of_string("100")->log // 100
int_of_string_opt("abc100")->log // undefined

int_of_string("100_000")->log // 100000
int_of_string("010")->log // 10

// hex literal
int_of_string("0xFF_FFF")->log // 1048575
int_of_string("0xFFFF_FFFF")->log // -1 - overflow

// binary literal
int_of_string("0b100")->log // 4
int_of_string("0b100_000")->log // 32

// octal literal
int_of_string("0o100")->log // 64
int_of_string("0o100_000")->log // 32768

// error
// int_of_string(" 111")->log // error
// int_of_string("111 ")->log // error

// int to string
1_000->Int.toString->log // 1000
0xff_fff->Int.toString->log // 104875
0b1_100->Int.toString->log // 12
0o1_100->Int.toString->log // 576

// string to float
float_of_string("1.1")->log // 1.1
float_of_string("  10. ")->log // 10
float_of_string("1.1e+4")->log // 11000
float_of_string_opt("a10.")->log // undefined
float_of_string(" 1.11 ")->log // 1.11

// float to string
1.1->Float.toString->log // 1.1

// int to float
(float_of_int(10) +. 10.)->log // 20
10->Int.toFloat->log // 10

// float to int
int_of_float(1.111)->log //

// char to string
Char.escaped('a')->log

// char to int
Char.code('a')->log
// int to char
(Char.chr(65) == 'A')->log
```
