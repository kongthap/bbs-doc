### Chapter 04

### Global & Services

- `.value()`
- `.constant()`
- `.service()`
- `.factory()`
- `.provider()`

### `.value()` & `.constant()`

*public/js/app.js*

```js
angular.module('app', [])
    .value('UserProfile', {
        username: 'steve',
        role: 'admin'
    })
    .constant('API', 'http://api.example.com')
    .controller('HomeController', function($scope, UserProfile, API) {
        console.log(UserProfile, API)
    })
```

### `.service()`

*public/js/app.js*

```js
angular.module('app', [])
    .service('CalculatorService', function() {
        this.plusNumbers = function(n1, n2) {
            return n1 + n2
        }

        this.multiplyNumbers = function(n1, n2) {
            return n1 * n2
        }
    })
    .controller('HomeController', function($scope, CalculatorService) {
        console.log(CalculatorService.plusNumbers(10, 20))
    })
```

### `.factory()`

*public/js/app.js*

```js
angular.module('app', [])
    .service('CalculatorFactory', function() {
        return {
            plusNumbers: function(n1, n2) {
                return n1 + n2
            },

            multiplyNumbers: function(n1, n2) {
                return n1 * n2
            }
        }
    })
```

### `.provider()`

*public/js/app.js*

```js
.provider('vat', function() {
    var currency = '$'
    var vat = 7

    return {
        $get: function() {
            return {
                addVat: function(amount) {
                    return currency + ' ' + amount * (100 + vat) / 100
                },

                extractVat: function(amount) {
                    return currency + ' ' + amount * (100 - vat) / 100
                }
            }
        }
    }
})
.controller('HomeController', function($scope, vat) {
    ...
})
```

### `.provider()` & Configuration

*public/js/app.js*

```js
.config(function(vatProvider) {
    vatProvider.setCurrency('B')
})
.provider('vat', function() {
    var currency = '$'
    var vat = 7

    return {
        $get: function() {
            return {
                ...
            }
        },

        setCurrency: function(value) {
            currency = value
        },

        setVat: function(value) {
            vat = value
        }
    }
})
