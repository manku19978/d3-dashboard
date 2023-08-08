<template>
  <path
    ref="path"
    :d="isArea ? area : d"
    :fill="isArea ? fillColor : 'none'"
    :opacity="opacity"
    :stroke="isArea ? 'none' : color"
    :stroke-width="strokeWidth"
  />

  <g v-if="isToolTip">
    <rect
      :style="toolTipRectStyle"
      ref="focusRect"
      stroke-dasharray="1"
      :stroke="isArea ? fillColor : color"
    />
    <circle
      :fill="isArea ? fillColor : color"
      ref="focus"
      stroke="white"
      stroke-width="3"
      r="8.5"
      opacity="0"
    />
    <text ref="focusTextX" text-anchor="left" alignment-baseline="middle" opacity="0" />
    <text ref="focusTextY" text-anchor="left" alignment-baseline="middle" opacity="0" />
  </g>

  <rect
    :style="overlayStyle"
    ref="overlay"
    v-if="isToolTip"
    @mouseover="mouseover"
    @mousemove="mousemove($event)"
    @mouseout="mouseout"
  />
</template>

<script>
import * as d3 from "d3";

export default {
  props: {
    data: {
      required: true,
      type: Array,
    },

    xScale: {
      required: true,
      type: Function,
    },

    yScale: {
      required: true,
      type: Function,
    },

    color: {
      required: false,
      type: String,
      default: () => "steelblue",
    },

    strokeWidth: {
      required: false,
      type: Number,
      default: () => 1.5,
    },

    isArea: {
      required: false,
      type: Boolean,
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

    dimensions: {
      type: Object,
      required: false,
    },

    isToolTip: {
      required: false,
      type: Boolean,
      default: () => true,
    },
  },

  methods: {
    mouseover() {
      this.$refs.focus.style.opacity = "1";
      this.$refs.focusRect.style.opacity = "1";
      this.$refs.focusTextX.style.opacity = "1";
      this.$refs.focusTextY.style.opacity = "1";
    },

    mousemove(e) {
      const bisect = d3.bisector(function (d) {
        return d.key;
      }).left;

      const x0 = this.xScale.invert(d3.pointer(e)[0]);
      var i = bisect(this.data, x0, 1);
      const selectedData = this.data[i];

      d3.select(this.$refs.focus)
        .attr("cx", this.xScale(selectedData.key))
        .attr("cy", this.yScale(selectedData.doc_count));

      d3.select(this.$refs.focusRect).attr("x", this.xScale(selectedData.key));

      d3.select(this.$refs.focusTextX)
        .html(new Date(selectedData.key).toLocaleString())
        .attr("x", this.xScale(selectedData.key) + 10)
        .attr("y", this.yScale(selectedData.doc_count) + 6)
        .attr("font-size", 11)
        .attr("font-weight", 700);

      d3.select(this.$refs.focusTextY)
        .html(selectedData.doc_count)
        .attr("x", this.xScale(selectedData.key) + 10)
        .attr("y", this.yScale(selectedData.doc_count) - 8)
        .attr("font-size", 11)
        .attr("font-weight", 700);
    },

    mouseout() {
      this.$refs.focus.style.opacity = "0";
      this.$refs.focusTextX.style.opacity = "0";
      this.$refs.focusTextY.style.opacity = "0";
      this.$refs.focusRect.style.opacity = "0";
    },
  },

  computed: {
    overlayStyle() {
      return {
        width: this.dimensions.width,
        height: this.dimensions.height,
        fill: "none",
        pointerEvents: "all",
      };
    },

    toolTipRectStyle() {
      return {
        width: 1,
        height: this.dimensions.height,
        fill: "none",
        opacity: "0",
      };
    },

    d() {
      const line = d3
        .line()
        .x((d) => this.xScale(d.key))
        .y((d) => this.yScale(d.doc_count));

      return line(this.data);
    },

    area() {
      const area = d3
        .area()
        .x((d) => this.xScale(d.key))
        .y0(this.yScale(0))
        .y1((d) => this.yScale(d.doc_count));

      return area(this.data);
    },
  },
};
</script>
