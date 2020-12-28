<template>
  <div id="article">
    <div v-for="(zone, i) in zones" :key="'article_zone_' + i">
      <ZoneDataHeader :zone="zone" />
      <div class="columns">
        <div class="column is-one-third ">
          <svg width="1000" height="600" class="article_svg">
            <Zone v-for="(zone_svg, j) in zones"
              :key="'zone_' + j"
              :i="j"
              :path="zone_svg.path"
              :density="zone_svg.density"
              :hover_function="zoneHover"
              :out_function="zoneOut"
              :hovered="i === j"
              :pic="zone_svg.pic"
              :color="zone_svg.color"
            />
          </svg>
          <ZoneChart :zones="zones" :hover="i" type="radar" height="400" class="zoneChart" />
        </div>
        <div class="column">
          <ZoneData :zone="zone" :lang="lang" />
        </div>
      </div>
      <ZoneDataFooter :zone="zone" :lang="lang"/>
    </div>
  </div>
</template>

<script>
import Zone from './Zone'
import ZoneDataHeader from './ZoneDataHeader'
import ZoneData from './ZoneData'
import ZoneDataFooter from './ZoneDataFooter'
import ZoneChart from './ZoneChart'

export default {
  name: 'Article',
  components: {
    Zone,
    ZoneDataHeader,
    ZoneData,
    ZoneDataFooter,
    ZoneChart
  },
  props: {
    zones: Array,
    lang: String
  },
  methods: {
    zoneHover() {
      return null
    },
    zoneOut() {
      return null
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#article {
  position: absolute;
  top: 100px;
  left: 20%;
  margin-top: 50px;
  width: 60%;
}
#article > * {
  background: white;
  margin-bottom: 100px;
  border-radius: 30px;
  overflow: hidden;
}
h1 {
  font-family: 'Anton';
  font-style: italic;
  color: #34495e;
  font-size: 50px;
  line-height: 50px;
  margin-top: 30px;
  margin-bottom: 50px;
  padding: 30px;
  border-top: solid 2px silver;
  border-bottom: solid 2px silver;
}
.image {
  width: 100%;
  height: 200px;
  background-position: center center;
  background-size: cover;
}
.caption {
  font-family: 'Roboto';
  font-style: italic;
  color:slategray;
  font-size: 90%;
  line-height: 90%;
  padding-top: 10px;
}
.article_svg {
  transform: scale(0.3);
  margin-left: -300px;
  margin-top: -150px;
  border: solid 1px silver;
}
.zoneChart {
  margin-top: -200px;

}
</style>
