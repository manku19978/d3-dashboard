<template>
  <div class="sidebar-wrapper" ref="sidebar" @mouseover="toggleSidebar" @mouseout="toggleSidebar">
    <div class="top">
      <div class="flex">
        <router-link class="icon-wrapper bg-black" to="/">
          <img :src="logoLight" alt="Rizzle Logo" />
        </router-link>

        <div class="icon-text">
          <p class="bold">Analytics</p>
          <p class="text-dark-grey text-13">by Rizzle</p>
        </div>
      </div>

      <div class="itemList">
        <side-bar-list-item v-for="item in items" :itemData="item" :key="item.label" />
      </div>
    </div>

    <user-bar />
  </div>
</template>

<script>
import SideBarListItem from "./SideBarListItem.vue";
import UserBar from "./UserBar.vue";
import logoLight from "@/assets/icons/logoLight.svg";
import logoWithoutText from "@/assets/icons/logoWithoutText.svg";

export default {
  components: { SideBarListItem, UserBar },

  data() {
    return {
      logoLight,
      logoWithoutText,
      items: [
        {
          label: "Home",
          imgDark: "userDark",
          imgLight: "userLight",
          path: "/dashboard",
        },
        {
          label: "About",
          imgDark: "aboutDark",
          imgLight: "aboutLight",
          path: "/about",
        },
        {
          label: "Config",
          imgDark: "configDark",
          imgLight: "configLight",
          path: "/config",
        },
        {
          label: "Setting",
          imgDark: "settingDark",
          imgLight: "settingLight",
          path: "/settings",
        },
      ],
    };
  },
};
</script>

<style scoped>
.sidebar-wrapper {
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 300px;
  box-shadow: inset -1px 0px 0px var(--grey);
}

.top {
  padding: 20px 16px;
}

.icon-wrapper {
  margin-right: 12px;
  padding: 10px;
  border-radius: 6px;
}

p {
  margin-bottom: 1px;
}

.itemList {
  margin-top: 36px;
}

.bottom {
  bottom: 0;
  position: relative;
}

.justify {
  justify-content: center;
}
</style>
