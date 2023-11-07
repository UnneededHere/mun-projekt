<template>
  <ul class="nav nav-pills nav-fill">
    <li class="nav-item">
      <a
        :class="isSession ? 'nav-link active' : 'nav-link'"
        aria-current="page"
        href="#"
        @click="switchTab(true)"
        >Session</a
      >
    </li>
    <li class="nav-item">
      <a
        :class="isSession ? 'nav-link' : 'nav-link active'"
        href="#"
        @click="switchTab(false)"
        >Motions</a
      >
    </li>
  </ul>
  <Session
    :presentCountries="presentCountries"
    v-if="isSession"
    :currentMotion="currentMotion"
  ></Session>
  <Motions
    :possibleMotions="possibleMotions"
    :presentCountries="presentCountries"
    v-if="!isSession"
    @new-motion="newMotion"
  ></Motions>
</template>
<script>
import Session from "./Session.vue";
import Motions from "./Motions.vue";
export default {
  components: { Session, Motions },
  data() {
    return {
      isSession: true,
      currentMotion: {
        name: "",
        proposingCountry: {
          officialName: "N/A"
        },
        totalTime: [0, 0],
        speakingTime: [0, 0],
        topic: "No Motion Defined",
      },
    };
  },
  props: {
    possibleMotions: Array,
    presentCountries: Array,
  },
  methods: {
    switchTab(tabIdenitifier) {
      this.isSession = tabIdenitifier;
    },
    newMotion(motion) {
      this.currentMotion = motion;
      this.isSession = true;
    },
  },
};
</script>
