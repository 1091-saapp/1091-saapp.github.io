<template>
  <div class="app">
    <div class="header">MS Intelligent Operation Command Platform</div>
    <div class="weather">
      <div class="scroll">
        <div class="cur">
          <img class="icon" :src="'https://openweathermap.org/img/wn/'+weather.cur.icon+'@2x.png'" alt="icon">
          <span class="temp">{{weather.cur.temp}}℃</span>
          <span class="name">{{weather.cur.name}}</span>
        </div>
        <div class="next">
          <img class="icon" :src="'https://openweathermap.org/img/wn/'+weather.next.icon+'@2x.png'" alt="icon">
          <span class="temp">{{weather.next.temp}}℃</span>
          <span class="name">{{weather.next.name}}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import mapStyle from "./mapStyle";

let map: google.maps.Map
export default Vue.extend({
  name: "App",
  data() {
    return {
      map: null,
      weather: {
        data: [{
          icon: "02d",
          name: "Nairobi",
          temp: 14
        }, {
          icon: "02d",
          name: "Nairobi",
          temp: 14
        }, {
          icon: "02d",
          name: "Nairobi",
          temp: 14
        }],
        index: 0,
        cur: {
          icon: "02d",
          name: "Nairobi West",
          temp: 14
        },
        next: {
          icon: "02d",
          name: "Nairobi",
          temp: 14
        }
      }
    }
  },
  created() {
    map = new google.maps.Map(document.getElementById("map") as HTMLElement, {
      center: {lat: -1.280682, lng: 36.7685158},
      zoom: 11,
      minZoom: 3,
      maxZoom: 22,
      styles: mapStyle,
      mapTypeControl: false,
      gestureHandling: 'greedy',
      fullscreenControl: false,
      zoomControl: false,
      streetViewControl: false
    });
  }
})
</script>

<style lang="scss" scoped>
.app {
  height: 100%;
}

.header {
  height: 6rem;
  background-image: url("/assets/headline.png");
  background-size: contain;
  background-repeat: no-repeat;
  opacity: 0.9;
  font-size: 3rem;
  line-height: 6rem;
  color: #54EAB3;
  text-align: center;
}

.weather {
  box-sizing: border-box;
  position: absolute;
  height: 6rem;
  width: 40rem;
  top: 0;
  padding: 1rem 2rem;
  line-height: 4rem;
  font-size: 1.6rem;
  word-spacing: 1rem;
  color: white;
  overflow: hidden;
  .icon{
    height: 4rem;
    vertical-align: top;
  }
}
</style>