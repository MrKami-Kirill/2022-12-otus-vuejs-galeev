<template>
  <section class="posts">
    <details @click="getPosts">
      <summary>Posts</summary>
      <post v-for="post in posts"
            :key="post.id"
            :post="post"
            @delete-post="deletePost(post.id)">
      </post>
    </details>
  </section>
</template>

<script setup>
import Post from "./Post.vue";
import axios from "axios";
import {ref} from "vue";

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
  axios.delete('https://jsonplaceholder.typicode.com/posts/' + id)
  .then((response) => {
    console.log(response)
    posts.value = posts.value.filter(p => p.id !== id)
  })
}
</script>

<style scoped></style>