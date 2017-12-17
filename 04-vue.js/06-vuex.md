## Chapter 06

### Vuex

![](https://i.cubeupload.com/x4hraV.png)

![](https://vuex.vuejs.org/en/images/vuex.png)

### Setup

*Path*

```
+-src
|   |-App.vue
|   |-main.js
|   |-store.js
```

*Terminal*

```
yarn add vuex
```

*src/store.js*

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

// setup vuex store
export default new Vuex.Store({

})
```

*src/main.js*

```js
import store from './store'

// apply vuex store into vue instance
new Vue({
    store
})
```

### `state`

*src/store.js*

```js
export default new Vuex.Store({
    state: {
        amount: 100
    }
})
```

*vue/App.vue*

```html
<p>{{ amount }}</p>
```

```js
export default {
    computed: {
        amount() {
            return this.$store.state.amount
        }
    }
}
```

> `$store` is passed into every components

### `mapState()`

*vue/App.vue*

```html
<p>{{ amount }}</p>
```

```js
import { mapState } from 'vuex'

export default {
    computed: {
        // this.$store.state.amount
        ...mapState([ 'amount' ])
    }
}
```

### `getters`

*src/store.js*

```js
export default new Vuex.Store({
    getters: {
        usAmount(state) {
            return state.amount * 1 / 32.51
        }
    }
})
```

### `mapGetters()`

*vue/App.vue*

```js
import { mapState, mapGetters } from 'vuex'

export default {
    computed: {
        ...mapState([ 'amount' ]),
        // this.$store.getters.usAmount
        ...mapGetters([ 'usAmount' ])
    }
}
```

### `mutations`

*src/store.js*

```js
export default new Vuex.Store({
    mutations: {
        mutateAmount(state) {
            // no return
            state.amount += 100
        }
    }
})
```

### `mapMutations()`

*vue/App.vue*

```html
<button @click="mutateAmount">+100</button>
```

```js
import { mapMutations } from 'vuex'

export default {
    methods: {
        // this.$store.commit('mutateAmount')
        ...mapMutations([ 'mutateAmount' ])
    }
}
```

### `mutations` with Payload

*src/store.js*

```js
export default new Vuex.Store({
    mutations: {
        mutateAmount(state, payload) {
            // payload: { }
            state.amount += payload.amount
        }
    }
})
```

*vue/App.vue*

```html
<button @click="mutateAmount({ amount: 150 })">+150</button>
<button @click="mutateAmount({ amount: -50 })">-50</button>
```

### `actions`

*src/store.js*

```js
export default new Vuex.Store({
    actions: {
        increment(context) {
            context.commit('mutateAmount', { amount: 100 })
        }
    }
})
```

### `mapActions()`

*vue/App.vue*

```html
<button @click="increment">+100</button>
```

```js
import { mapActions } from 'vuex'

export default {
    methods: {
        // this.$store.dispatch('increment')
        ...mapActions([ 'increment' ])
    }
}
```

### `actions` with Payload

*src/store.js*

```js
export default new Vuex.Store({
    actions: {
        increment(context, payload) {
            context.commit('mutateAmount', { amount: payload.amount })
        }
    }
})
```

*vue/App.vue*

```html
<button @click="increment({ amount: 200 })">+200</button>
```

### Async `actions`

*src/store.js*

```js
export default new Vuex.Store({
    state: {
        customers: [],
        waiting: false
    },
    mutations: {
        fetchStart(state) {
            state.waiting = true
        },
        fetchSuccess(state, payload) {
            state.waiting = false
            state.customers = payload.customers
        }
    }
})
```

*src/store.js*

```js
export default new Vuex.Store({
    actions: {
        async getCustomers(context) {
            context.commit('fetchStart')

            const { data } = await axios.get(...)
            context.commit('fetchSuccess', { customers: data })
        }
    }
})
```
