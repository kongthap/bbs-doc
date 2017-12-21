## Chapter 01

### VS Code

*Settings*

```json
{
    "emmet.excludeLanguages": [],
    "emmet.showExpandedAbbreviation": "always",
    "emmet.syntaxProfiles": {
        "blade": "html",
        "javascript": "html",
        "html": {
            "self_closing_tag": false,
            "tag_case": "lower"
        },
        "vue": {},
        "xml": {}
    },
    "emmet.triggerExpansionOnTab": true
}
```

### Setup

*Terminal*

```
vue init webpack-simple <project>
```

*Path*

```
|-.babelrc
|-index.html
|-package.json
|-webpack.config.js
 +-src
|   |-App.vue
|   |-main.js
```

*Terminal*

```
# install dependency
yarn
# start
yarn dev
```

### Vue.js Instance

*src/main.js*

```js
// const Vue = require('vue')
import Vue from 'vue'
import App from './App.vue'

new Vue({
    el: '#app',
    render: h => h(App)
})
```

*index.html*

```html
<body>
    <div id="app"></div>
    <script src="/dist/build.js"></script>
</body>
```

### `App` Component

*src/App.vue*

```html
<template>
    ...
</template>
```

```html
<script>
export default {
    name: 'app',
    data() {
        return {
            msg: 'Welcome to Your Vue.js App'
        }
    }
}
</script>
```

### Declarative Programming

*src/App.vue*

```html
<template>
    {{ msg }}
</template>
```

```html
<script>
export default {
    data() {
        return {
            msg: 'Welcome to Your Vue.js App'
        }
    }
}
</script>
```

### Expression

*src/App.vue*

```html
<template>
    <div>
        <p>{{ n + 1 }}</p>
        <p>{{ ok ? 'YES' : 'NO' }}</p>
        <p>{{ message.split('').reverse().join('') }}</p>
    </div>
</template>
```

```html
<script>
export default {
    data() {
        return {
            n: 20,
            ok: true,
            message: 'hello'
        }
    }
}
</script>
```

### `data()` State & Reactivity

![](https://u.cubeupload.com/jeud/68747470733a2f2f692e.png)

*src/App.vue*

```html
<input v-model="msg" type="text">
{{ msg }}
```

### `computed`

*src/App.vue*

```html
<input type="text" v-model="firstName">
<input type="text" v-model="lastName">

<p>{{ fullName }}</p>
```

```js
export default {
    data() {
        return {
            firstName: '',
            lastName: ''
        }
    },
    computed: {
        fullName() {
            return `${ this.firstName } ${ this.lastName }`
        }
    }
}
```

### Condition

*src/App.vue*

```html
<p v-if="status">This is visible</p>
<p v-else>This is not visible</p>

<p v-if="gender=='M'">Male</p>
<p v-else-if="gender=='F'">Female</p>
<p v-else>Undefined Gender</p>
```

```js
export default {
    data() {
        return {
            status: true,
            gender: 'M'
        }
    }
}
```

### Loop

*src/App.vue*

```html
<p v-for="n in numbers">{{ n }}</p>
```

```js
export default {
    data() {
        return {
            numbers: [1, 2, 3, 4, 5]
        }
    }
}
```

### Event

*src/App.vue*

```html
<button v-on:click="show=!show">Toggle</button>
<button @click="show=!show">Toggle</button>

<p>{{ show }}</p>
```

```js
export default {
    data() {
        return {
            show: true
        }
    }
}
```

### `methods`

*src/App.vue*

```html
<button @click="handleClick">Click Me</button>
<p>{{ msg }}</p>
```

```js
export default {
    data() {
        return {
            msg: 'Hello World'
        }
    },
    methods: {
        handleClick(event) {
            console.log('Hello World')
            console.log(event)
            this.msg = 'Hi, there!'
        }
    }
}
```

### `methods` & Argument

*src/App.vue*

```html
<button @click="handleClick('Hi, there!')">Click Me</button>
<p>{{ msg }}</p>
```

```js
export default {
    data() {
        return {
            msg: 'Hello World'
        }
    },
    methods: {
        handleClick(param, event) {
            console.log('Hello World')
            console.log(event)
            this.msg = param
        }
    }
}
```

### Event & Modifier

*src/App.vue*

```html
<input @keyup="handleKeyup" type="text">
<input @keyup.enter="handleKeyup" type="text">
```

```js
export default {
    methods: {
        handleClick(event) {
            console.log(event.target.value)
        }
    }
}
```

### Attribute Binding

*src/App.vue*

```html
<a href="https://google.com">google.com</a>

<a v-bind:href="url">google.com</a>
<a v-bind:href="'https://google.com'">google.com</a>
<a :href="'https://google.com'">google.com</a>
```

```js
export default {
    data() {
        return {
            url: 'https://google.com'
        }
    }
}
```

### Based CSS

*Path*

```
+-assets
|   |-bulma.min.css
```

*index.html*

```html
<body>
    <section class="section">
        <div class="container">
            <div id="app"></div>
        </div>
    </section>

    <link rel="stylesheet" href="/assets/bulma.min.css">
    <script src="/dist/build.js"></script>
</body>
```

### CSS Binding

*src/App.vue*

```html
<button :class="[ 'button','is-primary' ]">OK</button>
<button :class="classNames">Cancel</button>
```

```js
export default {
    data() {
        return {
            classNames: [ 'button', 'is-danger' ]
        }
    }
}
```

### Dynamic CSS Binding

*src/App.vue*

```html
<button :class="classNames">OK</button>
```

```js
export default {
    data() {
        return {
            isPrimary: true
        }
    }
    computed: {
        classNames() {
            return [
                'button',
                { 'is-primary': this.isPrimary }
            ]
        }
    }
}
```

### Style Binding

*src/App.vue*

```html
<h3 :style="{ color: 'red' }">Hello</h3>
<h3 :style="style">World</h3>
```

```js
export default {
    data() {
        return {
            style: {
                color: '#42b983',
                fontWeight: 'bold'
            }
        }
    }
}
```

### Dynamic Style Binding

*src/App.vue*

```js
export default {
    data() {
        return {
            isBold: true
        }
    },
    computed: {
        style() {
            const baseStyle = { color: '#42b983' }

            return this.isBold
                ? { ...baseStyle, fontWeight: 'bold' }
                : baseStyle
        }
    }
}
```

*Terminal*

```
yarn add babel-preset-stage-3 --save-dev
```

*.babelrc*

```json
{
    "presets": [
        ["env", { "modules": false }],
        "stage-3"
    ]
}
```

### Vue.js Lifecycle Method

![](https://codingexplained.com/wp-content/uploads/2017/04/Vue-instance-lifecycle-Page-1.png)

*Vue Instance* & *Component*

```js
export default {
    create() {
        // reigister, ajax (SSR)
    },
    mounted() {
        // ajax
    },
    updated() {
        // ajax
    },
    destroyed() {
        // unregister
    }
}
```
