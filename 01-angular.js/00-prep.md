## Chapter 00

### DOM Render Using HTML

```html
<body>
    <h1>Hello World</h1>
</body>
```

### DOM Render Using JavaScript

```html
<body>
</body>
```

```js
const text = 'Hello World'
const h1 = document.createElement('h1')
h1.appendChild(text)

document.body.appendChild(h1)
```

### AngularJS

```html
<h1>{{ title }}</h1>
```

```js
$scope.title = 'Hello World'

$scope.changeTitle = function() {
    $scope.title = 'Hi, there!'
}
```

### AngularJS Code Pattern

```js
angular.module('app', [])
    .config(function() {
        ...
    })
    .factory(function($http) {
        ...
    })
    .controller('Home', function($scope) {
        ...
    })
```
