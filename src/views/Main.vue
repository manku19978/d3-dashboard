<template>
  <side-bar />

  <div class="main-container" ref="main">
    <router-view></router-view>
  </div>
</template>

<script>
import SideBar from "@/components/sideBar/SideBar";

export default {
  components: { SideBar },
};
</script>

<style scoped>
.main-container {
  width: calc(100vw - 300px);
  margin-left: 300px;
  max-width: 1380px;
}
</style>
