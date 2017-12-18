### Chapter 06

### `ui-router`

*Path*

```
+-public
|   |-navbar.html
|   +-views
|   |   |-home.html
|   |   |-about.html
|   |   |-customer.html
|   |   |-customer-profile.html
```

*public/index.html*

```html
<body ng-app="app">
    ...
    <script src="/js/angular-ui-router.min.js"></script>
</body>
```

*public/app.js*

```js
angular.module('app', [ 'ui.router' ])
```

### Router & State

*public/app.js*

```js
angular.module('app', [ 'ui.router' ])
    .config(function($stateProvider, $urlRouterProvider) {
        $stateProvider
            .state('home', {
                url: '/',
                template: '<h3>Home</h3>'
            })
            .state('about', {
                url: '/',
                template: '<h3>About</h3>'
            })

        $urlRouterProvider.otherwise('/')
    })
```

*public/navbar.html*

```html
<a ui-sref="home">Home</a>&nbsp;|
<a ui-sref="about">About</a>
```

*public/index.html*

```html
<div ng-include="'navbar.html'"></div>
<ui-view></ui-view>
```

### `html5Mode`

*public/index.html*

```html
<head>
    <base href="/">
</head>
```

*public/app.js*

```js
.config(function($locationProvider) {
    $locationProvider.html5Mode(true)
})
```

### `templateUrl`

*public/views/home.html*

```html
<h3>Home</h3>
```

*public/app.js*

```js
.config(function($stateProvider, $urlRouterProvider) {
    $stateProvider
        .state('home', {
            url: '/',
            templateUrl: 'views/home.html'
        })
})
```

### Router & Controller

*public/app.js*

```js
.config(function($stateProvider, $urlRouterProvider) {
    $stateProvider
        .state('home', {
            url: '/',
            templateUrl: 'views/home.html',
            controller: 'HomeController'
        })
})
.controller('HomeController', function($scope) {
    console.log('HomeController')
})
```

### Parametered Route

*public/app.js*

```js
.config(function($stateProvider, $urlRouterProvider) {
    $stateProvider
        .state('customerProfile', {
            url: '/customer/:id',
            template: '<h3>Customer ID: {{ id }}</h3>'
            controller: 'CustomerProfileController'
        })
})
.controller('CustomerProfileController', function($scope, $stateParams) {
    $scope.id = $stateParams.id
})
```

*public/views/home.html*

```html
<a ui-sref="customerProfile({ id: 123 })">Customer</a>
```

### Router Guard

*public/app.js*

```js
.config(function($stateProvider, $urlRouterProvider) {
    $stateProvider
        .state('customerProfile', {
            resolve: {
                auth($q, Auth) {
                    return $q(function(resolve, reject) {
                        if (Auth.isAuth)
                            resolve()
                        else
                            reject()
                    })
                }
            }
        })
})
.run(function ($state) {
    $state.defaultErrorHandler(function (error) {
        // $state.go('login', { ... })
        console.log(error)
    })
})
.service('Auth', function() {
    this.isAuth = false

    this.login = function() {
        // backend authentication
        this.isAuth = true
    }

    this.logout = function() {
        this.isAuth = false
    }
})
```
