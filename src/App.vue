<template>
  <HouseComponent />
</template>

<script>
import HouseComponent from '@/components/HouseComponent.vue';

export default {
  name: 'App',
  components: {
    HouseComponent,
  },
}
</script>

<style>
@import "assets/normalize.css";
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap');

body {
  font-family: 'Roboto', sans-serif;
  line-height: 1;
}
</style>
