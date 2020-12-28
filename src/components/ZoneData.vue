<template>
  <div class="zoneData">
    <div v-for="(data, section) in zone.data" class="data_section margin" :key="section">
      <div class="title" v-html="section + '&nbsp;:&nbsp;' + data.value + '&nbsp;/&nbsp;10'" />
      <div class="spacebar"><span class="barvalue" :style="{ background: 'blue', width: data.value * 10 + '%' }"></span></div>
      <div class="data_caption" v-html="data.caption" />
    </div>
  </div>
</template>

<script>
import _ from 'lodash'

export default {
  name: 'ZoneData',
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
.data_section .title {
  font-family: 'Anton';
  font-size: 200%;
  line-height: 95%;
  margin-top: 10px;
  margin-bottom: 10px;
}
.data_section .data_caption {
  margin-top: 5px;
  font-family: 'Roboto';
  color:slategray;
  font-size: 100%;
  line-height: 100%;
  margin-right: 40px;
  text-align: justify
}
.spacebar, .barvalue {
  display: block;
  width: 100%;
  height: 12px;
}
.spacebar {
  background: red;
}
.data_section {
  text-align: left;
  margin-bottom: 50px;
}
.zoneData .grade {
  font-family: 'Anton';
  font-size: 200%;
  line-height: 95%;
  margin-top: 10px;
  margin-bottom: 10px;
  color: white;
}
.zoneData .grade .spacebar {
  position: absolute;
  margin-top: -40px;
  height: 50px;
  z-index: -1;
}
.zoneData .grade .spacebar .barvalue {
  height: 50px;
}
</style>
