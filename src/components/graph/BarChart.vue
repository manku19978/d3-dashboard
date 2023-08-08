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
        <bar
          v-for="d in data"
          :key="d.key"
          :data="d"
          :xScale="xBar"
          :yScale="y"
          :svgHeight="dimensions.height - dimensions.margin.top - dimensions.margin.bottom"
          :color="color"
          @onBarHover="onBarHover"
          @onBarOut="onBarOut"
        />

        <g v-if="onBar && isToolTip">
          <rect :style="toolTipRectStyle" stroke-dasharray="1" :stroke="color" :y="toolTipY" />
          <text
            alignment-baseline="middle"
            :y="toolTipY - 10"
            :x="toolTipX"
            v-text="toolTipStrX"
            :style="toolTipTextStyle"
          />
          <text
            alignment-baseline="middle"
            :y="toolTipY - 24"
            :x="toolTipX"
            v-text="toolTipStrY"
            :style="toolTipTextStyle"
          />
        </g>
      </g>
    </svg>
  </div>
</template>

<script>
import * as d3 from "d3";
import Axis from "./Axis.vue";
import Bar from "./Bar.vue";
import { AXIS_LEFT, AXIS_BOTTOM } from "@/utils/constants";

export default {
  components: { Axis, Bar },

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
    onBar: false,
    toolTipY: null,
    toolTipX: null,
    toolTipStrX: null,
    toolTipStrY: null,
  }),

  computed: {
    toolTipTextStyle() {
      return {
        fontSize: 11,
        fontWeight: 700,
      };
    },

    toolTipRectStyle() {
      const { dimensions } = this;

      return {
        width: dimensions.width - dimensions.margin.left - dimensions.margin.right,
        height: 1,
        fill: "none",
      };
    },

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

    xBar() {
      const { width, margin } = this.dimensions;

      return d3
        .scaleBand()
        .range([0, width - margin.left - margin.right])
        .domain(
          this.data.map(function (d) {
            return d.key;
          })
        )
        .padding(0.1);
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

  methods: {
    onBarHover(data) {
      this.onBar = true;
      this.toolTipY = this.y(data.doc_count);
      this.toolTipX = this.xBar(data.key);
      this.toolTipStrX = new Date(data.key).toLocaleString();
      this.toolTipStrY = data.doc_count;
    },

    onBarOut() {
      this.onBar = false;
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
