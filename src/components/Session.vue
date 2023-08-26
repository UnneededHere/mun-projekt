<template>
  <BigClock @next-speaker="nextSpeaker" :startTime="600"> </BigClock>
  <CountryList :propList="countryList"> </CountryList>
</template>

<script>
import BigClock from "./BigClock.vue";
import CountryList from "./CountryList.vue";

export default {
  name: "Session",
  props: {
    presentCountries: Array
  },
  components: {
    BigClock,
    CountryList,
  },
  data() {
    return {
      countryList: this.presentCountries
    };
  },
  methods: {
    nextSpeaker() {
        this.countryList = this.countryList.slice(1)
    }
  }
};
</script>
