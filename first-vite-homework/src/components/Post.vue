<template>
  <div class="post">
    <button class="delete-post" @click="$emit('delete-post')">Delete Post</button>
    <h2>{{ props.post.title }}</h2>
    <p>{{ props.post.body }}</p>
    <details @click="getPostComments">
      <summary>Comments</summary>
      <post-comments v-for="comment in comments"
                     :key="comment.id"
                     :comment="comment">
      </post-comments>
    </details>
  </div>
</template>

<script setup>
import PostComments from "./PostComments.vue";

import axios from "axios";
import {ref} from "vue";

const props = defineProps(['post'])
const comments = ref([])

function getPostComments() {
  if (comments.value.length === 0) {
    axios.get('https://jsonplaceholder.typicode.com/post/' + props.post.id + "/comments")
    .then((response) => {
      console.log(response)
      comments.value = response.data
    })
  } else {
    comments.value
  }
}
</script>

<style scoped></style>