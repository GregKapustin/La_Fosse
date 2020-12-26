<template>
  <div>
    <pattern v-for="(p, i) in patterns" :id="'pattern_' + p.density" :key="i" x="0" y="0" :width="grid" height="4" patternUnits="userSpaceOnUse">
      <rect v-if="!hovered" :width="grid" height="4" fill="white" />
      <rect v-for="j in p.dots" width="2" height="2" :x="j" y="0" fill="black" :key="'pattern_' + p.density + 'dot_' + j" />
    </pattern>
  </div>
</template>

<script>
import _ from 'lodash'

export default {
  name: 'Patterns',
  props: {
    zones: Array,
    grid: Number,
    hovered: Boolean
  },
  computed: {
    patterns() {
      return _.map(this.zones, zone => {

        // Let's do the dots array
        const dots = []
        let j = Math.floor(this.grid / zone.density)
        while (j <= this.grid) {
          dots.push(j)
          j += this.grid / zone.density
        }

        return {
          density: zone.density,
          dots
        }
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
