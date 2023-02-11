<template>
    <input class="input" @input="updateInput" type="text">
</template>

<script>
    export default {
        name: 'my-input',
        props: {
            modalValue: [String, Number]
        },
        methods: {
            updateInput(event) {
                this.$emit('update:modelValue', event.target.value)
            }
        }
    }
</script>

<style scoped>
     .input {
        margin-top: 10px;
        width: 100%;
        border: 1px solid teal;
        padding: 10px 15px;
    }
</style>