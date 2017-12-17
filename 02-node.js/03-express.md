## Chapter 03

### Setup

*Path*

```
|-package.json
+-src
|   |-index.js
```

*Terminal*

```
yarn add express
```

*src/index.js*

```js
const express = require('express')
const app = express()

app.get('/', (req, res) => {
    res.send('<h1>Home Page</h1>')
})

app.listen(3000)
```

*Terminal*

```
yarn dev
```

*Postman*

```
http://localhost:3000
```

### `nodemon`

*package.json*

```json
{
    "scripts": {
        "dev": "nodemon ./src/index.js"
    }
}
```

### Route

*src/index.js*

```js
app.get('/customers', (req, res) => {
    res.send('<h1>Customer Page</h1>')
})
```

### File Response

*src/index.js*

```js
const path = require('path')

app.get('/file', (req, res) => {
    res.sendFile(path.resolve(__dirname, '..', 'public', 'bulma.min.css'))
})
```

### `json` Response

*src/index.js*

```js
app.get('/customers', (req, res) => {
    res.json({})
})
```

### HTTP Status Response

*src/index.js*

```js
app.get('/customers', (req, res) => {
    res.status(404).end()
})
```

*src/index.js*

### Response Header

*src/index.js*

```js
app.get('/customers', (req, res) => {
    res.header('Access-Control-Allow-Origin', '*').end()
})
```

### Redirect Response

*src/index.js*

```js
app.get('/customers', (req, res) => {
    res.redirect('/')
})
```

### `cookie` Response

*src/index.js*

```js
app.get('/customers', (req, res) => {
    res.cookie('username', 'steve', { expires: new Date(Date.now() + 3600), secure: true }).end()
})
```

### Request `path`

*src/index.js*

```js
app.get('/customers', (req, res) => {
    const { path } = req
    res.json({ path })
})
```

### Request Protocol

*src/index.js*

```js
app.get('/customers', (req, res) => {
    const { protocol } = req
    res.json({ protocol })
})
```

### Request Header

*src/index.js*

```js
app.get('/customers', (req, res) => {
    const contentType = req.header('Content-Type')
    const cacheControl = req.header('Cache-Control')
    res.json({ contentType, cacheControl })
})
```

### Request Parameter

*src/index.js*

```js
app.get('/customers/:id', (req, res) => {
    const { id } = req.params
    res.json({ id })
})

app.get('/:foo/:bar', (req, res) => {
    const { foo, bar } = req.params
    res.json({ foo, bar })
})
```

### Request Query String

*src/index.js*

```js
app.get('/customers', (req, res) => {
    const { gender, sort } = req.query
    res.json({ gender, sort })
})
```

*Postman*

```
http://localhost:3000/customers?gender=male&sort=true
```

### Middleware

*src/index.js*

```js
const logging = (req, res, next) => {
    console.log('logging')
    next()
}

const auth = (req, res, next) => {
    const token = req.header('Authorization')

    if (token) {
        next()
    } else {
        res.status(401).end()
    }
}

// apply middleware
app.use(logging)

// chain middleware
app.use(logging, auth)
```

### Specific Path Middleware

*src/index.js*

```js
app.use('/customers', auth)
```

### Fallback Middleware

*src/index.js*

```js
app.use((req, res) => {
    res.status(404).end()
})
```
