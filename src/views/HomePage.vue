<template>
  <div class="homepage">
    <Weather />
  </div>
</template>

<script>
import Weather from '../components/Weather.vue';

  export default {
    name: 'HomePage',
    components: {
      Weather,
    }
  };
</script>

<style>
.homepage {
  text-align: center;
}
</style>
