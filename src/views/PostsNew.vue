<template>
  <div class="posts-new">
     <img v-if="status" :src="`https://http.cat/${status}`" />
    <form v-on:submit.prevent="createPost()">
      <h1>Create Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <p>
          Title
          <input type="text" v-model="newPostparams.title" />
        </p>
        <p>
          Body
          <input type="text" v-model="newPostparams.body" />
        </p>
      </div>

      <div v-for="post in posts" :key="post.id">
        <h2>Title: {{ post.title }}</h2>
        <p>Body: {{ post.body }}</p>
        <img v-bind:src="post.image" alt="post.title" />
        <button>More info!</button>
      </div>
      <input type="submit" value="submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Posts!",
      posts: [],
      newPostParams: {},
      errors: [],
      status: "",
    };
  },
  methods: {
    createPosts: function () {
      console.log("Creating post!");
      axios
        .post("/posts", this.newPostParams)
        .then((response) => {
          this.$router.push("/posts");
          console.log(response.data);
        })
        .catch((error) => {
          this.status = error.response.status;
        });
    },
  },
};
</script>
