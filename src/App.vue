<template>
  <total :possibleMotions="motionsList" :presentCountries="countryList"></total>
</template>

<script>
import total from "./components/BaseInterface.vue";

export default {
  name: "App",
  components: {
    total,
  },
  data() {
    return {
      countryList: [
        {
          officialName: "Russian Federation",
          imageSrc: "   https://cdn-icons-png.flaticon.com/512/551/551878.png ",
        },
        {
          officialName: "State of Israel",
          imageSrc: "https://cdn-icons-png.flaticon.com/512/552/552046.png",
        },
        {
          officialName: "Republic of Austria",
          imageSrc: "https://cdn-icons-png.flaticon.com/512/551/551917.png",
        },
      ],
      motionsList: [
        {
          name: "Moderated Caucus",
          description:
            "During a moderated caucus, delegates raise their placards to request speaking time and address specific topics or issues related to the agenda. The committee chairperson moderates the discussion, ensuring fairness and order while allowing delegates to share their perspectives, propose solutions, and collaborate on drafting resolutions.",
        },
        {
          name: "Unmoderated Caucus",
          description:
            "During an unmoderated caucus, delegates have the freedom to move around the room and engage in small group discussions with fellow delegates representing different countries. This format allows delegates to network, negotiate, and form alliances to work on draft resolutions or collaborate on finding common ground for complex issues.",
        },
        {
          name: "Consultation of the Whole",
          description:
            "During a Consultation of the Whole, the floor is open to all delegates, regardless of their committee membership, allowing for diverse perspectives and contributions. This format encourages a more holistic approach to problem-solving and fosters collaboration among delegates representing different countries and interests.",
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
