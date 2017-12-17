## Chapter 02

### AngularJS Application

*Path*

```
+-public
|   |-app.js
```


*public/js/app.js*

```js
angular.module('app', [])
```

*public/index.html*

```html
<body ng-app="app">
    ...
    <script src="/app.js"></script>
</body>
```

### `.run()`

*public/js/app.js*

```js
angular.module('app', [])
    .run(function() {
        console.log('Run!!!')
    })
```

### Controller

> AngularJS Controller defines **scope** of variables

*public/js/app.js*

```js
angular.module('app', [])
    .controller('HomeController', function() {
        console.log('HomeController')
    })
```

*public/index.html*

```html
<body ng-app="app">
    <div ng-controller="HomeController"></div>
</body>
```

### `$scope`

*public/js/app.js*

```js
// dependency injection
.controller('HomeController', function($scope) {
    $scope.title = 'Hello World'
    $scope.numbers = [1, 2, 3, 4, 5]
})
```

*public/index.html*

```html
<div ng-controller="HomeController">
    <p ng-bind="title"></p>
    <p>{{ title }}</p>
    <p>{{ numbers }}</p>
</div>
```

### Controller Function

*public/js/app.js*

```js
.controller('HomeController', function($scope) {
    $scope.greet = function(name) {
        alert('Hello, ' + name)
    }
})
```

*public/index.html*

```html
<div ng-controller="HomeController">
    <button ng-click="greet('Steve')">Greet!</button>
</div>
```

### `ng-repeat` Filter

*public/js/app.js*

```js
.controller('HomeController', function($scope) {
    $scope.customers = [
        ...
    ]
})
```

*public/index.html*

```html
<div ng-controller="HomeController">
    <input ng-model="query" type="text">
    <p>{{ query }}</p>

    <p ng-repeat="c in customers | filter: query">{{ c.firstName }} {{ c.lastName }}</p>
</div>
```

### `ng-repeat` Filter (Field Specific)

*public/index.html*

```html
<div ng-controller="HomeController">
    <input ng-model="query.firstName" type="text">
    <!-- and criteria -->
    <input ng-model="query.lastName" type="text">
    <p>{{ query }}</p>

    <p ng-repeat="c in customers | filter: query">{{ c.firstName }} {{ c.lastName }}</p>
</div>
```

### Sort

*public/index.html*

```html
<!-- ascending -->
<input type="radio" ng-model="sort" value="firstName">
<input type="radio" ng-model="sort" value="lastName">

<!-- descending -->
<input type="radio" ng-model="sort" value="-firstName">

<p>{{ sort }}</p>

<p ng-repeat="c in customers | filter: query | orderBy: sort">
    ...
</p>
```
