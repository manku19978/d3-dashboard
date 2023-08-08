<template>
  <section class="popup">
    <div class="modal">
      <div class="header">
        <a class="close" @click="$emit('close')">&#215;</a>
        <p class="text-28 bold">Create Config</p>
      </div>

      <div class="content">
        <step n="1" name="Event Name">
          <ui-input
            :value="name"
            placeholder="e.g. view-post"
            @handleChange="handleNameChange($event.target.value)"
          />
        </step>
        <step n="2" name="Payload Schema">
          <schema-input :value="schema" @update="handleSchemaUpdate" />
        </step>
        <step n="3" name="Enrichments">
          <enrichment @handleEnrichment="handleEnrichment($event)" />
        </step>
      </div>

      <div class="footer">
        <!-- TODO: handle create -->
        <ui-button styleType="primary" :handler="submitConfig">Create</ui-button>
      </div>
    </div>

    <!-- <pre style="position: fixed; right: 0">{{ JSON.stringify(schema, null, 2) }}</pre> -->
  </section>
</template>

<script>
import UiInput from "@/ui/UiInput.vue";
import UiButton from "@/ui/UiButton.vue";
import Step from "./Step.vue";
import SchemaInput from "./SchemaInput.vue";
import Enrichment from "./Enrichment.vue";

export default {
  name: "CreateConfig",

  components: {
    UiInput,
    UiButton,
    Step,
    SchemaInput,
    Enrichment,
  },

  data: () => ({
    name: "",
    schema: [],
    enrichments: [],
  }),

  methods: {
    handleNameChange(name) {
      this.name = name;
    },

    handleSchemaUpdate(schema) {
      const filterOutEmpty = (schema) =>
        schema.filter((fieldSchema) => {
          if (!fieldSchema.field) return false;
          if (!fieldSchema.type) return false;
          if (fieldSchema.type === "nested") {
            fieldSchema.schema = filterOutEmpty(fieldSchema.schema);
          }
          return true;
        });
      this.schema = filterOutEmpty(schema);
    },

    handleEnrichment(payload) {
      this.enrichments = payload;
    },

    submitConfig() {
      const { name, schema, enrichments } = this;
      const reqObj = {
        name,
        schema,
        enrichments,
      };

      console.log(reqObj);
    },
  },
};
</script>

<style scoped>
.popup {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.2);
  display: flex;
  z-index: 9999;
}

.modal {
  margin: auto;
  padding: 24px;
  background-color: white;
  width: 80%;
  height: 80%;
  max-width: 100%;
  border-radius: 3px;
  position: relative;
  overflow: hidden;

  display: flex;
  flex-direction: column;
}

.close {
  font-size: 30px;
  position: absolute;
  right: 0;
  top: 0;
  width: 48px;
  height: 48px;
  line-height: 48px;
  background-color: var(--grey);
  text-align: center;
  cursor: pointer;
}

.content {
  margin-top: 25px;
  flex-grow: 1;
  overflow: auto;
}

.footer {
  padding-top: 25px;
}
</style>
