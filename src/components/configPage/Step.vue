<template>
  <div class="step">
    <div class="flex semi-bold">
      <div class="step-number text-">{{ n }}</div>
      <div class="name">{{ name }}</div>
    </div>
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "Step",
  props: ["n", "name"],
};
</script>

<style scoped>
.step:not(:last-of-type) {
  background-image: linear-gradient(
    90deg,
    transparent 0,
    transparent 15px,
    var(--darkGrey) 0,
    var(--darkGrey) 17px,
    transparent 0,
    transparent
  );
  background-repeat: no-repeat;
  background-position: left 32px;
}

.step-number {
  border-radius: 50%;
  width: 32px;
  height: 32px;
  border: 2px solid var(--black);
  background: var(--black);
  color: var(--white);
  line-height: 30px;
  text-align: center;
  margin-right: 10px;
}

.content {
  margin-left: 35px;
  padding: 10px 15px 20px 15px;
}
</style>
