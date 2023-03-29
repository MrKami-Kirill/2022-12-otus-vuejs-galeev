<template>
  <div class="add-post">
    <form @submit.prevent="addPost">
      <div>
        <label for="userId">UsedID: </label>
        <input type="text" id="userId" v-model="post.userId">
      </div>
      <div>
        <label for="title">Title: </label>
        <input type="text" id="title" v-model="post.title">
      </div>
      <div>
        <label for="body">Body: </label>
        <textarea id="body" rows="6" cols="22" v-model="post.body"></textarea>
      </div>
      <button>Add Post</button>
    </form>
  </div>
  <details @click="getPosts">
    <summary>Posts</summary>
    <posts :posts="posts"
           @posts="getPosts"
           @delete-post="deletePost"></posts>
  </details>
</template>

<style scoped>
</style>

<script setup>
import Posts from "./components/Posts.vue";
import {ref} from "vue";
import axios from "axios";

const posts = ref([])

function getPosts() {
  if (posts.value.length === 0) {
    axios.get('https://jsonplaceholder.typicode.com/posts')
    .then((response) => {
      console.log(response)
      posts.value = response.data
    })
  } else {
    posts.value
  }
}

function deletePost(id) {
  posts.value = posts.value.filter(p => p.id !== id)
}

const post = ref({
  userId: '',
  title: '',
  body: ''
})

function addPost() {
  axios.post("https://jsonplaceholder.typicode.com/posts", post.value)
  .then((response) => {
    console.log(response)
    const data = response.data
    posts.value.push({id: data.id, title: data.title, body: data.body, userId: data.userId})
  })
}

</script>
