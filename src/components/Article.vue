<template>
  <div id="article">
    <div v-for="(zone, i) in zones" :key="'article_zone_' + i">
      <ZoneData :zone="zone" />
      <ZoneChart :zones="zones" :hover="i" type="radar" height="600" />
    </div>
  </div>
</template>

<script>
import ZoneData from './ZoneData'
import ZoneChart from './ZoneChart'

export default {
  name: 'Article',
  components: {
    ZoneData,
    ZoneChart
  },
  props: {
    zones: Array
  },
  computed: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#article {
  position: absolute;
  top: 100px;
  left: 50%;
  margin-left: -400px;
  margin-top: 50px;
  width: 800px;
  background: white;
}
</style>
