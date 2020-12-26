<template>
  <div class="hello">
    <div id="scene">
    </div>
    <svg id="svg_main" width="1000" height="800">
      <Zone v-for="(zone, i) in zonesSorted"
        :key="'zone_' + i"
        :i="i"
        :name="zone.name"
        :path="zone.path"
        :density="zone.density"
        :hover_function="zoneHover"
        :out_function="zoneOut"
        :hovered="hover === i"
      />
      <pattern v-for="(p, i) in patterns" :id="'pattern_' + p.density" :key="i" x="0" y="0" :width="grid" height="4" patternUnits="userSpaceOnUse">
        <rect :width="grid" height="4" fill="white" />
        <rect v-for="j in p.dots" width="2" height="2" :x="j" y="0" fill="black" :key="'pattern_' + p.density + 'dot_' + j" />
      </pattern>
    </svg>
    <div id="zone_info">
      <div v-if="hover >= 0">
        {{ zonesSorted[hover].name }}
      </div>
    </div>
  </div>
</template>

<script>
import _ from 'lodash'
import Zone from './Zone'
import zones from '../zones'

export default {
  name: 'Main',
  components: {
    Zone
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
    patterns() {
      const densities = _.uniq(_.map(zones, "density"))
      return _.map(densities, density => {

        // Let's do the dots array
        const dots = []
        let i = Math.floor(this.grid / density)
        while (i <= this.grid) {
          dots.push(i)
          i += this.grid / density
        }

        return {
          density,
          dots
        }
      })
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

}
</style>
