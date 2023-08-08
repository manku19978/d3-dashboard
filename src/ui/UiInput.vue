<template>
  <div>
    <label class="text-13 semi-bold" v-if="label">{{ label }}</label>
    <input
      :value="value"
      @input="handleChange"
      class="text-14 bg-white semi-bold"
      :placeholder="placeholder"
      :name="name"
    />
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
      required: true,
      type: String,
    },

    label: {
      required: false,
      type: String,
    },

    placeholder: {
      required: false,
      type: String,
    },
  },

  emits: ["handleChange"],

  methods: {
    handleChange(e) {
      this.$emit("handleChange", e);
    },
  },
};
</script>

<style scoped>
input {
  margin-top: 5px;
  height: 40px;
  width: 207px;
  border: 1px solid var(--grey);
  box-shadow: 0px 4px 3px rgba(0, 0, 0, 0.02);
  border-radius: 3px;
  outline: none;
  padding: 12px 10px;
}

label {
  display: block;
}
</style>
