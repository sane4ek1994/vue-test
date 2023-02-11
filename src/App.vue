<template>
<div class="app">
    <h1>Страница с постами</h1>
    <div class="app__btns">
        <my-button style='margin: 15px 0' @click="showDialog">Создать пост</my-button>
        <my-select/>
    </div>
    
    <my-dialog v-model:show="dialogVisible">
        <post-form @create="createPost"/>
    </my-dialog>

    <post-list :posts="posts" @remove="removePost" v-if="!isPostLoading" />
    <div v-else>Идет загрузка...</div>
</div >
</template>

<script>
    import axios from 'axios'
    import PostForm from './components/PostForm.vue'
    import PostList from './components/PostList.vue'
    import MyButton from './components/UI/MyButton.vue'
    import MySelect from './components/MySelect.vue'

 export default {
    components: {
        PostForm, PostList, MyButton, MySelect
    },

    data() {
        return {
           posts: [],
           dialogVisible: false,
           isPostLoading: false
        }
    },
    methods: {
        createPost(post) {
           this.posts.push(post)
           this.dialogVisible = false
        },
        removePost(post) {
            this.posts = this.posts.filter(p => p.id !== post.id)
        },
        showDialog() {
            this.dialogVisible = true
        },
        async fetchPost() {
            try {
                this.isPostLoading = true
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
                this.posts = response.data
                    
            } catch(e) {
                alert('Ошибка')
            } finally {
                this.isPostLoading = false
            }
        }
    },
    mounted() {
            this.fetchPost()
        }
 }
</script>

<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }
    .app {
        padding: 20px;
    }

    .app__btns {
        display: flex;
        justify-content: space-between;
    }
    

</style>