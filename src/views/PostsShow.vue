<template>
  <div class="showpost">
    <div class="container">
      <h2>{{ post.title }}</h2>
      <p>{{ post.body }}</p>
      <img v-bind:src="post.image" alt="post.title" />
      <router-link to="/posts">Back to all posts</router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      errors: [],
      post: {},
    };
  },
  created: function () {
    axios.get("/posts/" + this.$route.params.id).then((response) => {
      this.posts = response.data;
    });
  },
};
</script>
