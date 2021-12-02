<template>
  <div class="home">
    <a href="https://github.com/login/oauth/authorize?client_id=1a75328ffa60d689461c">Sign into GitHub</a>
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
      });
      var code = this.$route.query.code;
      if (code) {
        axios.get("/auth/github/callback?code=" + code).then((response) => {
          localStorage.setItem("github_access_token", response.data.access_token);
          this.$router.push("/about");
        });
      };
    },
    methods: {},
  };
</script>