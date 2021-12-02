<template>
  <div class="about">
    <p>{{ profile.name }}</p>
    <p>{{profile.location}}</p>
    <p>{{profile.url}}</p>
    <img v-bind:src="profile.avatar_url" alt="">
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data: function () {
      return {
        profile: {},
      };
  },
  created: function () {
    var githubAccessToken = localStorage.getItem("github_access_token");
    if (githubAccessToken) {
      axios
        .get("/github_profile?github_access_token=" + githubAccessToken)
        .then((response) => {
          this.profile = response.data;
        });
    }
  },
};

</script>
