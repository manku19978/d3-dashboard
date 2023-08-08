<template>
  <div class="container flex" ref="userBar">
    <div class="flex">
      <div class="dp-container">
        <img :src="DP" alt="User DP" />
      </div>
      <p>Mayank Singh</p>
    </div>
    <div class="dots flex cp">
      <img :src="dots" />
    </div>
  </div>
</template>

<script>
import DP from "@/assets/images/dp.png";
import dots from "@/assets/icons/dots.svg";

export default {
  data() {
    return {
      DP,
      dots,
    };
  },
};
</script>

<style scoped>
.container {
  height: 64px;
  border-top: 1px solid var(--grey);
  padding: 12px 16px;
  position: fixed;
  top: calc(100vh - 64px);
  width: 300px;
  justify-content: space-between;
}

.dp-container {
  border-radius: 100%;
  width: 40px;
  height: 40px;
  margin-right: 12px;
}

.dots {
  border: 1px solid var(--grey);
  border-radius: 3px;
  height: 32px;
  width: 32px;
  justify-content: center;
}
</style>
