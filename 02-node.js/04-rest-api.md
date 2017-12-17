## Chapter 04

### Setup

*Path*

```
|-package.json
|-db.json
+-src
|   |-index.js
|   |-customer.js
```

### Router Middleware

*src/customer.js*

```js
const express = require('express')
const router = express.Router()

router.get('/customers', (req, res) => {
    res.json([])
})

module.exports = router
```

*src/index.js*

```js
app.use(require('./customer'))
```

### ReSTfull

*URI*

```
GET http://localhost:3000/customers
POST http://localhost:3000/customers

GET http://localhost:3000/customers/:id
PUT http://localhost:3000/customers/:id
DELETE http://localhost:3000/customers/:id
```

### `GET` Customers

*src/customer.js*

```js
const { customers } = require('../db')

router.get('/customers', (req, res) => {
    res.json({ customers })
})
```

### `GET` Customer By ID

*src/customer.js*

```js
router.get('/customers/:id', (req, res) => {
    const { id } = req.params
    const customer = customers.find((c) => {
        return c.id == id
    })

    res.json({ customer })
})
```

### `POST` and `body`

*src/index.js*

```js
// urlencoded
app.use(express.urlencoded({ extended: true }))
// json
app.use(express.json())
```

*src/customer.js*

```js
router.post('/customers', (req, res) => {
    const { firstName, lastName } = req.body
    res.json({ firstName, lastName })
})
```

### `PUT`

*src/customer.js*

```js
router.put('/customers/:id', (req, res) => {
    const { id } = req.params
    const { firstName, lastName } = req.body

    res.json({ id, firstName, lastName })
})
```

### `DELETE`

*src/customer.js*

```js
router.delete('/customers/:id', (req, res) => {
    const { id } = req.params

    res.json({ id })
})
```

### `GET` Customers & Query String

*src/customer.js*

```js
router.get('/customers', (req, res) => {
    const { gender, age } = req.query

    if (gender || age) {
        const filteredCustomers = customers.filter((c) => {
            if (gender && age)
                return (c.gender == gender) && (c.age == age)

            if (gender)
                return (c.gender == gender)

            if (age)
                return (c.age == age)
        })

        res.json(filteredCustomers)
    }

    res.json(customers)
})
```
