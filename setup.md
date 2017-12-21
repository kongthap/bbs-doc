## Setup

[ติดตั้งโปรแกรม](https://gist.github.com/tutor4dev/dd4d48872798ecbd09ad8454e4719518)

### Contact

- LINE ID: jeud
- Facebook: @kongthap.thammachat

### Visual Studio Code Extensions

- Babel JavaScript
- npm Intellisense
- Path Intellisense
- vue (liuji-jim)

### `npm` Global Package

*Terminal*

```
npm -g install yarn
npm -g install live-server
npm -g install json-server
npm -g install nodemon
npm -g install vue-cli
```

### Libraries & Assets

- [`angular.js`](https://cdnjs.cloudflare.com/ajax/libs/angular.js/1.6.5/angular.js)
- [`angular-ui-router.js`](https://cdnjs.cloudflare.com/ajax/libs/angular-ui-router/1.0.3/angular-ui-router.js)
- [`vue.js`](https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.10/vue.js)
- [`bulma.min.css`](https://cdnjs.cloudflare.com/ajax/libs/bulma/0.6.1/css/bulma.min.css)
- [`animate.min.css`](https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.5.2/animate.min.css)
- [`db.json`](https://mega.nz/#!V41kkB5T!5zvBvVrGO49vUvVtyzY5oGPgEFD5xeDSn5mIsVBHfUA)
- [`mysql.northwind.sql`](https://mega.nz/#!8hNXwYha!zRJfxgIA9ruWf6DifmoR9hYGTJmXnjOOq--_GAPdrwQ)

### Snippet

```js
$scope.customers = [
    {
      "id": 101,
      "firstName": "Waller",
      "lastName": "Kent",
      "age": 34,
      "gender": "M"
    },
    {
      "id": 102,
      "firstName": "Deborah",
      "lastName": "Davis",
      "age": 26,
      "gender": "F"
    },
    {
      "id": 103,
      "firstName": "Hayden",
      "lastName": "Sherman",
      "age": 21,
      "gender": "M"
    },
    {
      "id": 104,
      "firstName": "Fletcher",
      "lastName": "Hansen",
      "age": 30,
      "gender": "M"
    },
    {
      "id": 105,
      "firstName": "Jeannette",
      "lastName": "Hays",
      "age": 25,
      "gender": "F"
    },
    {
      "id": 106,
      "firstName": "Stafford",
      "lastName": "Lindsay",
      "age": 29,
      "gender": "M"
    },
    {
      "id": 107,
      "firstName": "Minerva",
      "lastName": "Cash",
      "age": 25,
      "gender": "F"
    },
    {
      "id": 108,
      "firstName": "Madeleine",
      "lastName": "Ballard",
      "age": 33,
      "gender": "F"
    },
    {
      "id": 109,
      "firstName": "Dennis",
      "lastName": "Cannon",
      "age": 35,
      "gender": "M"
    },
    {
      "id": 110,
      "firstName": "Margery",
      "lastName": "Jensen",
      "age": 34,
      "gender": "F"
    }
]
```

### Docker

*Terminal*

```
# mariadb
docker run -d --rm -p 3306:3306 -e MYSQL_ALLOW_EMPTY_PASSWORD=yes --name db mariadb

# import
mysql -h 192.168.99.100 -u root -p < mysql.northwind.sql
```
