## Chapter 01

### Setup

*Path*

```
+-public
|   |-index.html
|   +-css
|   |   |-bulma.min.css
|   +-js
|   |   |-angular.min.js
```

*public/index.html*

```html
<body ng-app>
    {{ 1 + 1 }}

    <link rel="stylesheet" href="/css/bulma.min.css">
    <script src="/js/angular.min.js"></script>
</body>
```

*Terminal*

```
live-server public
```

### `ng-init`

*public/index.html*

```html
<body ng-app>
    <div ng-init="price=50;quty=25">
        <p>Price: <span ng-bind="price"></span></p>
        <p>Quantity: {{ qty }}</p>
        <p>Total: {{ price * qty }}</p>
        <p>Total: {{ price * qty | currency }}</p>
    </div>
</body>
```

### `ng-click`

*public/index.html*

```html
<div ng-init="counter=1">
    <p>Counter {{ counter }}</p>
    <button ng-click="counter=counter+1">+++</button>
</div>
```

### `ng-if`

*public/index.html*

```html
<div ng-init="show=true">
    <button ng-click="show=!show">Toggle</button>
    <p ng-if="show">Show</p>
</div>
```

### `ng-repeat`

*public/index.html*

```html
<div ng-init="numbers=[1, 2, 3, 4, 5]">
    <p>{{ numbers }}</p>
    <p ng-repeat="n in numbers">{{ n }}</p>
</div>
```

### `ng-repeat` (`key: value`)

*public/index.html*

```html
<div ng-init="data={ a: 10, b: 20, c: 30 }">
    <p ng-repeat="(key, value) in data">{{ key }}, {{ value }}</p>
</div>
```

### `ng-model`

*public/index.html*

```html
<div ng-controller="HomeController">
    <input ng-model="title" type="text">
    <p>{{ title }}</p>
</div>
```

### `ng-model` (`<input type="checkbox">`)

*public/index.html*

```html
<div ng-init="status='Single'">
    <input ng-model="status" ng-true-value="'Married'" ng-false-value="'Single'" type="checkbox">
    <p>{{ status }}</p>
</div>
```

### `ng-model` (`<input type="radio">`)

*public/index.html*

```html
<div ng-init="gender='Male'">
    <input ng-model="gender" ng-value="'Male'" type="radio">
    <input ng-model="gender" ng-value="'Female'" type="radio">
    <p>{{ gender }}</p>
</div>
```

### `ng-model` (`<select>`)

*public/index.html*

```html
<div ng-init="food='Rice'">
    <select ng-model="food">
        <option value="Rice">Rice</option>
        <option value="Salad">Salad</option>
        <option value="Noodle">Noodle</option>
    </select>
    <p>{{ food }}</p>
</div>
```
