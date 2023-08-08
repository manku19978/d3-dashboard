<template>
  <router-link class="container flex text-black" :to="itemData.path" active-class="active">
    <img :src="require(`@/assets/icons/${imgSelect}.svg`)" />
    <p class="semi-bold">{{ itemData.label }}</p>
  </router-link>
</template>

<script>
export default {
  props: ["itemData"],

  computed: {
    imgSelect() {
      return this.$route.path.includes(this.itemData.path)
        ? this.itemData.imgLight
        : this.itemData.imgDark;
    },
  },
};
</script>

<style scoped>
.container {
  padding: 10px 12px;
  margin-bottom: 4px;
  text-decoration: none;
}

img {
  margin-right: 12px;
  height: 20px;
  width: 20px;
}

.container:hover {
  background-color: var(--grey);
  border-radius: 4px;
}

.active,
.active:hover {
  background-color: var(--black);
  border-radius: 3px;
  color: var(--white);
}
</style>
