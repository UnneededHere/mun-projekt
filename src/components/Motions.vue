<template>
  <div class="container">
    <div class="row">
      <div class="raised col-6">
        <h1>Raised Motions</h1>
        <div class="card-column">
          <div
            class="raisedMotion card"
            v-for="motion in raisedMotions"
            :key="motion"
          >
            <div class="card-body">
              <h3 class="card-title">{{ motion.name }}</h3>
              <h4 class="card-subtitle">{{ motion.country }}</h4>
              <h4 class="card-subtitle">{{ motion.totalTime }}</h4>
              <h4 class="card-subtitle">{{ motion.speakingTime }}</h4>
            </div>
          </div>
        </div>
      </div>
      <div class="available col-6">
        <h1>Available Motions</h1>
        <div class="card-column">
          <div
            class="possibleMotion card"
            v-for="motion in possibleMotions"
            :key="motion"
          >
            <div class="card-body">
              <h3 class="card-title">{{ motion.name }}</h3>
              <p class="card-text">{{ motion.description }}</p>
              <a
                href="#"
                class="btn btn-primary"
                data-bs-toggle="modal"
                data-bs-target="#motionModal"
                @click="proposeMotion(motion.name)"
                >Add Motion</a
              >
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="modal fade" id="motionModal" tabindex="-1">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h1 class="modal-title">{{ proposedMotion }}</h1>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body">
            <form>
              <div class="form-group">
                <label for="proposedBy">Proposed by:</label>
                <select class="form-control" id="proposedBy">
                  <option
                    v-for="country in presentCountries"
                    :key="country"
                    :value="country.officialName"
                    :data-mdb-icon="country.imageSrc"
                  >
                    {{ country.officialName }}
                  </option>
                </select>
              </div>
              <div class="form-row">
                <div class="form-group col-md-6">
                  <label for="totalTime">Total Time</label>
                  <div class="input-group">
                    <input
                      type="number"
                      class="form-control"
                      id="totalTimeMinutes"
                      placeholder="Minutes"
                    />
                    <input
                      type="number"
                      class="form-control"
                      id="totalTimeSeconds"
                      placeholder="Seconds"
                    />
                  </div>
                </div>
                <div class="form-group col-md-6">
                  <label for="speakingTime">Speaking Time</label>
                  <div class="input-group">
                    <input
                      type="number"
                      class="form-control"
                      id="speakingTimeMinutes"
                      placeholder="Minutes"
                    />
                    <input
                      type="number"
                      class="form-control"
                      id="speakingTimeSeconds"
                      placeholder="Seconds"
                    />
                  </div>
                </div>
              </div>
              <div class="form-group">
                <label for="topic">Topic</label>
                <input
                  type="text"
                  class="form-control"
                  id="topic"
                  placeholder="Enter the topic"
                />
              </div>
              <button type="submit" class="btn btn-primary">Add Motion</button>
            </form>
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
      raisedMotions: [],
      proposedMotion: ""
    };
  },
  props: {
    possibleMotions: Array,
    presentCountries: Array,
  },
  computed: {
    countryOptions() {
      return this.presentCountries.map((country) => ({
        text: country.officialName,
        value: country.officialName,
      }));
    },
  },
  methods: {
    proposeMotion(motionName) {
        this.proposedMotion = motionName
    }
  }
};
</script>
  