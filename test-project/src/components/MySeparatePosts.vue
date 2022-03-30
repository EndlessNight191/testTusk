<template>
  <div class="postBlock">
    <h2 class="postTextHead">{{post.title}}</h2>
    <div class="postText">{{post.body}}</div>
  </div>
</template>

<script>
export default {
  name: "MySeparatePosts",
  props:{
    post: Object
  },
}
</script>

<style scoped>

</style>