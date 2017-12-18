## Chapter 07

### Setup

*Path*

```
+-public
|   |-index.html
|   |-app.js
|   |-route.js
|   |-customer.js
```

### Setter & Getter

*Code*

```js
// setter
angular.module('app', [])
// getter
angular.module('app')
```

*public/app.js*

```js
// setter
angular.module('app', [ 'ui.router' ])
    .constant('API', 'http://localhost:3000/')
    .service('Auth', function() {
        ...
    })
```

*public/route.js*

```js
// getter
angular.module('app')
    .config(function($stateProvider, $urlRouterProvider) {
        ...
    })
```

*public/index.html*

```html
<body>
    <script src="/app.js"></script>
    <script src="/route.js"></script>
</body>
```

### Module Dependency

*public/app.js*

```js
// setter
angular.module('app', [ 'ui.router', 'customer' ])
```

*public/app.js*

```js
// setter
angular.module('customer', [])
    .factory('CustomerFactory', function($http, API) {
        ...
    })
    .controller('CustomerController', function($scope, CustomerFactory) {
        ...
    })
```

*public/index.html*

```html
<body>
    <script src="/customer.js"></script>
</body>
```
