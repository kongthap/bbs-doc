## Chapter 07

### `webpack`

![](https://u.cubeupload.com/jeud/1Qo4yWofQHQKSOtLtTD5.png)

![](https://u.cubeupload.com/jeud/102016buildfastwithw.jpg)

### Build

*Terminal*

```
# build using webpack
yarn build
```

*Path*

```
+-[vue-project]
|   +-dist
|   |   |-build.js
|   |   |-build.js.map
+-[express-project]
|   +-src
|   |   |-index.js
|   +-public
|   |   |-index.html
|   |   +-dist
|   |   |   |-build.js
|   |   |   |-build.js.map
```

*[express-project]/src/index.js*

```js
app.use(express.static('public'))
```

*[express-project]/public/index.html*

```html
<body>
    <div id="app"></div>
    <script src="/dist/build.js"></script>
</body>
```
