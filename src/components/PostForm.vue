<template>
    <form @submit.prevent>
        <h4>Создание поста</h4>
        <my-input v-model="post.title"  placeholder="Название"/>
        <my-input v-model="post.body"  placeholder="Описание"/>
        <my-button style="align-self: flex-end; margin-top: 15px;" @click="createPost">Создать</my-button>
    </form>
</template>

<script>

    export default {
        data()  {
            return {
                post: {
                    title: '',
                    body: ''
                }
            }
        },
        methods: {
            createPost() {
            this.post.id = Date.now()
            this.$emit('create', this.post)
            this.title = ''
            this.body = ''
            this.post  = {
                title: '',
                body: ''
            }
        }
    }
    }
</script>

<style scoped>
    form {
        display: flex;
        flex-direction: column;
    }

</style>