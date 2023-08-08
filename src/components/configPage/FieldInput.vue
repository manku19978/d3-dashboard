<template>
  <div class="flex">
    <ui-input
      :value="field"
      placeholder="Field Name"
      style="margin-right: 10px"
      @handleChange="handleFieldChange($event)"
    />
    <ui-select
      :value="type"
      :options="FIELD_INPUT_TYPES"
      placeholder="Type"
      @selectChange="handleTypeChange($event)"
    />
    <div v-if="field && type" class="delete cp" @click="$emit('delete')">&#8211;</div>
  </div>
</template>

<script>
import UiInput from "@/ui/UiInput.vue";
import UiSelect from "@/ui/UiSelect.vue";
import { FIELD_INPUT_TYPES } from "@/utils/constants";

export default {
  name: "FieldInput",

  components: {
    UiInput,
    UiSelect,
  },

  props: ["field", "type"],

  emits: ["update", "delete"],

  data: () => ({
    FIELD_INPUT_TYPES,
  }),

  methods: {
    handleFieldChange(event) {
      this.$emit("update", {
        field: event.target.value,
        type: this.type,
      });
    },

    handleTypeChange(event) {
      this.$emit("update", {
        field: this.field,
        type: event.target.value,
      });
    },
  },
};
</script>

<style scoped>
.delete {
  border: 1px solid var(--error);
  border-radius: 50%;
  background-color: var(--error);
  color: var(--white);
  width: 24px;
  height: 24px;
  line-height: 22px;
  text-align: center;
  margin-left: 20px;
}
</style>
