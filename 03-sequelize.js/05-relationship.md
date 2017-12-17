## Chapter 05

### Documentation

- [`sequelize.js` Relationship](http://docs.sequelizejs.com/manual/tutorial/associations.html)

*Relationship Type*

- `hasOne()`
- `hasMany()`
- `belongsTo()`
- `belongsToMany()`

### Setup

*Path*

```
|-package.json
+-src
|   |-index.js
|   +-models
|   |   |-Customer.js
|   |   |-Order.js
|   +-routes
|   |   |-customer.js
|   |   |-order.js
```

*src/index.js*

```js
// models
const Customer = require('./models/Customer')()
const Order = require('./models/Order')()

// relationship
Customer.hasMany(Order, { foreignKey: 'customer_id' })
Order.belongsTo(Customer, { foreignKey: 'customer_id' })
```

### `getOrders()`

*src/routes/customer.js*

```js
router.get('/customers/:id', async (req, res) => {
    try {
        const { id } = req.params

        const customer = await Customer.findById(id)
        const orders = await customer.getOrders()

        res.json({ customer, orders })
    } catch (err) {
        res.status(500).end()
    }
})
```

### `getCustomer()`

*src/routes/order.js*

```js
router.get('/orders/:id', async (req, res) => {
    try {
        const { id } = req.params

        const order = await Order.findById(id)
        const customer = await order.getCustomer()

        res.json({ order, customer })
    } catch (err) {
        res.status(500).end()
    }
})
```

### Eager Loading

*src/routes/order.js*

```js
router.get('/order/:id', async (req, res) => {
    try {
        const { id } = req.params

        const order = await Order.findById(id, {
            include: [{
                model: Customer,
            }]
        })
    } catch(err) {
        res.status(500).end()
    }
})
```

### Pagination

```js
const options = { limit: 5, offset: 5 }
Customer.all(options)
```

### `attributes`

```js
const options = { attributes: [ 'first_name', 'last_name' ] }
Customer.all(options)
```
