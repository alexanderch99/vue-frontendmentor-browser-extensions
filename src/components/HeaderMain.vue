<script setup lang="ts">
import type { Theme } from "@/types/theme";
import LogoMain from "./UI/LogoMain.vue";

const { theme } = defineProps<{
  theme: Theme;
}>();
</script>

<template>
  <header class="header">
    <div class="container">
      <div class="header__items">
        <LogoMain class="header__logo" />
        <div class="header__theme">
          <img
            v-if="theme == 'dark'"
            src="@/assets/icons/icon-sun.svg"
            alt="change theme"
            class="header__theme-icon"
            @click="$emit('setLightTheme')"
          />
          <img
            v-else
            src="@/assets/icons/icon-moon.svg"
            alt="change theme"
            class="header__theme-icon"
            @click="$emit('setDarkTheme')"
          />
        </div>
      </div>
    </div>
  </header>
</template>

<style scoped lang="scss">
.header {
  padding-top: 20px;

  &__theme {
    cursor: pointer;
  }

  &__theme-icon {
    width: 24px;
    height: 24px;
    padding: 8px;
    border-radius: 8px;
    user-select: none;
    background-color: var(--theme);
    box-sizing: content-box;
  }

  &__items {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 12px 16px;
    background-color: var(--bg-header);
    border-radius: 16px;
    border: 4px solid var(--border);
  }
}
</style>
