<template>
  <div>
    <p class="text-14 text-error" v-if="jsonError && jsonstr">{{ jsonError }}</p>
    <p class="text-14 text-success" v-if="validJson">Valid JSON</p>
    <textarea
      @input="handleDataChange"
      v-model="jsonstr"
      rows="10"
      class="form-control"
      placeholder="Enrichment JSON...(in array format)"
    ></textarea>
  </div>

  <div v-if="jsonstr.length > 0">
    <ui-button class="width" :styleType="BUTTON_PRIMARY" :handler="formatJSON">Format</ui-button>
  </div>
</template>

<script>
import UiButton from "@/ui/UiButton.vue";
import { BUTTON_WHITE, BUTTON_PRIMARY } from "@/utils/constants.js";

export default {
  components: { UiButton },

  emits: ["handleEnrichment"],

  data: () => ({
    BUTTON_WHITE,
    BUTTON_PRIMARY,
    jsonstr: "",
    jsonError: "",
    validJson: null,
    formCount: 0,
  }),

  methods: {
    handleDataChange() {
      this.validateJSON(this.jsonstr);

      if (!this.jsonError) {
        const reqObj = JSON.parse(this.jsonstr);

        if (Array.isArray(reqObj)) {
          this.enrichments = reqObj;
          this.$emit("handleEnrichment", reqObj);
        } else {
          this.$emit("handleEnrichment", []);
        }
      }
    },

    validateJSON(json) {
      try {
        JSON.parse(json);
        this.jsonError = "";
        this.validJson = true;
      } catch (e) {
        this.jsonError = e.message;
        this.validJson = false;
      }
    },

    formatJSON() {
      if (!this.validJson) {
        alert("Format once your JSON is valid");
        return;
      }

      const parseJSON = JSON.parse(this.jsonstr);
      const JSONInPrettyFormat = JSON.stringify(parseJSON, undefined, 4);
      this.jsonstr = JSONInPrettyFormat;
    },
  },
};
</script>

<style scoped>
textarea {
  width: 424px;
  padding: 12px 10px;
  margin-top: 5px;
  resize: none;
  border: 1px solid var(--grey);
  box-shadow: 0px 4px 3px rgba(0, 0, 0, 0.02);
  border-radius: 3px;
  outline: none;
}

.width {
  margin-right: 10px;
}
</style>
