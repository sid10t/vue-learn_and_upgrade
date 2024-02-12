<template>
  <div :class="className" :style="{ height: height, width: width }"></div>
</template>

<script>
import _ from "lodash";
import * as echarts from "echarts";

export default {
  name: "DataChild",
  props: {
    className: {
      type: String,
      default: "DataChild",
    },
    width: {
      type: String,
      default: "100%",
    },
    height: {
      type: String,
      default: "500px",
    },
    autoResize: {
      type: Boolean,
      default: true,
    },
    series: {
      type: Array,
      default: null,
    },
  },
  data() {
    return {
      chart: null,
      option: {
        title: {
          text: "ECharts 入门示例",
        },
        tooltip: {},
        legend: {
          data: ["销量"],
        },
        xAxis: {
          data: ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"],
        },
        yAxis: {},
        series: [
          {
            name: "销量",
            type: "bar",
            data: [5, 20, 36, 10, 10, 20],
          },
        ],
      },
    };
  },
  watch: {
    option: {
      handler(newVal, oldVal) {
        if (this.chart) {
          if (newVal) {
            this.chart.setOption(newVal);
          } else {
            this.chart.setOption(oldVal);
          }
        } else {
          this.initChart();
        }
      },
      deep: true,
    },
  },
  mounted() {
    this.initChart();
    if (this.autoResize) {
      window.addEventListener("resize", this.resizeChart);
    }
  },
  beforeDestroy() {
    if (!this.chart) {
      return;
    }
    if (this.autoResize) {
      window.removeEventListener("resize", this.resizeChart);
    }
    this.chart.dispose();
    this.chart = null;
  },
  methods: {
    initChart() {
      this.chart = echarts.init(this.$el, "shine");
      this.option.series = this.series;
      this.chart.setOption(this.option);
    },
    resizeChart: _.debounce(function () {
      console.log("chart resize!");
      this.chart.resize();
    }, 100),
  },
};
</script>
