## Chapter 00

[codepen.io](https://codepen.io/pen/?editors=0012)

### Variable Declaration

```js
var x = 10
var y = [1, 2, 3]
var z = { foo: 'bar' }
```

### Array

```js
var numbers = [ 1, 2, 3, 4, 5 ]
var things = [ 1, 'A', ['foo', 'bar'] ]

console.log(numbers)
console.log(things)
```

### Plain JavaScript Object

```js
var person = {
    name: 'Steve',
    surname: 'Jobs',
    address: {
        city: 'California',
        country: 'USA'
    },
    greet() {
        alert('Hello World')
    }
}

console.log(person.adress)
person.greet()
```

### Object Assignment

```js
/**
 * value assignment
 */
var x = 10
var y = x

y = 20
console.log(x == y) // false

/**
 * reference assignment
 */
var x = { a: 1 }
var ref = x // reference assignment

ref['a'] = 2
console.log(x == ref) // true
console.log(x)
console.log(ref)
```

### Cloning Object

```js
var x = { a: 1 }
var copy = Object.assign({}, x)

console.log(x == copy) // false

// spread syntax
var copy = { ...x }
```

### `global` & `local` Scope

```js
/**
 * global scope
 */
var x = 10 // global scope declaration

function foo() {
    x = 20 // re-assignment
}

foo()
console.log(x) // 20

/**
 * local scope
 */
var x = 10 // global scope declaration

function foo() {
    var x = 20 // local scope declaration
}

foo()
console.log(x) // 10
```

### `block` Scope

```js
/**
 * var
 */
var x = 10

if (true) {
    var x = 20
}
console.log(x) // 20

/**
 * let & const
 */

let x = 10

if (true) {
    let x = 20
}
console.log(x) // 10
```

> `let` and `const` offer `block` scope declaration

### Immutable

```js
const x = []
x = [1, 2, 3, 4, 5] // runtime error, re-assigned

for (const y = 0; y < 5; y++) { console.log(y) } // runtime error, re-assigned

const z = []
z.push(1)
console.log(z) // [ 1 ]
```

### Ternary Statement

```js
const age = 40
const status = (age > 40) ? 'old' : 'young'
console.log(status) // young
```

### Template String

```js
const text = `line1\nline2`
console.log(text)

const age = 40
const text = `I'm ${ age } years old`
// ternary statement
const text = `I'm a ${ (age > 40) ? 'old' : 'young' } man`
```

### Destructuring

```js
const name = 'Steve'
const age = 40
const person = { name, age } // destructring
console.log(person) // { name: 'Steve', age: 40 }

const address = { city: 'Sriracha', province: 'Chonburi', postcode: 20230 }
const { city, postcode } = address // destructing
console.log(city, postcode) // 'Srirach' 20230
```

### Function Declaration & Function Expression

```js
// function declaration
function foo() {
    ...
}

// es5 function declaration
const foo = function() {
    ...
}

// es6 function declaration (arrow function)
const foo = () => {
    ...
}
```

### Non-Blocking I/O

```js
console.log(1)

setTimeout(() => {
    console.log(2)
}, 2000)

console.log(3)
```

### Async Function

```js
const random = () => {
    setTimeout(() => {
        return Math.random()
    }, 2000)
}

console.log(random())
```

### Callback

```js
const random = (cb) => {
    setTimeout(() => {
        cb(Math.random())
    }, 2000)
}

random((result) => {
    console.log(result)
})
```

### Callback Hell

```js
const random = (param, cb) => {
    setTimeout(() => {
        cb({ param, number: Math.random() })
    }, 2000)
}

random(1, (result) => {
    console.log(result)

    random(2, (result) => {
        console.log(result)

        random(3, (result) => {
            console.log(result)
        })
    })
})
```

### Promise

```js
const random = () => {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            const number = Math.random()
            console.log(number)

            if (number > 0.3)
                resolve(number)
            else
                reject('error')
        }, 1000)
    })
}

random()
    .then((result) => {
        console.log(result)
    })
    .catch((err) => {
        console.log(err)
    })
```

### Chaining Promise

```js
// one after another
random()
    .then((result) => {
        console.log(result)

        return random()
    })
    .then((result) => {
        console.log(result)

        return random()
    })
    .then((result) => {
        console.log(result)
    })
    .catch((err) => {
        console.log(err)
    })
```

### `Promise.all()`

```js
// pararell
Promise.all([random(), random(), random()])
    .then((results) => {
        // all resolves
        console.log(results)
    })
    .catch((err) => {
        // any single reject
        console.log(err)
    })
```

### `async` & `await`

```js
const asyncRandom = async () => {
    try {
        const result1 = await random()
        const result2 = await random()
        const result3 = await random()

        return `${ result1 } ${ result2 } ${ result3 }`
    } catch(err) {
        // any single reject
        return err
    }
}

asyncRandom()
    .then((result) => {
        console.log(result)
    })
```
