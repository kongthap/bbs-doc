## Chapter 03

### Documentation

- [`sequelize.js` Model Definition](http://docs.sequelizejs.com/en/latest/docs/models-definition/)
- [`sequelize.js` Data Type](http://docs.sequelizejs.com/manual/tutorial/models-definition.html#data-types)

```js
// setter
sequelize.define('supplier', fields, options)

// getter
sequelize.models['supplier']
```

### Setup

*Path*

```
|-package.json
+-src
|   |-index.js
|   +-models
|   |   |-Supplier.js
```

### Global `app`

*src/index.js*

```js
// const app = express()
app = express()

app.set('sequelize', sequelize)
```

*src/models/Supplier.js*

```js
const Sequelize = require('sequelize')

module.exports = () => {
    const sequelize = app.get('sequelize')

    const fields = {
        id: {
            autoIncrement: true,
            primaryKey: true,
            type: Sequelize.INTEGER
        },
        first_name: Sequelize.STRING,
        last_name: Sequelize.STRING
    }

    const options = {
        underscored: true
    }

    return sequelize.define('supplier', fields, options)
}
```

*src/index.js*

```js
require('./models/Supplier')()

// create
sequelize.sync()

// drop + create
sequelize.sync({ force: true })
```
