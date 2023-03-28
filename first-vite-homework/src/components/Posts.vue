<template>
  <section class="main">
    <ul class="post-list">
      <post v-for="post in posts"
            :key="post.id"
            :post="post"></post>
    </ul>
  </section>
</template>

<script setup>
import axios from "axios";
import Post from "./Post.vue";
import {onMounted, ref} from "vue";

const posts = ref([])

onMounted(async () => {
  await axios.get('https://jsonplaceholder.typicode.com/posts')
  .then((response) => {
    console.log(response)
    posts.value = response.data
  })
})
</script>

<style scoped></style>