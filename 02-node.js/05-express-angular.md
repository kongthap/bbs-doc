## Chapter 05

### Setup

*Path*

```
|-package.json
|-db.json
+-public
|   |-index.html
|   |-bulma.min.css
|   |-angular.min.js
|   |-app.js
+-src
|   |-index.js
|   |-customer.js
```

### Static Content

*public/index.html*

```html
<html>
<body>
    <link rel="stylesheet" href="/bulma.min.css">
    <script src="/angular.min.js"></script>
    <script src="/app.js"></script>
</body>
</html>
```

*public/app.js*

```js
console.log('Hello World')
```

*src/index.js*

```js
app.use(express.static('public'))
```

### `livereload`

*Terminal*

```
yarn add gulp gulp-livereload --dev
```

*gulpfile.js*

```js
const gulp = require('gulp')
const livereload = require('gulp-livereload')

const src = [
    './src/**/*.*',
    './public/**/*.*'
]

gulp.task('default', () => {
    livereload.listen(options)
    gulp.watch(src).on('change', livereload.changed)
}
```

*public/index.html*

```html
<body>
    <script src="http://localhost:35729/livereload.js?snipver=1"></script>
</body>
```

*Terminal*

```
gulp
```

### AngularJS Setup

*public/app.js*

```js
angular.module('app', [])
    .controller('GetCustomers', function($scope, $http) {
        $scope.customers = []

        $scope.getCustomers = function() {
            $http.get('http://localhost:3000/customers')
                .then(function(res) {
                    $scope.customers = res.data
                })
        }
    })
```
