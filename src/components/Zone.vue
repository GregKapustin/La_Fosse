<template>
  <path
    class="path"
    :d="path"
    :fill="fill"
    stroke="silver"
    @mouseover="hover_function(i)"
    viewbox="0 0 100 100"
  />
</template>

<script>
export default {
  name: 'Zone',
  props: {
    path: String,
    density: Number,
    i: Number,
    hover_function: Function,
    out_function: Function,
    hovered: Boolean,
    color: String
  },
  computed: {
    fill() {
      return this.hovered
        ? 'black'
        : this.color
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
