<template>
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

function addPost(data) {
  console.log(data)
  posts.value.push({id: data.id, title: data.title, body: data.body, userId: data.userId})
}

</script>
