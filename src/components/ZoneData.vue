<template>
  <div class="zoneData">
    <h1><span class="big">"</span><span v-html="zone.name" /><span class="big">"</span></h1>
    <div class="image" :style="{ backgroundImage: 'url(' + zone.pic + ')' }"></div>
    <div class="caption"><span v-html="zone.caption" /></div>
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
  font-family: 'Teko';
  font-style: italic;
  color:slategray;
  font-size: 120%;
  font-weight: 100;
  line-height: 90%;
  padding-top: 10px;
}
</style>
