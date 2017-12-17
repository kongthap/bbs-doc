## Chapter 04

### Documentation

- [`sequelize.js` Model Usage](http://docs.sequelizejs.com/manual/tutorial/models-usage.html)
- [`sequelize.js` Model Instance](http://docs.sequelizejs.com/manual/tutorial/instances.html)

### Setup

*Path*

```
|-package.json
+-src
|   |-index.js
|   +-models
|   |   |-Supplier.js
|   +-routes
|   |   |-supplier.js
```

*src/routes/supplier.js*

```js
const router = require('express').Router()
const sequelize = require('sequelize')

const Supplier = app.get('sequelize').models['supplier']

module.exports = router
```

*src/index.js*

```js
app.use(require('./routes/supplier.js'))
```

### `GET` & `Model.all()`

*src/routes/supplier.js*

```js
router.get('/suppliers', async (req, res) => {
    try {
        const suppliers = await Supplier.all()

        res.json(suppliers)
    } catch(err) {
        res.status(500).end()
    }
})
```

### `POST` & `Model.create()`

*src/routes/supplier.js*

```js
router.post('/suppliers', (req, res) => {
    try {
        const { first_name, last_name } = req.body
        const supplier = await Supplier.create({ first_name, last_name })

        res.json(supplier)
    } catch(err) {
        res.status(500).end()
    }
})
```

### `PUT`

*src/routes/supplier.js*

```js
router.put('/suppliers/:id', (req, res) => {
    try {
        const { id } = req.params
        const { first_name, last_name } = req.body

        const supplier = await Supplier.findById(id)

        supplier.first_name = first_name
        supplier.last_name = last_name

        await supplier.save()

        res.json(supplier)
    } catch(err) {
        res.status(500).end()
    }
})
```

### `DELETE`

*src/routes/supplier.js*

```js
router.delete('/suppliers/:id', (req, res) => {
    try {
        const { id } = req.params
        const supplier = await Supplier.findById(id)

        await supplier.destroy()

        res.status(200).end()
    } catch(err) {
        res.status(500).end()
    }
})
```
