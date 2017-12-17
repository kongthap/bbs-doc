## Chapter 03

### Setup

*Path*

```
 +-src
|   |-App.vue
|   |-Level1.vue
|   |-Level2.vue
```

*Hierarchy*

```html
<app>
    <level1>
        <level2>
```

### Vue.js Component

*src/Level1.vue*

```html
<h3>Level1</h3>
```

```js
export default {
}
```

### Component Registration

*src/App.vue*

```html
<level1 />
```

```js
import Level1 from 'level1'

export default {
    components: { level1 }
}
```

### `<slot>`

*src/App.vue*

```html
<level1>Hello World</level1>
```

*src/Level1.vue*

```html
<slot />
```

### Communication Between Components

![](https://vuejs.org/images/props-events.png)

### `props`

*src/App.vue*

```html
<input v-model.number="value" type="range" min="1" max="20">

<level1 :value="value"></level1>
```

```js
export default {
    data() {
        return {
            value: 1
        }
    }
}
```

*src/Level1.vue*

```html
<p>{{ value }}</p>
```

```js
export default {
    props: [ 'value' ]
}
```

### Default `props`

*src/Level1.vue*

```js
export default {
    props: {
        value: {
            default: 1
        },
        foo: {
            default: 'FOO'
        }
    }
}
```

### `props` Validation

*src/Level1.vue*

```js
export default {
    props: {
        value: {
            required: true
            type: Number
        },
        foo: {
            required: true,
            type: String
        },
        bar: [ String, Number ],
        baz: Array
    }
}
```

### `$emit()`

*src/Level1.vue*

```js
export default {
    methods: {
        resetValue() {
            this.$emit('reset')
        }
    }
}
```

*src/App.vue*

```html
<level1 @reset="handleReset" :value="value"></level1>
```

```js
export default {
    methods: {
        handleReset() {
            ...
        }
    }
}
```

### Global `$emit()`

*EventBus.js*

```js
import Vue from 'vue'

export default EventBus = new Vue()
```

*Child.vue*

```js
import EventBus from './EventBus'

EventBus.$emit('fooEvent', { foo: 'foo' })
```

*Parent.vue*

```js
import EventBus from './EventBus'

EventBus.$on('fooEvent', (data) => {
    console.log(data)
})
```

### `mixins`

*src/BaseComponent.js*

```js
export default {
    data() {
        return {
            global: 'Hello World'
        }
    },
    methods: {
        greet() {
            alert('Hello World')
        }
    }
}
```

*src/App.vue*

```html
<template>
    <div class="box">
        {{ global }}
        {{ local }}
        <button @click="greet">Hello</button>
    </div>
</template>
```

```js
import Vue from 'vue'
import BaseComponent from './BaseComponent'

export default Vue.extend({
    mixins: [ BaseComponent ],
    data() {
        return {
            local: 'Vue.js'
        }
    }
})
```
