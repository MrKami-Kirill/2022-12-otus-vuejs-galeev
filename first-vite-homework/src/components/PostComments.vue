<template>
  <div class="post-comments">
    <h3>{{ props.comment.name }}</h3>
    <h4>{{ props.comment.email }}</h4>
    <p>{{ props.comment.body }}</p>
  </div>
</template>

<script setup>
const props = defineProps(['comment'])
</script>

<style scoped>
</style>