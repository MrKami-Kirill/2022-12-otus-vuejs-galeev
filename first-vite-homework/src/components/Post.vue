<template>
  <div class="view">
    <button @click="deletePost">Delete post</button>
    <h2>{{ props.post.title }}</h2>
    <p>{{ props.post.body }}</p>
    <details>
      <summary>Comments</summary>
      <post-comments v-for="comment in comments"
                     :key="comment.id"
                     :comment="comment"></post-comments>
    </details>
  </div>
</template>

<script setup>
import axios from "axios";
import PostComments from "./PostComments.vue";
import {onMounted, ref} from "vue";

const props = defineProps(['post'])
const comments = ref([])

onMounted(async () => {
  await axios.get('https://jsonplaceholder.typicode.com/post/' + props.post.id + "/comments")
  .then((response) => {
    console.log(response)
    comments.value = response.data
  })
})

function deletePost() {
  axios.delete('https://jsonplaceholder.typicode.com/posts/' + props.post.id)
  .then((response) => console.log(response))
}

</script>

<style scoped></style>