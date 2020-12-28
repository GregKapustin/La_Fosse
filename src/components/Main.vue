<template>
  <div class="hello" @mouseenter="zoneOut()">
    <vue-headful
      title="La Fosse"
      description="Géographie d'une fosse de concert"
      keywords="concerts, musique, festival, fosse"
      image="https://media.vanityfair.com/photos/5e6921443b2c6a0008bf5b20/master/w_2560%2Cc_limit/FestivalCancellations-2020-GettyImages-174725380.jpg"
      ogLocale="fr_FR"
      url="http://lafosse.cre8ive.fr"
    />
    <vue-headful
      title="A concert's geography"
      description="Géographie d'une fosse de concert"
      keywords="concerts, music, festival, mosh pit, hall"
      image="https://media.vanityfair.com/photos/5e6921443b2c6a0008bf5b20/master/w_2560%2Cc_limit/FestivalCancellations-2020-GettyImages-174725380.jpg"
      ogLocale="en_US"
      url="http://lafosse.cre8ive.fr"
    />
    <vue-headful
      :title="lang === 'en' ? 'A concert\'s geography' : 'La fosse'"
    />
    <Menu
      :graphChange="paramGraph" :graphType="graphType"
      :langChange="paramLang" :lang="lang"
      :articleChange="paramArticle" :articleType="articleType"
    />
    <div id="topTitle">
      {{ lang === 'fr' ? 'Géographie de la fosse' : 'Concert geography' }}
    </div>
    <div id="scene" @mouseenter="zoneOut()"></div>
    <div id="scene_2_0" v-if="articleType === 'interactive'" ></div>
    <div id="scene_2_1" v-if="articleType === 'interactive'" ></div>
    <div v-if="articleType === 'interactive'">
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
          <ZoneDataHeader :zone="zonesSorted[hover]" />
          <ZoneData :zone="zonesSorted[hover]" style="margin: 20px;" />
        </div>
      </div>
      <div id="zone_chart" class="zone_popup" v-if="graphType !== 'none'">
        <ZoneChart :zones="zonesSorted" :hover="hover" height="650" :type="graphType" />
      </div>
    </div>
    <div v-if="articleType === 'read'" >
      <Article :zones="zonesSorted" />
    </div>
  </div>
</template>

<script>
import zones from '../zones'

import Menu from './Menu'
import Zone from './Zone'
import ZoneDataHeader from './ZoneDataHeader'
import ZoneData from './ZoneData'
import ZoneChart from './ZoneChart'
import Article from './Article'

export default {
  name: 'Main',
  components: {
    Menu,
    Zone,
    ZoneDataHeader,
    ZoneData,
    ZoneChart,
    Article
  },
  data: () => {
    return {
      zones,
      hover: -1,
      infoLeft: 500,
      windowWidth: window.innerWidth,
      graphType: 'radar',
      lang: 'fr',
      articleType: 'interactive'
    }
  },
  computed: {
    zonesSorted() {
      return zones[this.lang]
    },
    zoneInfo() {
      return this.hover >= 0
    }
  },
  methods: {
    zoneHover(zone) {
      this.hover = zone
      this.infoLeft = this.zonesSorted[zone].right > this.windowWidth * 2 / 10 // Bloc is 30% wide and we count from half 
        ? this.windowWidth * 2 / 10
        : this.zonesSorted[zone].right
    },
    zoneOut() {
      this.hover = -1
    },
    paramGraph(value) {
      this.graphType = value
    },
    paramLang(value) {
      this.lang = value
    },
    paramArticle(value) {
      this.articleType = value
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#topTitle {
  position: absolute;
  z-index: 119;
  background: white;
  padding: 10px 50px 10px 5px;
  border-bottom-right-radius: 10px;
  font-family: 'Carter One';
  color: #34495e;
  font-size: 40px;
  line-height: 40px;
  padding: 10px 100px 10px 15px;
  margin-bottom: 35px;
  border-bottom: solid 1px silver;
}
.shadow {
  box-shadow: 5px 3px 3px black;
}
#scene {
  position: fixed;
  display: block;
  width: 100%;
  height: 100%;
  background: center center no-repeat;
  background-image: url('https://upload.wikimedia.org/wikipedia/commons/thumb/0/0a/2018_-_Pol%E2%80%99and%E2%80%99Rock_Festival_-_Extrema_24.jpg/1280px-2018_-_Pol%E2%80%99and%E2%80%99Rock_Festival_-_Extrema_24.jpg');
  background-size: cover;
}
#scene_2_0 {
  position: fixed;
  display: block;
  width: 100%;
  height: 600px;
  top: 50%;
  margin-top: -300px;
  border-top: solid 1px silver;
  border-bottom: solid 1px silver;
}
#scene_2_1 {
  position: fixed;
  display: block;
  width: 1000px;
  height: 100%;
  left: 50%;
  margin-left: -500px;
  border-right: solid 1px silver;
  border-left: solid 1px silver;
}
#svg_main {
  opacity: 0.9;
  border: solid 1px silver;
  position: absolute;
  top: 50%;
  margin-top: -300px;
  left: 50%;
  margin-left: -500px;
  background-position: center center;
  background-size: cover;
  z-index: 2;
  border-radius: 10px;;
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
