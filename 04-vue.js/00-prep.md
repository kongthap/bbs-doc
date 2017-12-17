## Chapter 00

### Component Based Application

![](https://u.cubeupload.com/jeud/1FBqKwp2v4wvhFEGYtUG.jpg)

```html
<app>
    <friend-list>
        <friend-list-item>
            <friend-info />
        </friend-list-item>
    </friend-list>
</app>
```

### Single Component

- JavaScript (Logic)
- Text, Media, Image, etc (Content)
- Style Sheet

### Vue.js Single File Component

```html
<script>
export default {
    ...
}
</script>

<style>
p {
    color:red;
}
</style>

<template>
    <div>
        <p>Hello World</p>
    </div>
</template>
```

### Component's Plain JavaScript Object

```js
{
    data() {
        return {

        }
    },
    computed: {
        greet() {

        }
    },
    methods: {
        hello() {

        },

        world() {

        }
    }
}
```

### Vue

![](https://u.cubeupload.com/jeud/68747470733a2f2f692e.png)

### `webpack`

![](https://u.cubeupload.com/jeud/1Qo4yWofQHQKSOtLtTD5.png)
