## Chapter 05

### Setup

*Path*

```
+-src
|   |-App.vue
|   |-main.js
|   |-Customer.vue
|   |-CustomerProfile.vue
|   |-SearchCustomer.vue
|   |-Pagination.vue
```

*Terminal*

```
yarn add axios
```

*src/Customer.vue*

```js
import axios from 'axios'

export default {
    data() {
        return {
            customers: []
        }
    },
    mounted() {
        axios.get('http://localhost:3000/customers')
            .then((res) => {
                this.customers = res.data
            })
    }
}
```

### `async` & `await`

*Terminal*

```
yarn add babel-plugin-transform-runtime --dev
```

*.babelrc*

```json
{
    "plugins": [
        "transform-runtime"
    ]
}
```

*src/Customer.vue*

```js
import axios from 'axios'

export default {
    data() {
        return {
            customers: []
        }
    },
    async mounted() {
        const { data } = await axios.get('http://localhost:3000/customers')
        this.customers = data
    }
}
```

### Customer Profile

*src/Customer.vue*

```html
<router-link :to="...">...</router-link>
```

*src/CustomerProfile.vue*

```js
export default {
    async mounted() {
        ...
    }
}
```

### `regexp` & Filter

*src/Customer.vue*

```js
export default {
    data() {
        return {
            searchBy: ''
        }
    },
    computed: {
        filterCustomers() {
            const pattern = new RegExp(this.searchBy, 'i')

            return this.customers.filter(c => {
                return pattern.test(c.firstName)
            })
        }
    }
}
```

### Sorting

*src/Customer.vue*

```html
<a @click.prevent="sortBy='firstName'" href="#">Name</a>
```

```js
export default {
    data() {
        return {
            sortBy: 'id'
        }
    }
}
```

*src/Customer.vue*

```js
export default {
    computed: {
        sortCustomers() {
            return this.filterCustomers.sort((a, b) => {
                if (a[this.sortBy] < b[this.sortBy])
                    return -1
                if (a[this.sortBy] > b[this.sortBy])
                    return 1
                return 0
            })
        }
    }
}
```

### Search

*src/SearchCustomer.vue*

```html
<input @keyup="handleSearch" type="text">
```

```js
export default {
    methods: {
        async handleSearch(event) {
            const { data } = await axios.get('http://localhost:3000/customers?q=...')
        }
    }
}
```

### `debounce` Search

*Terminal*

```
yarn add lodash
```

*src/SearchCustomer.vue*

```js
import { debounce } from 'lodash'

export default {
    created() {
        this.handleSearch = debounce(this.handleSearch, 2000)
    }
}
```

### Columns

HTML

```html
<div class="columns">
    <div class="column">Customer 1</div>
    <div class="column">Customer 2</div>
    <div class="column">Customer 3</div>
</div>
```

### `chunk`

*src/SearchCustomer.vue*

```html
<div v-for="row in chunkCustomers" class="columns">
    <div v-for="c in row" class="column">
        ...
    </div>
</div>
```

```js
import { chunk } from 'lodash'

export default {
    data() {
        return {
            columnQty: 3
        }
    },
    computed: {
        chunkCustomers() {
            return chunk(this.customers, this.columnQty)
        }
    }
}
```

### Dummy Column

*src/SearchCustomer.vue*

```html
<div v-for="row in chunkCustomers" class="columns">
    ...
    <template v-if="row.length < columnQty">
        <div v-for="dummy in (columnQty - row.length)"
            class="column">
            <div class="box">
                <p>Dummy</p>
            </div>
        </div>
    </template>
</div>
```

### Pagination

*Postman*

```
http://localhost:3000/customers?_page=...
http://localhost:3000/customers?_limit=...
```

*Response Header*

```
x-total-count
```

*src/Pagination.vue*

```js
export default {
    data() {
        return {
            customers: [],
            limitPerPage: 8,
            totalCustomers: 0,
            currentPageNumber: 1
        }
    }
}
```

*src/Pagination.vue*

```html
<nav class="pagination">
    <ul class="pagination-list">
        <li v-for="pageNumber in totalPages">
            <a @click.prevent="fetchCustomers(pageNumber)"
                href="#" class="pagination-link">
                {{ pageNumber }}
            </a>
        </li>
    </ul>
</nav>
```

```js
export default {
    computed: {
        totalPages() {
            return Math.ceil(this.totalCustomers / this.limitPerPage)
        }
    }
}
```

*src/Pagination.vue*

```html
<a @click.prevent="fetchCustomers(pageNumber)" href="#"
    :class="classNames(pageNumber)">
    {{ pageNumber }}</a>
```

```js
export default {
    methods: {
        classNames() {
            return [
                'pagination-link',
                { 'is-current': this.currentPageNumber == pageNumber }
            ]
        }
    }
}
```
