<template>
  <details>
    <summary>Add Post Form</summary>
    <section class="add-post">
      <form @submit.prevent="addPost">
        <div>
          <label for="userId">UsedID:</label>
          <input type="text" id="userId" v-model="postData.userId">
        </div>
        <div>
          <label for="title">Title:</label>
          <input type="text" id="title" v-model="postData.title">
        </div>
        <div>
          <label for="body">Body:</label>
          <textarea id="body" rows="6" cols="22" v-model="postData.body"></textarea>
        </div>
        <button>Add Post</button>
      </form>
    </section>
  </details>
</template>

<script setup>
import axios from "axios";
import {ref} from "vue";

const postData = ref([{
  userId: '',
  title: '',
  body: ''
}])

function addPost() {
  axios.post("https://jsonplaceholder.typicode.com/posts", postData.value)
  .then((response) => console.log(response))
}
</script>

<style scoped>

</style>