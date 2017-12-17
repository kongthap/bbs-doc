## Chapter 05

### `$http`

*Path*

```
|-db.json
```

*Terminal*

```
json-server db.json
```

*public/js/app.js*

```js
angular.module('app', [])
    .constant('API', 'http://localhost:3000/')
    .controller('HomeController', function($scope, $http) {
        $scope.customers = []

        $scope.getCustomers = function() {
            $http.get(API + 'customers')
                .then(function(res) {
                    $scope.customers = res.data
                })
                .catch(function(err) {
                    console.log(err)
                })
        }
    })
```

### `$http` & Factory

*public/js/app.js*

```js
.factory('CustomerFactory', function($http, API) {
    return {
        getCustomers: function() {
            return $http.get(API + 'customers')
        }
    }
})
.controller('HomeController', function($scope, CustomerFactory) {
    $scope.customers = []

    $scope.getCustomers = function() {
        CustomerFactory.getCustomers()
            .then(function(res) {
                $scope.customers = res.data
            })
    }
})
```

### `$http` & `POST` Request

*public/js/app.js*

```js
.factory('SupplierFactory', function($http, API) {
    return {
        insertSupplier function(suupplier) {
            return $http.post(API + 'suppliers', supplier)
        }
    }
})
.controller('HomeController', function($scope, SupplierFactory) {
    $scope.supplier = {}

    $scope.submitForm = function() {
        SupplierFactory.insertSupplier($scope.supplier)
            .then(function(res) {
                console.log(res.data)
            })
    }
})
```

### Authentication

*public/js/app.js*

```js
.service('Auth', function($http) {
    this.isAuth = false

    this.login = function() {
        // backend authentication
        this.isAuth = true
        $http.defaults.headers.common['Authorization'] = 'Bearer abcde12345'
    }

    this.logout = function() {
        this.isAuth = false
        delete $http.defaults.headers.common['Authorization']
    }
})
```
