<template>
  <path
    class="path"
    :d="path"
    :fill="fill"
    stroke="silver"
    @mouseenter="hover_function(i)"
    @mouseout="out_function()"
  />
</template>

<script>
export default {
  name: 'Zone',
  props: {
    name: String,
    path: String,
    zone: Number,
    density: Number,
    i: Number,
    hover_function: Function,
    out_function: Function,
    hovered: Boolean
  },
  computed: {
    fill() {
      return this.hovered
        ? "black"
        : 'url(#pattern_' + this.density + ')'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.path {
  position: absolute;
}
</style>
