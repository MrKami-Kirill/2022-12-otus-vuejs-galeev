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
</template>

<script setup>
import {ref} from "vue";
import axios from "axios";

const props = defineProps(['posts']);

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
    props.posts.push({id: data.id, title: data.title, body: data.body, userId: data.userId})
  })
}
</script>

<style scoped>

</style>