<template>
  <div class="btn-wrapper text-14 flex cp semi-bold" :class="styleObject" @click="handler">
    <img :src="iconUrl" v-if="iconUrl" alt="Button Image" />

    <p>
      <slot></slot>
    </p>
  </div>
</template>

<script>
import { BUTTON_PRIMARY, BUTTON_BLACK, BUTTON_WHITE } from "../utils/constants";

export default {
  props: {
    iconUrl: {
      required: false,
    },

    styleType: {
      type: String,
      required: false,
      validator(value) {
        return [BUTTON_WHITE, BUTTON_BLACK, BUTTON_PRIMARY].includes(value);
      },
    },

    handler: {
      type: Function,
      required: false,
    },
  },

  computed: {
    styleObject() {
      return {
        white: this.styleType === "white",
        "bg-primary": this.styleType === "primary",
        "bg-white": this.styleType === "white",
        "bg-black": this.styleType === "black",
        "text-white": this.styleType === "primary" || this.styleType === "black",
      };
    },
  },
};
</script>

<style scoped>
.btn-wrapper {
  padding: 12px 16px;
  border-radius: 6px;
  width: fit-content;
}

img {
  height: 14px;
  width: 14px;
  margin-right: 10.5px;
}

.white {
  border: 1px solid #ebebeb;
  box-shadow: 0px 4px 3px rgba(0, 0, 0, 0.02);
}
</style>
