<template>
  <div class="zoneChartRender">
    <div class="columns is-centered">
      <div class="row">
        <b-field>
          <b-radio-button v-model="type" native-value="bar" size="is-small">
            <span>Bars</span>
          </b-radio-button>
          <b-radio-button v-model="type" native-value="radar" size="is-small">
            <span>Radar</span>
          </b-radio-button>
          <b-radio-button v-model="type" native-value="none" size="is-small">
            <span>X</span>
          </b-radio-button>
        </b-field>
      </div>
    </div>
    <apexchart v-if="type != 'none'" width="100%" :height="height + 'px'" :type="type" :options="options" :series="series"></apexchart>
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
    zones: Array,
    height: String
  },
  data: function() {
    return {
      type: 'radar',
      options: {
        chart: {
          id: 'Zones-Chart',
          toolbar: {
            show: false
          }
        },
        xaxis: {
          categories: _.keys(this.zones[0].data)
        },
        endingShape: 'rounded',
        horizontal: true,
        yaxis: {
          max: 10,
          min: 0,
          tickAmount: 5,
          show: false
        },
        dataLabels: {
          enabled: false
        },
        markers: {
          size: 0
        },
        stroke: {
          show: false
        },
        tooltip: {
          position: 'topRight',
          followCursor: true,
          custom: this.getTooltip
        }
      }
    }
  },
  computed: {
    hovered() {
      return this.hover >= 0
    },
    zone() {
      return this.zones[this.hover]
    },
    series() {
      return !this.hovered
        ? _.map(this.zones, this.zoneGetData)
        : [this.zoneGetData(this.zone)]
    },
    subtitle() {
      return this.hovered
        ? ''
        : this.zone.caption
    }
  },
  methods: {
    zoneGetData: (zone) => {
      return {
        name: zone.name,
        data: _.map(_.values(zone.data), 'value'),
        color: zone.color
      }
    },
    getTooltip({series, seriesIndex, dataPointIndex}) {
      const zone = this.hovered ? this.zone : this.zones[seriesIndex]
      return '<div class="tooltip">'
          + '<div class="section">"' + zone.name + '"</div>'
          + '<div class="note">' + _.keys(zone.data)[dataPointIndex] + ' : ' + series[seriesIndex][dataPointIndex] + '/10</div>'
        + '</div>'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.apexcharts-tooltip {
  overflow: visible!important;
}
.tooltip .section {
  font-family: 'Teko';
  color:rgb(66, 66, 66);
  font-size: 160%;
  line-height: 90%;
  padding-top: 10px;
  border-bottom: solid 1px silver;
}
.tooltip .note {
  margin: 10px;
  font-family: 'Anton';
  color:rgb(66, 66, 66);
  font-size: 200%;
  font-weight: bolder;
  line-height: 90%;
}
</style>
