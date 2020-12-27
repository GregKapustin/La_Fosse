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
    <div id="zone_info" class="zone_popup" :class="{hidden: !zoneInfo}">
      <div v-if="hover >= 0">
        <ZoneData :zone="zonesSorted[hover]" />
      </div>
    </div>
    <div id="zone_chart" class="zone_popup">
      <ZoneChart :zones="zonesSorted" :hover="hover" />
    </div>
  </div>
</template>

<script>
import _ from 'lodash'
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
      hover: -1
    }
  },
  computed: {
    zonesSorted() {
      return _.sortBy(zones, "layer")
    },
    zoneInfo() {
      return this.hover >= 0
    }
  },
  methods: {
    zoneHover(zone) {
      this.hover = zone
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
  width: 20%;
  z-index: 101;
  border: solid 1px silver;
  border-radius: 5px;
  background: white;
  padding: 10px;
  transition: 1s all ease;
}
.zone_popup.hidden {
  padding: 0;
  border: none;
}
#zone_info {
  left: 50%;
  margin-left: 500px;
}
#zone_chart {
  width: 30%;
  left: 30%;
  margin-left: -500px;
  height: 100%;
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
