<template>
  <Interface
    :permittedMotions="motionsList"
    :presentCountries="countryList"
    v-if="showMainPage"
  ></Interface>
  <InitialMenu
    :customCountries="allowCustomCountries"
    :allMotions="possibleMotions"
    v-if="!showMainPage"
    @end-setup="switchPage"
    @set-motions="setMotions"
    @set-countries="setCountries"
  ></InitialMenu>
  </template>
  <script>
  import Interface from "./Interface.vue";
  import InitialMenu from "./InitialMenu.vue";
  export default {
    components: { Interface, InitialMenu },
    data() {
      return {
        showMainPage: false,
        motionsList: [],
        countryList: [],
        votingCountries: []
      };
    },
    props: {
      possibleCountries: Array,
      possibleMotions: window.MotionList,
      allowCustomCountries: Boolean
    },
    methods: {
      switchPage() {
        this.showMainPage = !this.showMainPage;
      },
      setMotions(motions) {
        this.motionsList = motions.slice();
        console.log("set motions");
      },
      setCountries(countries) {
        this.countryList = countries.slice();
      }
    }
  };
  </script>
  