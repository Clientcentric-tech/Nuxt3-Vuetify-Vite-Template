<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <div class="account-selector">
      <h2 class="account-title">Select account</h2>
      <p class="hint-title">Use the dropdown to select where you want to login.</p>
      <Dropdown
        :options="options"
        @selected="validateSelection"
        @filter="getDropdownValues"
        :disabled="false"
        placeholder="Select account"
      />
      <button class="button button-black">Open dashboard</button>
      <button class="button button-white">Connect account</button>
      <a href="#" class="link-platform">Select another platform</a>
    </div>
  </main>
</template>

<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue';
import Dropdown from "@/components/SearchableDropdown.vue";
import { ref } from 'vue';

// Define options as a reactive reference
const options = ref([
  { name: 'jack', id: '1' },
  { name: 'kevin', id: '2' },
  { name: 'austin', id: '3' },
  { name: 'jemma', id: '4' }, // Corrected typo here
  { name: 'tomas', id: '5' },
  { name: 'ewan', id: '6' },
  { name: 'anna', id: '7' }
]);

// Define selected as a reactive reference
const selected = ref({ name: null, id: null });

// Method to validate selection
const validateSelection = (selection) => {
  selected.value = selection;
  console.log(selection.name + ' has been selected');
};

// Method to filter dropdown values
const getDropdownValues = (keyword) => {
  console.log('You could refresh options by querying the API with ' + keyword);
};
</script>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

.account-selector {
  align-content: center;
  justify-content: center;
}

.account-title {
  margin: auto;
  width: fit-content;
  padding: 10px;
  font-weight: bold;
}

.button {
  display: block;
  margin: 10px auto;
  width: 75%;
  padding: 12px 0;
  font-size: 1em;
  border-radius: 10px;
  border-color: #222222;
  cursor: pointer;
}

.button:hover {
  opacity: 80%;
}

.button-black {
  color: white;
  background-color: #222222;
}

.button-white {
  color: #222222;
  background-color: white;
}

.link-platform {
  display: block;
  margin: auto;
  /*width: 75%;*/
  width: fit-content;
  color: dodgerblue;
}

.hint-title {
  font-size: 1.2em;
  width: fit-content;
  margin: 20px auto;
  color: #555555;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}

/* Optional: Add styles to ensure dropdown visibility */
.SearchableDropdown {
  margin-top: 20px; /* Ensure there's space for the dropdown */
}
</style>
