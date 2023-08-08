<template>
  <g :transform="`translate(${xScale(data.key)}, ${yScale(data.doc_count)})`">
    <rect
      :fill="color"
      :width="xScale.bandwidth()"
      :height="svgHeight - yScale(data.doc_count)"
      @mouseover="mouseover"
      @mouseout="mouseout"
    />
  </g>
</template>

<script>
export default {
  props: {
    data: {
      required: true,
      type: Object,
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

    svgHeight: {
      required: true,
      type: Number,
    },
  },

  methods: {
    mouseover() {
      this.$emit("onBarHover", this.data);
    },

    mouseout() {
      this.$emit("onBarOut");
    },
  },
};
</script>
