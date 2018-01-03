## Chapter 08

### Express.js & Vue.js Setup

![](https://i.cubeupload.com/7bT1tP.png)

*Path*

```
|-package.json
|-webpack.config.js
|-.babelrc
+-public
|   |-index.html
+-express
|   |-index.js
|   +-routes
|   |   |-auth.js
|   +-middlewares
|   |   |-authorize.js
+-vue
|   |-main.js
|   |-App.vue
```

### Express.js Setup

*Terminal*

```
yarn add express
```

*express/index.js*

```js
const express = require('express')
const app = express()

app.use(express.static('public'))

/**
 * routes
 **/

app.listen(3000)
```

*package.json*

```json
{
    "scripts": {
        "express": "nodemon ./express/index.js"
    }
}
```

*Terminal*

```
yarn express
```

### `webpack` Setup

*Terminal*

```
yarn add webpack --dev
```

*webpack.config.js*

```js
const path = require('path')

modules.export = {
    entry: path.resolve('vue', 'main.js'),
    output: {
        path: path.resolve('public'),
        filename: 'build.js'
    }
}
```

*vue/main.js*

```js
console.log('Hello World')
```

*package.json*

```json
{
    "scripts": {
        "vue": "webpack --watch"
    }
}
```

*Terminal*

```
yarn vue
```

### Vue.js Setup

*Terminal*

```
yarn add vue-loader vue-template-compiler --dev
yarn add style-loader css-loader --dev

yarn add vue
```

*webpack.config.js*

```js
module.exports = {
    module: {
        loaders: [
            {
                test: /\.vue$/,
                loader: 'vue-loader',
                exclude: /(node_modules)/
            },
            {
                test: /\.css$/,
                loader: 'style-loader!css-loader',
            }
        ]
    }
}
```

*vue/App.vue*

```html
<template>
    <div>App</div>
</template>

<script>
export default {

}
</script>
```

*vue/main.js*

```js
import Vue from 'vue'
import App from './App.vue'

new Vue({
    el: '#vueApp',
    render(renderElement => {
        return renderElement(App)
    })
})
```

### `babel` Setup

*Terminal*

```
yarn add babel-core babel-loader --dev
yarn add babel-preset-env babel-preset-stage-0 --dev
```

*.babelrc*

```json
{
    "presets": [
        [ "env", {
            "module": false
        } ],
        "stage-3"
    ]
}
```

*webpack.config.js*

```js
module.exports = {
    module: {
        loaders: [
            {
                test: /\.vue$/,
                loader: 'vue-loader!babel-loader',
                exclude: /(node_modules)/
            }
        ]
    }
}
```

### Token Based Authentication

*Terminal*

```
yarn add jsonwebtoken
```

*express/routes/auth.js*

```js
const jwt = require('jsonwebtoken')
const SECRET = 'SUPERSECRET'
const options = { expiresIn: '2 days' }

router.post('/login', (req, res) => {
    const { username } = req.body

    // username & password againt database
    const payload = { username, role: 'admin' }
    const token = jwt.sign(payload, SECRET, options)

    res.json({ token })
})
```

*vue/App.vue*

```js
export default {
    data() {
        return {
            token: '',
            credentials: {
                username: 'admin'
            }
        }
    },
    methods: {
        async login() {
            const { data } = await axios.post('http://localhost:3000/login', this.credentials)
            const { token } = data

            this.token = token
        },

        async getCustomers() {
            const options = { headers: { Authorization: `bearer ${ token }` } }
            const { data } = await axios.get('http://localhost:3000/customers')
        }
    }
}
```

### Express.js Authorization Middleware

*express/middlewares/authorize.js*

```js
const jwt = require('jsonwebtoken')
const SECRET = 'SUPERSECRET'

module.exports = (req, res, next) => {
    if (!req.headers['authorization']) {
        res.status(401).end()
    } else {
        const token = req.headers['authorization'].replace('Bearer ', '')

        try {
            const payload = jwt.verify(token, SECRET)
            next()
        } catch(err) {
            res.status(403).end()
        }
    }
}
```

*express/routes/customer.js*

```js
const authorize = require('../middlewares/authorize')

router.get('/customers', authorize, (req, res) => {
    const customers = [1, 2, 3, 4, 5]
    res.json(customers)
})
```

### `sessionStorage` & `cookieStorage`

```js
// set
sessionStorage.setItem('token', token)
// array
sessionStorage.setItem('items', JSON.stringify(items))

// get
const token = sessionStorage.getItem('token') || ''
// array
const items = JSON.parse(sessionStorage.getItem('items')) || []

// remove
sessionStorage.removeItem('token')

// clear
sessionStorage.clear()
```

*vue/App.vue*

```js
export default {
    data() {
        return {
            token: '',
            credentials: {
                username: 'admin'
            }
        }
    },
    mounted() {
        this.token = sessionStorage.getItem('token') || ''
    },
    methods: {
        async login() {
            const { data } = await axios.post('http://localhost:3000/login', this.credentials)
            const { token } = data

            this.token = token
            sessionStorage.setItem('token', token)
        }
    }
}
```
