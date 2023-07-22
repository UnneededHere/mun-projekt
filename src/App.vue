<template>
  <test></test>
</template>

<script>
import test from "./components/Session.vue";

export default {
  name: "App",
  components: {
    test,
  },
  data() {
    return {
      countryList: [
        {
          officialName: "Russian Federation",
          imageSrc:
            "   https://cdn-icons-png.flaticon.com/512/551/551878.png ",
        },
        {
          officialName: "State of Israel",
          imageSrc:
            "https://cdn-icons-png.flaticon.com/512/552/552046.png",
        },
        {
          officialName: "Republic of Austria",
          imageSrc:
            "https://cdn-icons-png.flaticon.com/512/551/551917.png",
        },
      ],
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
