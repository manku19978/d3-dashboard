<template>
  <div>
    <div v-for="(fieldSchema, i) in schema" :key="i">
      <field-input
        :field="fieldSchema.field"
        :type="fieldSchema.type"
        @update="handleFieldUpdate(i, $event)"
        @delete="handleFieldDelete(i)"
      />
      <schema-input
        v-if="fieldSchema.type === 'nested'"
        :value="fieldSchema.schema"
        class="sub-schema"
        @update="handleSubSchemaUpdate(i, $event)"
      />
    </div>
  </div>
</template>

<script>
import FieldInput from "./FieldInput.vue";

const empty = () => ({ field: "", type: "" });
const cloneJson = (json) => JSON.parse(JSON.stringify(json));

export default {
  name: "SchemaInput",

  components: {
    FieldInput,
  },

  props: ["value"],
  emits: ["update"],

  data() {
    return {
      schema: cloneJson(this.value || []),
    };
  },

  created() {
    this.schema.push(empty());
  },

  methods: {
    handleFieldUpdate(i, { field, type }) {
      const data = { field, type };
      if (data.type === "nested") data.schema = [];

      this.schema[i] = data;

      const shouldAddEmpty = i === this.schema.length - 1 && field && type;
      if (shouldAddEmpty) this.schema.push(empty());

      this.emitUpdate();
    },

    handleFieldDelete(i) {
      this.schema.splice(i, 1);
      this.emitUpdate();
    },

    handleSubSchemaUpdate(i, schema) {
      this.schema[i].schema = schema;
      this.emitUpdate();
    },

    emitUpdate() {
      this.$emit("update", cloneJson(this.schema));
    },
  },
};
</script>

<style scoped>
.sub-schema {
  padding-left: 30px;
  border-left: 1px dashed var(--darkGrey);
}
</style>
