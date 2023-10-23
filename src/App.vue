<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <TheWelcome />
    <div v-if="apiData">
      <h2>{{ apiData }}</h2>
      <p>{{ apiData }}</p>
    </div>
    <div v-else>
      <p>Loading...</p>
    </div>
  </main>
</template>

<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
import axios from 'axios';

let apiData = null;

const fetchData = async () => {
  try {
    const response = await axios.get('https://pokeapi.co/api/v2/pokemon?limit=151%27'); // แทนที่ด้วย URL ของ API ที่คุณต้องการใช้
    apiData = response.data;
    console.log(apiData);
  } catch (error) {
    console.error(error);
  }
};

import { onMounted } from 'vue';

onMounted(() => {
  fetchData();
});
</script>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
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
