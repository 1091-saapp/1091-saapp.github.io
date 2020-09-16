<template>
  <div class="app">
    <div id="map" style="height: 100%"></div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: "App",
  mounted() {
    new google.maps.Map(document.getElementById("map") as HTMLElement, {
        center: {lat: 30, lng: -110},
        zoom: 8
    });
  }
})
</script>

<style lang="scss">
body{
  margin: 0;
  height: 100vh;
}
.app{
  height: 100%;
}
</style>