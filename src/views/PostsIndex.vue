<template>
  <div class="posts-index">
    <div class="card-deck">
      <div class="card">
        <div
          v-for="post in posts"
          :key="post.id"
          v-bind:class="{ selected: post === currentPost }"
          v-on:click="currentPost = post"
        >
          <div class="col-3">
            <img class="card-img-top" v-bind:src="post.image" alt="Card image cap" />
            <div class="card-body">
              <h5 class="card-title">Title: {{ post.title }}</h5>
              <p class="card-text">Name: {{ post.name }}</p>
              <p class="card-text"><small class="text-muted">Last updated 3 mins ago</small></p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- <div v-for="post in posts" :key="post.id">
      <router-link v-bind:to="`/posts/${post.id}`"></router-link>
      <h2>Title: {{ post.title }}</h2>
      <p>Body: {{ post.body }}</p>
      <img v-bind:src="post.image_url" alt="post.title" />
      <button>More info!</button>
    </div> -->
  </div>
</template>

<style>
.selected {
  color: white;
  background-color: aqua;
}
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Posts!",
      posts: [],
      currentPost: {},
    };
  },
  created: function () {
    this.indexPosts();
  },
  methods: {
    indexPosts: function () {
      axios.get("http://localhost:3000/posts").then((response) => {
        this.posts = response.data;
        console.log("All posts:", this.posts);
      });
    },
  },
};
</script>
