<template>
  <h2>Current Speaker</h2>
  <div class="currentSpeaker">
    <img :src="currentSpeaker.imageSrc" height="44" class="countryFlag" />
    <h1 class="countryName">{{ currentSpeaker.officialName }}</h1>
  </div>
  <div id="upcomingSpeakers">
    <h2>Upcoming Speakers</h2>
    <div id="countryList">
      <div
        v-for="country in upcomingSpeakers"
        :key="country"
        class="countryInList"
      >
        <img height="46" :src="country.imageSrc" class="countryFlag" />
        <h3 class="countryName">{{ country.officialName }}</h3>
      </div>
    </div>
  </div>
  <button data-bs-toggle="modal" data-bs-target="#countryModal">
    Add Speaker
  </button>
  <div class="modal fade" id="countryModal" tabindex="-1">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h1 class="modal-title">Add Country to Speaking List</h1>
          <button
            type="button"
            class="btn-close"
            data-bs-dismiss="modal"
            aria-label="Close"
          ></button>
        </div>
        <div class="modal-body">
          <div>
            <div class="form-group">
              <label for="newSpeaker">Country:</label>
              <select class="form-control" id="newSpeaker" v-model="newSpeaker">
                <option
                  v-for="country in propList"
                  :key="country"
                  :value="country"
                  :data-mdb-icon="country.imageSrc"
                >
                  {{ country.officialName }}
                </option>
              </select>
            </div>
            <button
              class="btn btn-primary"
              data-bs-dismiss="modal"
              @click="addSpeaker"
            >
              Add Speaker
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      speakingCountries: [],
      newSpeaker: {
        officialName: "",
        imageSrc: "",
      },
    };
  },
  props: {
    propList: Array,
  },
  computed: {
    currentSpeaker() {
      if (this.speakingCountries.length) {
        return this.speakingCountries[0];
      }
      return {
        officialName: "No Speaker",
        imageSrc: "https://cdn-icons-png.flaticon.com/512/300/300129.png",
      };
    },
    upcomingSpeakers() {
      if (this.speakingCountries.length > 1) {
        return this.speakingCountries.slice(1);
      }
      return [];
    },
  },
  methods: {
    addSpeaker() {
      this.speakingCountries.push(this.newSpeaker);
    },
  },
};
</script>
<style>
.countryName {
  display: inline-block;
  margin: 0;
  padding: 10px;
  vertical-align: middle;
}
.countryFlag {
  vertical-align: middle;
}
.countryInList {
  vertical-align: middle;
  text-align: left;
}
#countryList {
  display: inline-block;
}
#upcomingSpeakers {
  margin-bottom: 20px;
}
</style>