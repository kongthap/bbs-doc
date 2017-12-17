## Chapter 02

### Setup

*Path*

```
+-src
|   |-App.vue
|   |-main.js
```

*src/App.vue*

```html
<input v-model="person.firstName" type="text">
<input v-model="person.lastName" type="text">
<input v-model="person.email" type="email">

<input type="submit" value="Submit">
```

```js
export default {
    data() {
        return {
            person { }
        }
    },
    methods: {
        handleSubmit() {
            console.log(this.person)
        }
    }
}
```

### Reactive Object & Plain JavaScript Object

*src/App.vue*

```js
export default {
    methods: {
        handleSubmit() {
            const personString = JSON.stringify(this.person)
            const personObject = JSON.parse(personString)
            console.log(personObject)
        }
    }
}
```

### `<input type="checkbox">`

*src/App.vue*

```html
<input v-model="person.single" type="checkbox">
```

```js
export default {
    data() {
        return {
            person: {
                single: true
            }
        }
    }
}
```

### `<input type="radio">`

*src/App.vue*

```html
<input v-model="person.gender" value="M" type="radio">
<input v-model="person.gender" value="F" type="radio">
```

```js
export default {
    data() {
        return {
            person: {
                gender: 'M'
            }
        }
    }
}
```

### `<select>`

*src/App.vue*

```html
<select v-model="person.income">
    <option disabled value="">Please Choose</option>
    <option v-for="o in options" :value="o.value">{{ o.text }}</option>
</select>
```

```js
export default {
    data() {
        return {
            person: {

            },
            options: [
                { value: 'A', text: '< 20,000' },
            ]
        }
    }
}
```

### `<select>` & `<groupopt>`

*src/App.vue*

```html
<select v-model="person.language">
    <optgroup v-for="go in groupOptions"
        :label="go.label">
        <option v-for="o in go.options"
            :value="o.value">{{ o.text }}</option>
    </optgroup>
</select>
```

```js
export default {
    data() {
        return {
            groupOptions: [
                {
                    label: 'Server-side',
                    options: [ { value: 'C', text: 'C#' } ]
                }
            ]
        }
    }
}
```

### Form Validation & `vee-validate`

*Terminal*

```
yarn add vee-validate
```

*src/main.js*

```js
import VeeValidate from 'vee-validate'

Vue.use(VeeValidate)

new Vue({
    ...
})
```

### Validation Rule

*src/App.vue*

```html
<input
    v-model="person.firstName"
    name="firstName"
    v-validate="'required|alpha'"
    :class="className('firstName')"
    type="text">

<p class="help is-danger">{{ errors.first('firstName') }}</p>
```

```js
export default {
    methods: {
        className(fieldName) {
            ...
        }
    }
}
```

### Form Submission

*src/App.vue*

```js
export default {
    methods: {
        handleSubmit() {
            this.$validator.validateAll()
                .then(result => {
                    if(result) {
                        // pass
                    }

                    // fail
                })
        }
    }
}
```
