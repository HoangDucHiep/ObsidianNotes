---
title: switch
tags:
  - Go
---
``` go
switch <initial statement>; <expression> { // initial is like if
case <expression>:
	<statements>
case <expression>, <expression>:  // match multiple cases
	<statements>
default: 
	<statements>
}
```