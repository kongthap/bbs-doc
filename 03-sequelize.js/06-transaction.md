## Chapter 06

### Documentation

- [`sequelize.js` Transaction](http://docs.sequelizejs.com/manual/tutorial/transactions.html)

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

### `sequelize.js` Transaction

*src/routes/supplier.js*

```js
sequelize.transaction((transaction) => {
    // operation 1
    return Supplier.create({}, { transaction })
        .then((supplier) => {
            // operation 2
            return Supplier({}, { transaction })
        })
})
.then((result) => {
    // automatic commit
})
.catch((err) => {
    // automatic rollback
})
```

### `async` & `await`

*src/routes/supplier.js*

```js
router.post('/suppliers', async (req, res) => {
    try {
        const t = await sequelize.transaction()

        try {
            // pass
            const s1 = await Supplier.create({ first_name: 'Steve', last_name: 'Jobs' }, { transaction: t })
            // fail
            const s2 = await Supplier.create({ first_name: 'John' }, { transaction: t })

            t.commit()
        } catch (err) {
            t.rollback()

            throw err
            // or
            throw new Error(err)
        }
        res.status(200).end()
    } catch (err) {
        res.status(500).end()
    }
})
```
