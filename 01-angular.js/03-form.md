### Chapter 03

### `<form>`

*public/js/app.min.js*

```js
.controller('HomeController', function($scope) {
    $scope.user = {}

    $scope.submitForm = function() {
        console.log($scope.user)
    }
})
```

*public/index.html*

```html
<div ng-controller="HomeController">
    <form ng-submit="submitForm()">
        <input type="submit" value="Save">
    </form>
</div>
```

### `<form>` Validation

*public/index.html*

```html
<form ng-submit="userForm.$valid && submitForm()" name="userForm" novalidate>
    <input name="email" ng-required="true" ng-model="user.email" type="email">
    <input name="password" ng-required="true" ng-model="user.password" type="password">
</form>

<pre>{{ userForm }}</pre>
```

### Validation Message

*public/index.html*

```html
<form>
    <input ng-class="['input', { 'is-danger': userForm.email.$invalid }]">

    <p ng-show="userForm.email.$error.email" class="help is-danger">This email is invalid</p>
    <p ng-show="userForm.email.$dirty && userForm.email.$error.required" class="help is-danger">This field is required</p>
</form>

<pre>{{ userForm.email }}</pre>
```

### RegExp Validation

*public/index.html*

```html
<input name="username" ng-required="true" ng-pattern="/^[a-z]/" ng-model="user.username" type="text">

<p ng-show="userForm.username.$error.pattern" class="help is-danger">This username is invalid</p>
```

### Reference

- [`<input>` Validation Directive](https://docs.angularjs.org/api/ng/directive/input#usage)
