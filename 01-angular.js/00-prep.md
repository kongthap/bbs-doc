## Chapter 00

### HTTP Lifecycle

![](https://betterexplained.com/wp-content/uploads/compression/HTTP_request.png)

### DOM Render Using HTML (PHP, .NET, Node.js, etc)

```html
<body>
    <h1>Hello World</h1>
</body>
```

### DOM Render Using JavaScript

![](https://image.slidesharecdn.com/clientserverrendering-140707022702-phpapp01/95/client-vs-server-rendering-42-638.jpg?cb=1404959822)

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

![](https://cdn-images-1.medium.com/max/1600/1*m-FZj4M4_20rJs_nFhkdAg.png)

### AngularJS Framework

```html
<h1>{{ title }}</h1>
```

```js
$scope.title = 'Hello World'

$scope.changeTitle = function() {
    $scope.title = 'Hi, there!'
}
```

### AngularJS `$digest()` Loop

![](https://docs.angularjs.org/img/guide/concepts-startup.png)

### Angular Dependency Injection

![](http://i2.wp.com/www.geekhours.com/wp-content/uploads/2016/07/dependency-injection-angularjs.png)

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
