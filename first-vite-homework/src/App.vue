<template>
  <details @click="getPosts">
    <summary>Post List</summary>
    <add-post :posts="posts"></add-post>
    <posts :posts="posts"
           @posts="getPosts"
           @delete-post="deletePost"></posts>
  </details>
</template>

<script setup>
import Posts from "./components/Posts.vue";
import {ref} from "vue";
import axios from "axios";
import AddPost from "./components/AddPost.vue";

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
</script>

<style scoped>
</style>
