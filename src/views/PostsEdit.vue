<template>
<div class="posts-edit">
    <form v-on:submit.prevent="updatePost()">
      <h1>Edit Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="currentPostParams.title" />
      </div>
      <div>
        <label>Name:</label>
        <input type="text" v-model="currentPostParams.chef" />
      </div>
      <div>
        <label>Desscription:</label>
        <input type="text" v-model="currentPostParams.prep_time" />
      </div>
      <div>
        <label>Image Url:</label>
        <input type="text" v-model="currentPostParams.image_url" />
      </div>
      <input type="submit" value="Submit" />
      <button v-on:click="destroyPost()">Delete</button>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      currentPostParams: [],
    };
  },
  created: function () {
     axios.get(`/posts/${this.$route.params.id}`).then((response) => {
       console.log("Post info", response.data);
      this.posts = response.data;
    });
  },

 methods: {
    updatePost: function () {
      axios.patch(`/posts/${this.$route.params.id}`, this.currentPostParams).then((response) => {
        console.log(response.data);
        this.$router.push(`/posts/${response.data.id}`);
      });
    },
    destroyPost: function () {
      axios.delete(`/posts/${this.$route.params.id}`).then((response) => {
        console.log("Success", response.data);
        this.$router.push("/posts");
      });
    },
  },
};

</script>