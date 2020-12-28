<template>
  <div class="zoneData">
    <div>
      <div class="image" :style="{ backgroundImage: 'url(' + zone.pic + ')' }"></div>
      <div class="caption margin"><span v-html="zone.caption" /></div>
      <h1>"<span v-html="zone.name" />"</h1>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ZoneDataHeader',
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
</style>
