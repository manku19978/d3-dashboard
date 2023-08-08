<template>
  <div class="container">
    <p class="text-36 bold">Dashboard</p>

    <div class="flex char-container">
      <line-chart :data="data1" :dimensions="dimensions" title="Line Chart" color="#FFA800" />
      <bar-chart :data="data" :dimensions="dimensions1" title="Bar Chart" color="#0A5DFF" />
    </div>

    <div class="flex char-container">
      <bar-chart :data="data1" :dimensions="dimensions2" title="Bar Chart" color="#20C933" />
      <line-chart
        :data="data"
        :dimensions="dimensions3"
        title="Line Chart"
        :isArea="true"
        fillColor="#624ce0"
        :opacity="0.5"
      />
    </div>
  </div>
</template>

<script>
import LineChart from "../components/graph/LineChart.vue";
import BarChart from "../components/graph/BarChart.vue";

export default {
  components: { BarChart, LineChart },

  data() {
    return {
      dimensions: {
        width: 390,
        height: 240,
        margin: {
          top: 10,
          bottom: 30,
          left: 42,
          right: 30,
        },
      },
      dimensions1: {
        width: 850,
        height: 240,
        margin: {
          top: 10,
          bottom: 30,
          left: 30,
          right: 30,
        },
      },
      dimensions2: {
        width: 850,
        height: 240,
        margin: {
          top: 10,
          bottom: 30,
          left: 42,
          right: 30,
        },
      },
      dimensions3: {
        width: 390,
        height: 240,
        margin: {
          top: 10,
          bottom: 30,
          left: 30,
          right: 30,
        },
      },
      data: [
        {
          key: 1618770600000,
          doc_count: 182,
        },
        {
          key: 1618857000000,
          doc_count: 639,
        },
        {
          key: 1618943400000,
          doc_count: 317,
        },
        {
          key: 1619029800000,
          doc_count: 323,
        },
        {
          key: 1619116200000,
          doc_count: 176,
        },
        {
          key: 1619202600000,
          doc_count: 7,
        },
        {
          key: 1619289000000,
          doc_count: 65,
        },
        {
          key: 1619375400000,
          doc_count: 477,
        },
        {
          key: 1619461800000,
          doc_count: 803,
        },
        {
          key: 1619548200000,
          doc_count: 470,
        },
        {
          key: 1619634600000,
          doc_count: 350,
        },
        {
          key: 1619721000000,
          doc_count: 357,
        },
        {
          key: 1619807400000,
          doc_count: 115,
        },
        {
          key: 1619893800000,
          doc_count: 23,
        },
        {
          key: 1619980200000,
          doc_count: 694,
        },
        {
          key: 1620066600000,
          doc_count: 9,
        },
      ],
      data1: [
        {
          key_as_string: "1644235680000",
          key: 1644235680000,
          doc_count: 23844,
        },
        {
          key_as_string: "1644235740000",
          key: 1644235740000,
          doc_count: 54475,
        },
        {
          key_as_string: "1644235800000",
          key: 1644235800000,
          doc_count: 48668,
        },
        {
          key_as_string: "1644235860000",
          key: 1644235860000,
          doc_count: 50707,
        },
        {
          key_as_string: "1644235920000",
          key: 1644235920000,
          doc_count: 50573,
        },
        {
          key_as_string: "1644235980000",
          key: 1644235980000,
          doc_count: 39126,
        },
        {
          key_as_string: "1644236040000",
          key: 1644236040000,
          doc_count: 32614,
        },
        {
          key_as_string: "1644236100000",
          key: 1644236100000,
          doc_count: 33223,
        },
        {
          key_as_string: "1644236160000",
          key: 1644236160000,
          doc_count: 32774,
        },
        {
          key_as_string: "1644236220000",
          key: 1644236220000,
          doc_count: 33172,
        },
        {
          key_as_string: "1644236280000",
          key: 1644236280000,
          doc_count: 25319,
        },
        {
          key_as_string: "1644236340000",
          key: 1644236340000,
          doc_count: 203,
        },
        {
          key_as_string: "1644236400000",
          key: 1644236400000,
          doc_count: 96,
        },
        {
          key_as_string: "1644236460000",
          key: 1644236460000,
          doc_count: 89,
        },
        {
          key_as_string: "1644236520000",
          key: 1644236520000,
          doc_count: 123,
        },
        {
          key_as_string: "1644236580000",
          key: 1644236580000,
          doc_count: 53,
        },
      ],
    };
  },
};
</script>

<style scoped>
.container {
  margin: 20px 24px;
}

p {
  margin-bottom: 25px;
}

.char-container {
  justify-content: space-between;
  margin-bottom: 24px;
}
</style>
