<template>
    <div>
        <div>{{message1}}</div>
        <div>{{message2}}</div>
        <div>{{message1and2}}</div>
        <!-- <div>{{message2and3}}</div> -->
        <div>{{fullName}}</div>
        <div>{{firstName}}</div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            message1: 'this is message1',
            message2: 'this is message2',
            message3: '',
            firstName: 'Foo',
            lastName: 'Bar'

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
        // fullName: function() {
        //     return this.firstName + ' ' + this.lastName
        // }
        fullName: {
            get: function() {
                return this.firstName + ' ' + this.lastName
            },
            set: function(newValue) {
                let nameArry = newValue.split(' ')
                this.firstName = nameArry[0]
                this.lastName = nameArry[nameArry.length - 1]
            }
        }
    }
}
</script>

<style>

</style>