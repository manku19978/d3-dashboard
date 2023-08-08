<template>
  <div>
    <p class="text-28 bold" v-if="title.length > 0">{{ title }}</p>

    <svg :style="svgStyleObject">
      <g class="g" :style="gStyleObject">
        <axis :type="AXIS_LEFT" :scale="y" :dimensions="dimensions" />
        <axis
          :type="AXIS_BOTTOM"
          :scale="x"
          :transform="`translate(0, ${
            dimensions.height - dimensions.margin.top - dimensions.margin.bottom
          })`"
        />
        <single-line
          :data="data"
          :xScale="x"
          :yScale="y"
          :color="color"
          :isArea="isArea"
          :fillColor="fillColor"
          :opacity="opacity"
          :isToolTip="isToolTip"
          :dimensions="{
            width: dimensions.width - dimensions.margin.left - dimensions.margin.right,
            height: dimensions.height - dimensions.margin.top - dimensions.margin.bottom,
          }"
        />
      </g>
    </svg>
  </div>
</template>

<script>
import * as d3 from "d3";
import Axis from "./Axis.vue";
import SingleLine from "./Line.vue";
import { AXIS_LEFT, AXIS_BOTTOM } from "@/utils/constants";

export default {
  components: { Axis, SingleLine },

  props: {
    data: {
      type: Array,
      required: true,
    },

    dimensions: {
      type: Object,
      required: true,
    },

    title: {
      type: String,
      required: true,
    },

    isArea: {
      type: Boolean,
      required: false,
      default: () => false,
    },

    fillColor: {
      required: false,
      type: String,
      default: () => "#cce5df",
    },

    opacity: {
      required: false,
      type: Number,
      default: () => 1,
    },

    color: {
      required: false,
      type: String,
      default: () => "steelblue",
    },

    isToolTip: {
      required: false,
      type: Boolean,
      default: () => true,
    },
  },

  data: () => ({
    AXIS_LEFT,
    AXIS_BOTTOM,
  }),

  computed: {
    svgStyleObject() {
      const { width, height } = this.dimensions;

      return {
        width,
        height,
      };
    },

    gStyleObject() {
      const { margin } = this.dimensions;

      return {
        transform: `translate(${margin.left}px, ${margin.top}px)`,
      };
    },

    x() {
      const { width, margin } = this.dimensions;

      return d3
        .scaleTime()
        .domain(
          d3.extent(this.data, function (d) {
            return d.key;
          })
        )
        .range([0, width - margin.left - margin.right]);
    },

    y() {
      const { height, margin } = this.dimensions;

      return d3
        .scaleLinear()
        .domain([
          0,
          d3.max(this.data, function (d) {
            return +d.doc_count;
          }),
        ])
        .range([height - margin.top - margin.bottom, 0]);
    },
  },
};
</script>

<style scoped>
div {
  background: var(--white);
  border-radius: 6px;
  border: 1px solid var(--grey);
  width: fit-content;
  padding: 20px 16px 16px 16px;
}

svg {
  overflow: visible;
}

p {
  margin-bottom: 12px;
}
</style>
