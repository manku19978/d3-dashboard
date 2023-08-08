<template>
  <g ref="axis" :transform="this.transform" />
</template>

<script>
import * as d3 from "d3";
import { AXIS_LEFT, AXIS_BOTTOM } from "@/utils/constants";

export default {
  props: {
    type: {
      required: true,
      type: String,
      validator(value) {
        return [AXIS_LEFT, AXIS_BOTTOM].includes(value);
      },
    },

    dimensions: {
      required: false,
      type: Object,
    },

    transform: {
      required: false,
      type: String,
    },

    scale: {
      required: true,
      type: Function,
    },
  },

  watch: {
    scale() {
      this.plotAxis();
    },
  },

  methods: {
    plotAxis() {
      const axisGenerator = this.type === AXIS_LEFT ? d3.axisLeft : d3.axisBottom;
      const axis = axisGenerator(this.scale);
      const axisGroup = d3.select(this.$refs.axis);

      if (this.type === AXIS_LEFT) {
        const { width, margin } = this.dimensions;

        axisGroup
          .call(axis.tickSize(-width + margin.right + margin.left))
          .call((g) => g.select(".domain").remove())
          .call((g) =>
            g.selectAll(".tick line").attr("stroke-dasharray", "2,2").attr("stroke", "#ebebeb")
          )
          .call((g) => g.selectAll(".tick text").attr("dx", -8));
      } else {
        axisGroup
          .call(axis.tickSize(0))
          .call((g) => g.select(".domain").remove())
          .call((g) => g.selectAll(".tick text").attr("dy", 16));
      }
    },
  },

  mounted() {
    this.plotAxis();
  },
};
</script>
