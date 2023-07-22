<template>
  <BigClock @next-speaker="nextSpeaker" :startTime="600"> </BigClock>
  <CountryList :propList="countryList"> </CountryList>
</template>

<script>
import BigClock from "./BigClock.vue";
import CountryList from "./CountryList.vue";

export default {
  name: "Session",
  components: {
    BigClock,
    CountryList,
  },
  data() {
    return {
      countryList: [
        {
          officialName: "Russian Federation",
          imageSrc: "https://cdn-icons-png.flaticon.com/512/551/551878.png ",
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
    };
  },
  methods: {
    nextSpeaker() {
        this.countryList = this.countryList.slice(1)
    }
  }
};
</script>
