<template>
  <div class="home">
    <h1>Search a GitHub Profile</h1>
    <Search @search-profile="searchProfile" />
    <User :user="user" :data="data" />
  </div>
</template>

<script>
import Search from "../components/Search.vue";
import User from "../components/User.vue";
export default {
  name: "Home",
  data() {
    return {
      user: "",
      data: {},
    };
  },
  components: {
    Search,
    User,
  },
  methods: {
    async searchProfile(user) {
      const getProfile = await fetch(`https://api.github.com/users/${user}`);
      const getProfileJson = await getProfile.json();
      if (getProfileJson) {
        this.user = getProfileJson.login;
        this.data = getProfileJson;
        // console.log(this.user);
        // console.log(this.data);
      }
    },
  },
};
</script>
