<template>
  <main>
    <home></home>
  </main>
</template>

<script lang="ts">
import { ref, defineComponent } from 'vue';
import Home from './pages/MainPage.vue';

export default defineComponent({
  name: 'App',
  components: {
    Home,
  }
});
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;500;700&display=swap');

body {
  margin: 0;
  padding: 0;
}

#app {
  font-size: 16px;
  font-family: 'Montserrat', sans-serif;
}

main {
  width: 25rem;
  height: 18rem;
  border: 10px solid rgb(75, 75, 75);
}
</style>
