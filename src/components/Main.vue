<template>
  <div class="hello" @mouseenter="zoneOut()">
    <div id="scene" @mouseenter="zoneOut()">
      <h1>Scene</h1>
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
  display: block;
  width: 100%;
  height: 100px;
  border-bottom: solid 2px #34495e;
  background: white;
}
#svg_main {
  position: absolute;
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
  height: 90%;
  overflow-y: scroll;
}
.zone_popup.hidden {
  padding: 0;
  border: none;
  height: 0;
}
#zone_info {
  left: 50%;
}
#zone_chart {
  width: 30%;
  left: 0;
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
