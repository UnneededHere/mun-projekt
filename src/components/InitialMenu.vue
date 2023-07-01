<template>
  <div class="menu">
    <h1>Initialisation</h1>

    <!-- Dropdown for selecting templates -->
    <div class="dropdown">
      <label for="template-dropdown">Select Template:</label>
      <select
        id="template-dropdown"
        v-model="selectedTemplate"
        @change="selectTemplate"
      >
        <option value="">Select Template</option>
        <option
          v-for="template in templates"
          :value="template.value"
          :key="template.value"
        >
          {{ template.label }}
        </option>
      </select>
    </div>

    <!-- Button for showing scrollable list popup -->
    <div class="popup-menu">
      <button class="popup-btn" @click="showScrollableList">
        This Session's Nations
      </button>
      <div class="popup-content" v-if="isScrollableListOpen" @click.stop="">
        <h2>Available Nations</h2>
        <ul>
          <li v-for="item in scrollableList" :key="item">{{ item }}</li>
        </ul>
        <div>
          <input type="text" v-model="newItem" placeholder="Enter item text" />
          <button @click="addItemToList">Add Item</button>
        </div>
      </div>
    </div>

    <!-- Button for showing checkbox menu popup -->
    <div class="popup-menu">
      <button class="popup-btn" @click="showCheckboxMenu">
        This Session's Motions
      </button>
      <div class="popup-content" v-if="isCheckboxMenuOpen" @click.stop="">
        <h2>Available Motions</h2>
        <ul>
          <li v-for="element in checkboxMenu" :key="element">
            <label>
              <input
                type="checkbox"
                v-model="selectedElements"
                :value="element"
              />
              {{ element }}
            </label>
          </li>
        </ul>
      </div>
    </div>

    <!-- Submit button -->
    <button class="submit-btn" @click="submitForm">Submit</button>
  </div>
</template>
  
  <script>
export default {
  data() {
    return {
      selectedTemplate: "",
      templates: [
        { label: "United Nations General Assembly, 2023", value: "genAss2023" },
        { label: "NATO 2023", value: "nato2023" },
        { label: "League of Nations, 1931", value: "leagueNat1931" },
      ],
      isScrollableListOpen: false,
      scrollableList: [],
      isCheckboxMenuOpen: false,
      checkboxMenu: ["Moderated Caucus", "Unmoderated Caucus", "Consultation of the Whole"],
      selectedElements: [],
      newItem: ''
    };
  },
  mounted() {
    document.addEventListener("click", this.closeMenus);
  },
  unmounted() {
    document.removeEventListener("click", this.closeMenus);
  },
  methods: {
    selectTemplate() {
      // Logic to set values based on the selected template
      switch (this.selectedTemplate) {
        case "genAss2023":
          // Set values appropriately
          break;
        case "nato2023":
          // Set values appropriately
          break;
        case "leagueNat1931":
        //Set values appropriately
      }
    },
    showScrollableList() {
      this.isScrollableListOpen = true;
    },
    addItemToList() {
      this.scrollableList.push(this.newItem);
    },
    showCheckboxMenu() {
      this.isCheckboxMenuOpen = true;
    },
    closeMenus(event) {
      if (!this.$el.contains(event.target)) {
        this.isScrollableListOpen = false;
        this.isCheckboxMenuOpen = false;
      }
    },
    submitForm() {
      // Logic for submitting the form
    },
  },
};
</script>
  
  <style scoped>
/* Styles for the menu component... */

.dropdown {
  margin-top: 20px;
}

.popup-menu {
  margin-top: 20px;
}

.popup-btn {
  padding: 10px;
  border: none;
  background-color: #f1f1f1;
  cursor: pointer;
}

.popup-content {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 9999;
  min-width: 200px;
  padding: 10px;
  background-color: #f9f9f9;
  box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
}

.popup-content h2 {
  margin-top: 0;
}

.popup-content ul {
  max-height: 200px;
  overflow-y: auto;
  list-style-type: none;
  margin: 0;
  padding: 0;
}

.popup-content li {
  margin-bottom: 5px;
}

.submit-btn {
  margin-top: 20px;
  padding: 10px 20px;
  background-color: #4caf50;
  border: none;
  color: #fff;
  cursor: pointer;
}
</style>
  