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
            <div class="card-header">
              <h3 class="card-title">{{ motion.name }}</h3>
              <h5 class="card-subtitle text-body-secondary">
                {{ motion.topic }}
              </h5>
            </div>
            <div class="card-body">
              <h5 class="card-subtitle">
                {{ motion.proposingCountry.officialName }}
              </h5>
              <h5 class="card-subtitle">
                {{ motion.totalTime[0] }}:{{
                  String(motion.totalTime[1]).padStart(2, "0")
                }}
              </h5>
              <h5
                class="card-subtitle"
                v-if="motion.name == 'Moderated Caucus'"
              >
                {{ motion.speakingTime[0] }}:{{
                  String(motion.speakingTime[1]).padStart(2, "0")
                }}
              </h5>
            </div>
            <div class="card-footer">
              <div class="btn-group">
                <a
                  href="#"
                  class="btn btn-success"
                  @click="acceptMotion(motion)"
                  >Accept</a
                >
                <a href="#" class="btn btn-danger" @click="rejectMotion(motion)"
                  >Reject</a
                >
              </div>
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
            <h1 class="modal-title">{{ proposedMotion.name }}</h1>
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
                <label for="proposedBy">Proposed by:</label>
                <select
                  class="form-control"
                  id="proposedBy"
                  v-model="proposedMotion.proposingCountry"
                >
                  <option
                    v-for="country in presentCountries"
                    :key="country"
                    :value="country"
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
                      v-model="proposedMotion.totalTime[0]"
                    />
                    <input
                      type="number"
                      class="form-control"
                      id="totalTimeSeconds"
                      placeholder="Seconds"
                      v-model="proposedMotion.totalTime[1]"
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
                      v-model="proposedMotion.speakingTime[0]"
                      :disabled="noSpeakingTime(proposedMotion)"
                    />
                    <input
                      type="number"
                      class="form-control"
                      id="speakingTimeSeconds"
                      placeholder="Seconds"
                      v-model="proposedMotion.speakingTime[1]"
                      :disabled="noSpeakingTime(proposedMotion)"
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
                  v-model="proposedMotion.topic"
                />
              </div>
              <button
                class="btn btn-primary"
                data-bs-dismiss="modal"
                @click="submitMotion"
              >
                Add Motion
              </button>
            </div>
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
      proposedMotion: {
        name: "",
        proposingCountry: null,
        totalTime: [0, 0],
        speakingTime: [0, 0],
        topic: "",
      },
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
    motionNames() {
      return this.possibleMotions.map((x)=>(x[0]));
    }
  },
  methods: {
    proposeMotion(motionName) {
      this.proposedMotion.name = motionName;
    },
    submitMotion() {
      this.raisedMotions.push(this.proposedMotion);
      this.proposedMotion = {
        name: "",
        proposingCountry: "",
        totalTime: [0, 0],
        speakingTime: [0, 0],
        topic: "",
      };
    },
    rejectMotion(motion) {
      this.raisedMotions = this.raisedMotions.splice(
        this.raisedMotions.indexOf(motion),
        -1
      );
    },
    noSpeakingTime(motion) {
      return motion.name != 'Moderated Caucus'
    },
    acceptMotion(motion) {
      if (this.noSpeakingTime(motion)) {
        motion.speakingTime = motion.totalTime
      }
      this.$emit("new-motion", motion);
    },
  },
};
</script>
  