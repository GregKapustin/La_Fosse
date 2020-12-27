<template>
  <div>
    <div v-for="(comp, i) in patterns" :key="'pattern_parent_' + i">
      <component :is="comp" />
    </div>
  </div>
</template>

<script>
import _ from 'lodash'
import patterns from './patterns/index.js'

export default {
  name: 'Patterns',
  components: patterns,
  data: () => {
    return {
      grid: 100,
      patterns
    }
  },
  props: {
    zones: Array,
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
