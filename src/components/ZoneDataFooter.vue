<template>
  <div class="zoneData">
    <div class="total">
      <div class="grade">
        <div class="title">
          <span class="a">{{ lang === 'fr' ? 'Moyenne' : 'Grade' }} : </span><span class="b">{{ total }}</span><span class="c">/10</span>
        </div>
        <div class="spacebar"><span class="barvalue" :style="{ background: 'blue', width: parseInt(total) * 10 + '%' }"></span></div>
      </div>
      <div class="total_subtitle" v-html="zone.total_subtitle" />
    </div>
  </div>
</template>

<script>
import _ from 'lodash'

export default {
  name: 'ZoneDataFooter',
  props: {
    zone: Object,
    lang: String
  },
  computed: {
    total() {
      return (_.sum(_.map(this.zone.data, 'value')) / 6).toLocaleString('fr-FR', {maximumFractionDigits: 1, useGrouping:false})
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.spacebar, .barvalue {
  display: block;
  width: 100%;
  height: 12px;
}
.spacebar {
  background: red;
}
.zoneData .grade {
  font-family: 'Anton';
  font-size: 200%;
  line-height: 95%;
  margin-top: 10px;
  margin-bottom: 10px;
  color: white;
  margin-top: 30px;
}
.zoneData .grade .title {
  padding-left: 40px;
  position: absolute;
  z-index: 2;
  color: white;
  margin-top: -32px;
}
.zoneData .grade .spacebar {
  position: absolute;
  margin-top: -40px;
  height: 50px;
  z-index: 1;
}
.zoneData .grade .spacebar .barvalue {
  height: 50px;
}
.zoneData .total_subtitle {
  margin-top: 63px;
  padding: 40px;
  padding-top: 17px;
  font-family: 'Roboto';
  text-align: left;
  font-style: italic;
  line-height: 96%;
  font-size: 120%;
  margin-bottom: 10px;
}
</style>
