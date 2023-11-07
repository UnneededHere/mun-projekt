<template>
  <Interface
    :possibleMotions="motionsList"
    :presentCountries="countryList"
    v-if="showMainPage"
  ></Interface>
  <InitialMenu
    :customCountries="allowCustomCountries"
    :allMotions="allPossibleMotions"
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
        allPossibleMotions: [
          "Moderated Caucus",
          "Unmoderated Caucus",
          "Consultation of the Whole",
          // Unlike lists of nations, we must make this list comprehensive since users cannot define the actual logic behind motions
        ],
        motionsList: [],
        countryList: [],
        votingCountries: []
      };
    },
    props: {
      possibleCountries: Array,
      allowCustomCountries: Boolean
    },
    methods: {
      switchPage() {
        this.showMainPage = !this.showMainPage;
      },
      setMotions(motions) {
        this.motionsList = motions.slice();
      },
      setCountries(countries) {
        this.countryList = countries.slice();
      }
    },
  };
  </script>
  