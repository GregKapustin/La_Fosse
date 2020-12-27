<template>
  <div class="zoneData">
    <div class="image" :style="{ backgroundImage: 'url(' + zone.pic + ')' }"></div>
    <div class="caption margin"><span v-html="zone.caption" /></div>
    <h1 class="margin"><span class="big">"</span><span v-html="zone.name" /><span class="big">"</span></h1>
    <div v-for="(data, section) in zone.data" class="section margin" :key="section">
      <div class="title" v-html="section + '&nbsp;:&nbsp;' + data.value + '&nbsp;/&nbsp;10'" />
      <div class="spacebar"><span class="barvalue" :style="{ background: zone.color, width: data.value * 10 + '%' }"></span></div>
      <div class="data_caption">{{ data.caption }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ZoneData',
  props: {
    zone: Object
  },
  computed: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.margin {
  margin-left: 20px;
  margin-right: 20px;
}
h1 {
  font-family: 'Anton';
  font-style: italic;
  color: #34495e;
  margin-top: 10px;
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
.section .title {
  font-family: 'Anton';
  font-size: 200%;
  line-height: 95%;
  margin-top: 10px;
  margin-bottom: 10px;
}
.section .data_caption {
  margin-top: 5px;
  margin-bottom: 25px;
  font-family: 'Roboto';
  color:slategray;
  font-size: 100%;
  line-height: 90%;
}
.spacebar, .barvalue {
  display: block;
  width: 100%;
  height: 8px;
}
.spacebar {
  background: red;
}
.section {
  text-align: left;
}
</style>
