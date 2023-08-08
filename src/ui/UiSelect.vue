<template>
  <div>
    <label class="text-13 semi-bold" v-if="label">{{ label }}</label>
    <select :value="value" @change="handleChange" :name="name">
      <option disabled value="">{{ placeholder }}</option>
      <option v-for="option in options" :key="option" :value="option">{{ option }}</option>
    </select>
  </div>
</template>

<script>
export default {
  props: {
    name: {
      type: String,
      required: false,
    },

    value: {
      type: String,
      required: true,
    },

    options: {
      type: Array,
      required: true,
    },

    label: {
      type: String,
      required: false,
    },

    placeholder: {
      type: String,
      required: false,
    },
  },

  emits: ["selectChange"],

  methods: {
    handleChange(e) {
      this.$emit("selectChange", e);
    },
  },
};
</script>

<style scoped>
label {
  display: block;
}

select {
  margin-top: 5px;
  height: 40px;
  width: 207px;
  border: 1px solid var(--grey);
  box-shadow: 0px 4px 3px rgba(0, 0, 0, 0.02);
  border-radius: 3px;
  outline: none;
  padding: 0 10px;
}
</style>
