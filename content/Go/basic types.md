---
title: basic types
tags:
  - Go
---
``` go
bool

string

// `int`, `uint`, and `uintptr` types are usually 32 bits wide on 32-bit systems and 64 bits wide on 64-bit systems 
int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr

byte // alias for uint8

rune // alias for int32
     // represents a Unicode code point

float32 float64

complex64 complex128
```


- Type conversions
``` go
var i int = 42
var f float64 = float64(i)
var u uint = uint(f)

// 
i := 42
f := float64(i)
u := uint(f)
```
- Trong Go, conversion cần explicit

#### Integers

| uint8  | the set of all unsigned 8-bit integers (0 to 255)                                   |
| ------ | ----------------------------------------------------------------------------------- |
| uint16 | the set of all unsigned 16-bit integers (0 to 65535)                                |
| uint32 | the set of all unsigned 32-bit integers (0 to 4294967295)                           |
| uint64 | the set of all unsigned 64-bit integers (0 to 18446744073709551615)                 |
| int8   | the set of all signed 8-bit integers (-128 to 127)                                  |
| int16  | the set of all signed 16-bit integers (-32768 to 32768)                             |
| int32  | the set of all signed 32-bit integers (-2147483648 to 2147483647)                   |
| int64  | the set of all signed 64-bit integers (-9223372036854775808 to 9223372036854775807) |
| byte   | alias for uint8                                                                     |
| rune   | alias for int32                                                                     |
