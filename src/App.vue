<template>
  <router-view />
</template>

<script>
export default {
  created() {
    this.$router.push({ name: "Dashboard" });
  },
};
</script>

<style>
*,
*::before,
*::after {
  top: 0;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

:root {
  --primary: #0a5dff;
  --success: #20c933;
  --warning: #ffa800;
  --error: #ff6e6e;
  --white: #fff;
  --lightGrey: #f7f7f7;
  --grey: #ebebeb;
  --darkGrey: #b2b2b2;
  --black: #000;
  --purple: #624ce0;
}

#app {
  font-family: "Inter", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #000;
  font-size: 15px;
}

.bold {
  font-weight: bold;
}

.none {
  display: none;
}

.semi-bold {
  font-weight: 500;
}

.cp {
  cursor: pointer;
}

.auto {
  margin: 0 auto;
}

.flex {
  display: flex;
  align-items: center;
}

.text-36 {
  font-size: 36px;
  letter-spacing: -2.5px;
}

.text-32 {
  font-size: 32px;
  letter-spacing: -2px;
}

.text-28 {
  font-size: 28px;
  letter-spacing: -2px;
}

.text-14 {
  font-size: 14px;
  letter-spacing: -0.5px;
}

.text-13 {
  font-size: 13px;
  letter-spacing: -0.5px;
}

.text-11 {
  font-size: 11px;
  letter-spacing: -0.5px;
}

.text-primary {
  color: var(--primary);
}

.text-success {
  color: var(--success);
}

.text-warning {
  color: var(--warning);
}

.text-error {
  color: var(--error);
}

.text-white {
  color: var(--white);
}

.text-light-grey {
  color: var(--lightGrey);
}

.text-grey {
  color: var(--grey);
}

.text-dark-grey {
  color: var(--darkGrey);
}

.text-black {
  color: var(--black);
}

.text-purple {
  color: var(--purple);
}

.bg-primary {
  background-color: var(--primary);
}

.bg-success {
  background-color: var(--success);
}

.bg-warning {
  background-color: var(--warning);
}

.bg-error {
  background-color: var(--error);
}

.bg-white {
  background-color: var(--white);
}

.bg-light-grey {
  background-color: var(--lightGrey);
}

.bg-grey {
  background-color: var(--grey);
}

.bg-dark-grey {
  background-color: var(--darkGrey);
}

.bg-black {
  background-color: var(--black);
}

.bg-purple {
  background-color: var(--purple);
}
</style>
