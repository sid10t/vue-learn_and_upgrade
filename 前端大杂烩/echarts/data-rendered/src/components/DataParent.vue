<template>
  <data-child :series="this.series"></data-child>
</template>

<script>
import DataChild from "./DataChild.vue";
import axios from "axios";

export default {
  name: "DataParent",
  components: {
    DataChild,
  },
  data() {
    return {
      series: [
        {
          name: "销量",
          type: "bar",
          data: [],
        },
      ],
    };
  },
  created() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      const url = "";
      axios
        .get(url + "/test/data")
        .then((resp) => {
          this.series[0].data = resp.data.data;
          this.series[0].time = new Date();
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>
