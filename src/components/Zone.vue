<template>
  <path
    :d="path"
    :fill="'url(#pattern_' + density + ')'"
    stroke="silver"
  />
</template>

<script>
export default {
  name: 'Zone',
  props: {
    name: String,
    path: String,
    zone: Number,
    density: Number
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#scene {
  display: block;
  width: 100%;
  height: 100px;
  border-bottom: solid 2px black;
}
</style>
