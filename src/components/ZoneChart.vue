<template>
  <div class="zoneChartRender">
    <apexchart width="100%" height="1000" type="radar" :options="options" :series="series"></apexchart>
  </div>
</template>

<script>
import _ from 'lodash'

export default {
  name: 'ZoneChart',
  components: {
  },
  props: {
    hover: Number,
    zones: Array
  },
  data: function() {
    return {
      options: {
        chart: {
          id: 'Zones-Chart'
        },
        xaxis: {
          categories: _.keys(this.zones[0].data)
        },
        stroke: {
          show: false
        },
        markers: {
          size: 0
        },
        subtitle: {
          text: this.subtitle
        }
      }
    }
  },
  computed: {
    zone() {
      return this.zones[this.hover]
    },
    series() {
      return this.hover < 0
        ? _.map(this.zones, this.zoneGetData)
        : [this.zoneGetData(this.zone)]
    },
    subtitle() {
      return this.hover < 0
        ? ''
        : this.zone.caption
    }
  },
  methods: {
    zoneGetData: (zone) => {
      return {
        name: zone.name,
        data: _.values(zone.data),
        color: zone.color
      }
    }
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
