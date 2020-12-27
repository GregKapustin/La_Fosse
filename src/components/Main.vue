<template>
  <div class="hello" @mouseenter="zoneOut()">
    <div id="scene" @mouseenter="zoneOut()">
    </div>
    <svg id="svg_main" width="1000" height="600">
      <Zone v-for="(zone, i) in zonesSorted"
        :key="'zone_' + i"
        :i="i"
        :path="zone.path"
        :density="zone.density"
        :hover_function="zoneHover"
        :out_function="zoneOut"
        :hovered="hover === i"
        :pic="zone.pic"
        :color="zone.color"
      />
    </svg>
    <div id="background" @mouseenter="zoneOut()"></div>
    <div id="zone_info" class="zone_popup" :class="{ hidden: !zoneInfo }" :style="{ marginLeft: infoLeft + 'px' }">
      <div v-if="hover >= 0">
        <ZoneData :zone="zonesSorted[hover]" />
      </div>
    </div>
    <div id="zone_chart" class="zone_popup">
      <ZoneChart :zones="zonesSorted" :hover="hover" height="650" />
    </div>
  </div>
</template>

<script>
import Zone from './Zone'
import ZoneData from './ZoneData'
import ZoneChart from './ZoneChart'
import zones from '../zones'

export default {
  name: 'Main',
  components: {
    Zone,
    ZoneData,
    ZoneChart
  },
  data: () => {
    return {
      zones,
      hover: -1,
      infoLeft: 500,
      windowWidth: window.innerWidth
    }
  },
  computed: {
    zonesSorted() {
      return zones
    },
    zoneInfo() {
      return this.hover >= 0
    }
  },
  methods: {
    zoneHover(zone) {
      this.hover = zone
      this.infoLeft = this.zones[zone].right > this.windowWidth * 2 / 10 // Bloc is 30% wide and we count from half 
        ? this.windowWidth * 2 / 10
        : this.zones[zone].right
    },
    zoneOut() {
      this.hover = -1
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#scene {
  position: absolute;
  display: block;
  width: 100%;
  height: 100%;
  background: center center no-repeat;
  background-image: url('https://upload.wikimedia.org/wikipedia/commons/thumb/0/0a/2018_-_Pol%E2%80%99and%E2%80%99Rock_Festival_-_Extrema_24.jpg/1280px-2018_-_Pol%E2%80%99and%E2%80%99Rock_Festival_-_Extrema_24.jpg');
  background-size: cover;
}
#svg_main {
  border: solid 1px silver;
  position: absolute;
  top: 50%;
  margin-top: -300px;
  left: 50%;
  margin-left: -500px;
  background-position: center center;
  background-size: cover;
  z-index: 2;
}
.zone_popup {
  display: block;
  position: absolute;
  width: 30%;
  z-index: 101;
  border: solid 1px silver;
  border-radius: 5px;
  background: white;
  padding: 10px;
  transition: 0.5s all ease;
  padding: 0;
  top: 5%;
  overflow-y: scroll;
}
.zone_popup.hidden {
  padding: 0;
  border: none;
  height: 0;
}
#zone_info {
  left: 50%;
  height: 90%;
}
#zone_info.hidden {
  height: 0
}
#zone_chart {
  width: 30%;
  left: 2%;
  padding-top: 30px;
  overflow: hidden;
}
#background {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: -1;
}
</style>
