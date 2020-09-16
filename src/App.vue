<template>
  <div class="app">
    <div class="header">MS Intelligent Operation Command Platform</div>
    <div class="weather">
      <div class="scroll" :style="{transform: 'translateY(-'+weather.index*4+'rem)'}" :class="{transition: weather.index !== 0}">
        <div class="weather-item" v-for="item in weather.data.concat(weather.data[0])" v-if="item">
          <img class="icon" :src="'https://openweathermap.org/img/wn/'+item.icon+'@2x.png'" alt="icon">
          <span class="temp">{{item.temp}}℃</span>
          <span class="name">{{item.name}}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import MarkerClusterer, {MarkerClustererOptions} from '@google/markerclustererplus'
import outageCluster from './assets/outageCluster.png'
import styles from "./styles";

export default Vue.extend({
  name: "App",
  data() {
    return {
      weather: {
        data: [{
          icon: "02d",
          name: "Nairobi A",
          temp: 14
        }, {
          icon: "02d",
          name: "Nairobi B",
          temp: 14
        }, {
          icon: "02d",
          name: "Nairobi C",
          temp: 14
        }],
        index: 0
      },
      locations: [
        {lat: -31.563910, lng: 147.154312},
        {lat: -33.718234, lng: 150.363181},
        {lat: -33.727111, lng: 150.371124},
        {lat: -33.848588, lng: 151.209834},
        {lat: -33.851702, lng: 151.216968},
        {lat: -34.671264, lng: 150.863657},
        {lat: -35.304724, lng: 148.662905},
        {lat: -36.817685, lng: 175.699196},
        {lat: -36.828611, lng: 175.790222},
        {lat: -37.750000, lng: 145.116667},
        {lat: -37.759859, lng: 145.128708},
        {lat: -37.765015, lng: 145.133858},
        {lat: -37.770104, lng: 145.143299},
        {lat: -37.773700, lng: 145.145187},
        {lat: -37.774785, lng: 145.137978},
        {lat: -37.819616, lng: 144.968119},
        {lat: -38.330766, lng: 144.695692},
        {lat: -39.927193, lng: 175.053218},
        {lat: -41.330162, lng: 174.865694},
        {lat: -42.734358, lng: 147.439506},
        {lat: -42.734358, lng: 147.501315},
        {lat: -42.735258, lng: 147.438000},
        {lat: -43.999792, lng: 170.463352}
      ]
    }
  },
  created() {
    console.log("created")
    const map = new google.maps.Map(document.getElementById("map") as HTMLElement, {
      center: {lat: -1.280682, lng: 36.7685158},
      zoom: 11,
      minZoom: 3,
      maxZoom: 22,
      mapTypeControl: false,
      gestureHandling: 'greedy',
      fullscreenControl: false,
      zoomControl: false,
      streetViewControl: false,
      styles: styles as MapTypeStyle[]
    });
    map.setCenter({lat: -28.024, lng: 140.887})
    map.setZoom(3)
    const markers = this.locations.map(function(location) {
      return new google.maps.Marker({
        position: location,
        label: "A"
      });
    })
    console.log(outageCluster)
    const options: MarkerClustererOptions = {
      styles: [{
        url: outageCluster,
        height: 50,
        width: 28,
        anchorText: [22, 2],
        textColor: '#000000',
        textSize: 10,
        fontWeight: 'bold'
      }],
      title: "Test"
    }
    new MarkerClusterer(map, markers, options)
    this.intervalId = setInterval(() => {
      if (this.weather.index === this.weather.data.length){
        this.weather.index = 0
      }else {
        this.weather.index++
      }
    }, 5000)
  },
  beforeDestroy() {
    console.log("destroyed")
    clearInterval(this.intervalId)
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
  height: 4rem;
  width: 40rem;
  top: 0;
  line-height: 4rem;
  font-size: 1.6rem;
  word-spacing: 1rem;
  color: white;
  overflow: hidden;
  margin: 1rem 2rem;
  .icon{
    height: 4rem;
    vertical-align: top;
  }
}
.transition{
  transition: transform 2s linear;
}
</style>