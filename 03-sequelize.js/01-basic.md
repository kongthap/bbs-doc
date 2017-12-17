## Chapter 01

### Documentation

- [`sequelize.js` Setup - Official](http://docs.sequelizejs.com/manual/installation/getting-started.html)

### Setup

*Path*

```
|-package.json
+-src
|   |-index.js
```

*Terminal*

```
yarn add express sequelize

# mysql
yarn add mysql2
# mssql
yarn add tedious
```

*src/index.js*

```js
const Sequelize = require('sequelize')

const connecitonUri = 'mysql://root@192.168.99.100:3306/northwind'
const options = {
    operatorsAliases: false
}

const sequelize = new Sequelize(connecitonUri, options)
```

### Authentication

*src/index.js*

```js
sequelize.authenticate()
    .then(() => {
        console.log('Connected')
    })
    .catch(err => {
        console.log(err)
    })
```
