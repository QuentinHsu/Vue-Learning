# 0.4 计算属性与侦听器

## 计算属性：Computed

> 计算属性将被混入到 Vue 实例中。所有 *getter* 和 *setter* 的 *this* 上下文自动地绑定为 *Vue* 实例。
>
> 注意如果你为一个计算属性使用了箭头函数，则 *this* 不会指向这个组件的实例，不过你仍然可以将其实例作为函数的第一个参数来访问。
>
> **计算属性的结果会被缓存**，除非依赖的响应式 *property* 变化才会重新计算。注意，如果某个依赖 (比如非响应式 *property*) 在该实例范畴之外，则计算属性是不会被更新的。
>
> -- [#computed · Vue.js](https://cn.vuejs.org/v2/api/#computed)

```vue
<template>
    <div>
        <div>{{message1}}</div>
        <div>{{message2}}</div>
        <div>{{message1and2}}</div>
        <div>{{message2and3}}</div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            message1: 'this is message1',
            message2: 'this is message2',
            message3: ''
        }
    },
    computed: {
        message1and2() {
            return '这是 message3：' + this.message1 + this.message2
        },
        /**
         * 不要在 computed 中写箭头函数，会发生报错
         */
        // message2and3: () => this.message2 + this.message3
    }
}
</script>
```

### 不要在计算属性 *computed* 中使用箭头函数

在计算属性 *computed* 中使用箭头函数作为计算函数，会发生报错，Vue 无法成功编译。虽然你在代码编辑器中没有看到语法上的报错，但你去看浏览器就会发现已编译报错。

因为箭头函数的没有 *this*，其作用域绑定在父级作用域上下文，而不会去指向 Vue

### 计算属性 *computed* 只有 *getter*

计算属性默认只有 *getter*，若需要 *setter* 则需要自行添加。

这是只有 *getter* 的版本
```vue
<template>
    <div>
        <div>{{fullName}}</div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            firstName: 'Foo',
            lastName: 'Bar'

        }
    },
    computed: {
        fullName: function() {
            return this.firstName + ' ' + this.lastName
        }
    }
}
</script>
```

当你需要 setter ，则需要这样实现：

```


