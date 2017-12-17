## Chapter 04

### Vue Router

![](https://i.cubeupload.com/pSeOgX.png)

### Setup

*Path*

```
+-src
|   |-App.vue
|   |-main.js
|   |-routes.js
|   |-Navbar.vue
|   |-Customer.vue
|   |-CustomerProfile.vue
|   |-guard.js
|   |-GuardComponent.js
```

*Terminal*

```
yarn add vue-router
```

*src/routes.js*

```js
const Home = {
    name: 'home',
    template: `<p>Home</p>`
}

const Contact = {
    name: 'contact',
    template: `<p>Contact</p>`
}
```

*src/routes.js*

```js
const PageNotFound = {
    name: 'pageNotFound',
    template: `<p>PageNotFound</p>`
}

// setup routes
export default [
    { path: '/', component: Home },
    { path: '/contact', component: Contact },
    { path: '*', component: PageNotFound }
]
```

*src/main.js*

```js
import VueRouter from 'vue-router'
import routes from './routes'

Vue.use(VueRouter)

// setup router
const router = new VueRouter({
    mode: 'history',
    routes
})

// apply router into vue instance
new Vue({
    router
})
```

*src/App.vue*

```html
<router-view></router-view>
```

### Navbar

*src/Navbar.vue*

```html
<nav class="nav">
    <div class="nav-right">
        <router-link :exact="true" to="/"
            class="nav-item is-tab"
            activeClass="is-active">
            Home
        </router-link>
    </div>
</nav>
```

*src/App.vue*

```html
<navbar />
```

```js
import Navbar from './Navbar.vue'

export default {
    components: {
        navbar
    }
}
```

### Parameterized Route

*index.html*

```html
<head>
    <base href="/">
</head>
```

*src/routes.js*

```js
export default [
    { path: '/customers/:id', component: CustomerProfile }
]
```

*src/Customer.vue*

```html
<router-link to="`/customers/1001`">1001</router-link>
<router-link to="`/customers/1002`">1002</router-link>
```

*src/CustomerProfile.vue*

```html
<p>Customer ID: {{ customerId }}</p>
```

```js
export default {
    computed: {
        customerId() {
            return this.$route.params.id
        }
    }
}
```

### Router Guard

*src/App.vue*

```html
<router-view :isAuth="isAuth" />
```

*src/guard.js*

```js
export const beforeRouteEnter = (to, from, next) => {
    next(vm => {
        console.log(vm)

        if (!vm.isAuth) {
            next(false)
            next({ path: '/' })
            // next({ path: '/login' })
        }
    })

    next()
}
```

> `vm` callback variable is the component itself

*src/GuardComponent.js*

```js
import { beforeRouteEnter } from './guard'

export default {
    beforeRouteEnter,
    props: [ 'isAuth' ]
}
```

*src/CustomerProfile.vue*

```js
import Vue from 'vue'
import GuardComponent from './GuardComponent'

export default Vue.extend({
    mixins: [ GuardComponent ]
})
```
