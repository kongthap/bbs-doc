## Chapter 01

### Setup

*Path*

```
|-package.json
+-src
|   |-index.js
```

*src/index.js*

```js
console.log('Hello World')
```

*Terminal*

```
node ./src/index.js
```

### `npm` Script

*package.json*

```json
{
    "scripts": {
        "dev": "node ./src/index.js"
    }
}
```

*Terminal*

```
yarn dev

# or
npm run dev
```

### Runtime Argument

*package.json*

```json
{
    "scripts": {
        "dev": "node ./src/index.js foo bar"
    }
}
```

*src/index.js*

```js
console.log(process.argv[2])
console.log(process.argv[3])
console.log(process.argv)
```

### Environment

*Terminal*

```
yarn add cross-env --dev
```

*package.json*

```json
{
    "scripts": {
        "dev": "cross-env foo=10 bar=20 NODE_ENV=production node ./src/index.js"
    }
}
```

*src/index.js*

```js
console.log(process.env.foo)
console.log(process.env.bar)
console.log(process.env.NODE_ENV)
console.log(process.env)
```

### Reset `npm` Script

*package.json*

```json
{
    "scripts": {
        "dev": "node ./src/index.js"
    }
}
```
