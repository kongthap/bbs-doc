## Chapter 08

### Setup

*Path*

```
|-gulpfile.js
+-app
|   |-app.js
|   |-route.js
|   |-customer.js
+-public
|   |-index.html
```

*Terminal*

```
yarn add gulp --dev
yarn add gulp-concat gulp-ng-annotate gulp-uglify --dev

# or
npm install gulp --save-dev
```

*gulpfile.js*

```js
const gulp = require('gulp')
const concat = require('gulp-concat')
const uglify = require('gulp-uglify')
const annotate = require('gulp-ng-annotate')

const src = [
    './app/app.js',
    './app/route.js',
    './app/customer.js'
]

gulp.task('default', () => {
    gulp.watch(src, [ 'build' ])
})

gulp.task('build', () => {
    return gulp.src(src)
        .pipe(concat('app.min.js'))
        .pipe(annotate())
        .pipe(uglify())
        .pipe(gulp.dest('public'))
})
```
