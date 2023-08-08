<template>
  <div class="login-wrapper flex bg-black">
    <div class="container">
      <img class="auto logo-img" :src="LogoLight" alt="Rizzle Logo" />

      <div class="login-card-container flex">
        <div class="card bg-white">
          <p class="hero-txt text-36 bold">Welcome to Rizzle Analytics</p>
          <ui-button :iconUrl="GoogleLogo" :handler="login" :styleType="BUTTON_WHITE">
            Sign in with Google
          </ui-button>
        </div>

        <div class="card bg-purple flex">
          <img class="auto" :src="LoginBanner" alt="Login Banner" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import UiButton from "@/ui/UiButton";
import { BUTTON_WHITE } from "@/utils/constants";
import LogoLight from "@/assets/icons/logoLight.svg";
import LoginBanner from "@/assets/images/loginBanner.svg";
import GoogleLogo from "@/assets/icons/googleLogo.svg";

export default {
  components: { UiButton },

  data() {
    return {
      LogoLight,
      LoginBanner,
      GoogleLogo,
      BUTTON_WHITE,
    };
  },

  methods: {
    login() {
      this.$router.push({ name: "Dashboard" });
    },
  },
};
</script>

<style scoped>
.login-wrapper {
  height: 100vh;
  width: 100vw;
  position: fixed;
  top: 0;
  justify-content: center;
}

.logo-img {
  display: block;
  margin-bottom: 50px;
}

.login-card-container {
  width: 63.8vw;
  height: 66.6vh;
  align-items: stretch;
}

.card {
  width: 31.9vw;
}

.card:first-child {
  border-radius: 6px 0 0 6px;
  padding: 44px;
}

.card:last-child {
  border-radius: 0 6px 6px 0;
}

.hero-txt {
  margin-bottom: 14px;
}
</style>
