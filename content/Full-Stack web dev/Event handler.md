---
title: Event handler
tags:
  - Full-Stack
  - React
---
### Some lưu ý :>
- Event handlers phải luôn là một ***function*** hoặc một ***reference to a function***
``` js
<button onClick="crap...">button</button>
```
``` shell
index.js:2178 Warning: Expected `onClick` listener to be a function, instead got a value of `string` type.
    in button (at index.js:20)
    in div (at index.js:18)
    in App (at index.js:27)
```

### Functions that return a Function
``` jsx
const App = () => {
  const [value, setValue] = useState(10)

  const hello = () => {
    const handler = () => console.log('hello world')
    return handler
  }

  return (
    <div>
      {value}
      <button onClick={hello()}>button</button>
      <button onClick={hello('world')}>button</button>
      <button onClick={hello('react')}>button</button>
      <button onClick={hello('function')}>button</button>
    </div>
  )
}
```
