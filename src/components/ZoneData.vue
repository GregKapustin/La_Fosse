<template>
  <div class="zoneData">
    <div class="image" :style="{ backgroundImage: 'url(' + zone.pic + ')' }"></div>
    <div class="caption margin"><span v-html="zone.caption" /></div>
    <h1>"<span v-html="zone.name" />"</h1>
    <div v-for="(data, section) in zone.data" class="data_section margin" :key="section">
      <div class="title" v-html="section + '&nbsp;:&nbsp;' + data.value + '&nbsp;/&nbsp;10'" />
      <div class="spacebar"><span class="barvalue" :style="{ background: 'blue', width: data.value * 10 + '%' }"></span></div>
      <div class="data_caption" v-html="data.caption" />
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
</style>
