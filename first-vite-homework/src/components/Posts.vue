<template>
  <div class="posts">
      <post v-for="post in props.posts"
            :key="post.id"
            :post="post"
            @delete-post="$emit('delete-post', deletePost(post.id))">
      </post>
  </div>
</template>

<script setup>
import Post from "./Post.vue";
import axios from "axios";

const props = defineProps(['posts'])

const emit = defineEmits(['delete-post']);

function deletePost(id) {
  axios.delete('https://jsonplaceholder.typicode.com/posts/' + id)
  .then((response) => {
    console.log(response)
  })
  emit('delete-post', id)
  return id
}
</script>

<style scoped></style>