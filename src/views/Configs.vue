<template>
  <div class="container">
    <p class="text-36 bold title">Configs</p>
    <ui-button :styleType="BUTTON_PRIMARY" @click="isCreating = true">Create Config</ui-button>

    <!-- TODO: Show list of configs -->

    <create-config v-if="isCreating" @close="this.isCreating = false" />
  </div>
</template>

<script>
import UiButton from "@/ui/UiButton.vue";
import CreateConfig from "@/components/configPage/CreateConfig.vue";
import { BUTTON_PRIMARY } from "@/utils/constants";

export default {
  components: { UiButton, CreateConfig },

  data() {
    return {
      isCreating: false,

      BUTTON_PRIMARY,
    };
  },

  methods: {
    handleChange(event) {
      this.value.name = event.target.value;
    },

    handleFieldForm(payload) {
      let isPresent = false;
      this.value.schema.forEach((item) => {
        if (item.id === payload.id) {
          isPresent = true;
        }
      });

      if (!isPresent) {
        this.value.schema.push(payload);
      }
    },

    addFieldForm() {
      const value = this.count[this.count.length - 1];
      this.count.push(value + 1);
    },
  },
};
</script>

<style scoped>
.container {
  margin: 20px 24px;
}

.title {
  margin-bottom: 25px;
}

.config-container {
  align-items: flex-start;
}

.data-fields {
  margin-left: 100px;
}

img {
  margin-top: 5px;
}

.width {
  width: 419px;
  justify-content: space-between;
}
</style>
