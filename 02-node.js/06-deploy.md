### Chapter 06

### Compression `gzip`

*Terminal*

```
yarn add compression
```

*src/index.js*

```js
const express = require('express')
const compression = require('compression')
const app = express()

app.use(compression())

app.use(express.static('public'))

app.get('/', (req, res) => {
    return res.json([ ... ])
})
```

### Cache Control

*Code*

```js
const options = {
    etag: true,
    lastModified: true,
    maxAge: '60d',
    setHeaders(res, path, stat) {
        res.set('x-timestamp, Date.now())
        res.set('...', '...')
    }
}

app.use(express.static('public'), options)
```

### SSL

*Path*

```
|-package.json
+-src
|   |-index.js
|   +-ssl
|   |   |-server.crt
|   |   |-server.key
```

*Terminal*

```
# generate private key + self-signed certificate
openssl req -newkey rsa:2048 -nodes -keyout localhost.key -x509 -days 365 -out server.crt

openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:2048 -out server.key
```

*src/index.js*

```js
const fs = require('fs')
const express = require('express')

const app = express()

const httsOptions = {
    cert: fs.readFileSync('./ssl/server.crt'),
    key: fs.readFileSync('./ssl/server.key')
}

require('https').createServer(httpsOptions, app)
    .listen(3443, () => {
        console.log('...')
    })
```

### Production Server Setup

*Path*

```
|-package.json
+-src
|   |-index.js
|   |-...
```

*Terminal*

```
# install dependencies
yarn
```

### Production Environment

- `NODE_ENV=production`
- `PORT=80`

*Terminal+*

```
# windows
SET NODE_ENV=production

# linux
export NODE_ENV=production
```

*src/index.js*

```js
const port = process.env.PORT || 3000
app.listen(port)
```

### `pm2`

*Terminal*

```
# install
npm -g install pm2
# update
pm2 update

# list
pm2 list

# add & start
pm2 start src/index.js
pm2 start src/index.js --name api

# restart
pm2 restart 0
pm2 restart api

# stop
pm2 stop api

# delete
pm2 delete api
```
