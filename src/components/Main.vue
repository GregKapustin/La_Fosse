<template>
  <div class="hello">
    <div id="scene">
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
      />
      <Patterns :zones="zones" :grid="grid" />
    </svg>
    <div id="zone_info" :class="{hidden: !zoneInfo}">
      <div v-if="hover >= 0">
        <h1><span class="big">"</span><span v-html="zonesSorted[hover].name" /><span class="big">"</span></h1>
      </div>
    </div>
  </div>
</template>

<script>
import _ from 'lodash'
import Zone from './Zone'
import Patterns from './Patterns'
import zones from '../zones'

export default {
  name: 'Main',
  components: {
    Zone,
    Patterns
  },
  data: () => {
    return {
      zones,
      grid: 100,
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
  border-bottom: solid 2px black;
}
#svg_main {
  position: absolute;
  left: 50%;
  margin-left: -500px;
  background-position: center center;
  background-size: cover;
}
#zone_info {
  display: block;
  position: absolute;
  right: 100px;
  width: 20%;
  z-index: 101;
  border: solid 1px silver;
  border-radius: 5px;
  background: white;
  padding: 10px;
  text-align: right;
  transition: 1s all ease;
}
#zone_info.hidden {
  padding: 0;
  border: none;
}
#zone_info h1 {
  font-family: 'Anton';
  font-style: italic;
}
#zone_info h1 .big {
}
</style>
