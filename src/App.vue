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
      <CustomDropdown
        placeholder="Select Account"
        v-model="selectedValue"
        :options=new_options
        :groupBy="(option) => option.group"
      />
      <button class="button button-black">Open dashboard</button>
      <button class="button button-white">Connect account</button>
      <a href="#" class="link-platform">Select another platform</a>
    </div>
  </main>
</template>

<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import CustomDropdown from '@/components/CustomDropdown.vue'
import {ref} from "vue";

const new_options = [
  { label: 'Option A', value: 'valA', group: 'Group A' },
  { label: 'Option B', value: 'valB', group: 'Group B' },
  { label: 'Option C', value: 'valC', group: 'Group A' }
]

const selectedValue = ref(''); // To hold the selected option's value

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
  max-width: 1024px;
  margin: auto;
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
  width: 50%;
  padding: 12px 0;
  font-size: 1em;
  border-radius: 10px;
  border: #222222 solid 2px;
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

</style>
