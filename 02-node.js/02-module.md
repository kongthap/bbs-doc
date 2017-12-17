## Chapter 02

### Setup

*Path*

```
|-package.json
+-src
|   |-index.js
|   |-calculator.js
```

### Core Module

*src/index.js*

```js
const fs = require('fs')

fs.readdir('c:\\', 'utf8', (err, dirArray) => {
    console.log(dirArray)
})
```

### 3rd Party Module

*Terminal*

```
yarn add figlet
```

*src/index.js*

```js
const figlet = require('figlet')

console.log(figlet.textSync('Awesome!!!'))
```

### File Module

*src/calculator.js*

```js
module.exports = {
    add(number1, number2) {
        return number1 + number2
    },

    multiply(number1, number2) {
        return number1 * number2
    }
}
```

*src/index.js*

```js
const calculator = require('./calculator')

console.log(calculator.add(10, 20))
console.log(calculator.multiply(10, 20))
```
