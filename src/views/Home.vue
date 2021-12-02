<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="post in posts.articles">
      <p><b>Headline: {{ post.description }}</b></p>
      <p>Body: {{ post.content }}</p>
      <hr>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from 'axios'
  export default {
    data: function () {
      return {
        message: "Today's Headlines",
        posts: [],
      };
    },
    created: function () {
      // axios.get("https://jsonplaceholder.typicode.com/posts").then(response => {
      //   console.log(response.data);
      //   this.posts = response.data
      // });
      axios.get("/news_headlines").then(response => {
        console.log(response.data);
        this.posts = response.data
      })
    },
    methods: {},
  };
</script>