<template>
  <h3 class="text-secondary">{{ motion.topic }}</h3>
  <h5 class="text-secondary">Proposed by: {{ motion.proposingCountry.officialName }}</h5>
  <BigClock
    @next-speaker="nextSpeaker"
    :startTime="convertToSeconds(currentMotion.speakingTime)"
    :maxTime="convertToSeconds(currentMotion.totalTime)"
    :motionType="this.motion.name"
  >
  </BigClock>
  <CountryList v-if="motionHasCountries" :propList="countryList" ref="countryList"> </CountryList>
</template>

<script>
import BigClock from "./BigClock.vue";
import CountryList from "./CountryList.vue";

export default {
  name: "Session",
  props: {
    presentCountries: Array,
    currentMotion: {
      name: String,
      proposingCountry: Object,
      totalTime: [Number, Number],
      speakingTime: [Number, Number],
      topic: String,
    },
  },
  components: {
    BigClock,
    CountryList,
  },
  data() {
    return {
      countryList: this.presentCountries,
      motion: this.currentMotion,
    };
  },
  methods: {
    nextSpeaker() {
      this.$refs.countryList.removeSpeaker();
    },
    convertToSeconds(timeArray) {
      return timeArray[1] + timeArray[0] * 60;
    },
  },
  computed: {
    motionHasCountries() {
      return this.motion.name == "Moderated Caucus";
    },
  },
};
</script>
