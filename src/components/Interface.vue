<template>
  <ul class="nav nav-pills nav-fill">
    <li class="nav-item">
      <a
        :class="isSession ? 'nav-link active' : 'nav-link'"
        aria-current="page"
        href="#"
        @click="switchPage(true)"
        >Session</a
      >
    </li>
    <li class="nav-item">
      <a
        :class="isSession ? 'nav-link' : 'nav-link active'"
        href="#"
        @click="switchPage(false)"
        >Motions</a
      >
    </li>
  </ul>
  <Session :presentCountries="presentCountries" v-if="isSession"></Session>
  <Motions :possibleMotions="possibleMotions" :presentCountries="presentCountries" v-if="!isSession"></Motions>
</template>
<script>
import Session from "./Session.vue";
import Motions from './Motions.vue';
export default {
  components: { Session, Motions },
  data() {
    return {
      isSession: true,
    };
  },
  props: {
    possibleMotions: Array,
    presentCountries: Array,
  },
  methods: {
    switchPage(pageIdenitifier) {
      this.isSession = pageIdenitifier;
    },
  },
};
</script>