<script setup lang="ts">
import { computed, onMounted, ref } from "vue";
import { useTheme } from "./composables/use-theme";
import ExtensionItem from "./components/ExtensionItem.vue";
import HeaderMain from "./components/HeaderMain.vue";
import ButtonMain from "./components/UI/ButtonMain.vue";

const themeController = useTheme();

const filterType = ref("all");

const data = ref([
  {
    logo: new URL("@/assets/icons/logo-devlens.svg", import.meta.url).href,
    name: "DevLens",
    description: "Quickly inspect page layouts and visualize element boundaries.",
    isActive: true,
  },
  {
    logo: new URL("@/assets/icons/logo-style-spy.svg", import.meta.url).href,
    name: "StyleSpy",
    description: "Instantly analyze and copy CSS from any webpage element.",
    isActive: true,
  },
  {
    logo: new URL("@/assets/icons/logo-speed-boost.svg", import.meta.url).href,
    name: "SpeedBoost",
    description: "Optimizes browser resource usage to accelerate page loading.",
    isActive: false,
  },
  {
    logo: new URL("@/assets/icons/logo-json-wizard.svg", import.meta.url).href,
    name: "JSONWizard",
    description: "Formats, validates, and prettifies JSON responses in-browser.",
    isActive: true,
  },
  {
    logo: new URL("@/assets/icons/logo-tab-master-pro.svg", import.meta.url).href,
    name: "TabMaster Pro",
    description: "Organizes browser tabs into groups and sessions.",
    isActive: true,
  },
  {
    logo: new URL("@/assets/icons/logo-viewport-buddy.svg", import.meta.url).href,
    name: "ViewportBuddy",
    description: "Simulates various screen resolutions directly within the browser.",
    isActive: false,
  },
  {
    logo: new URL("@/assets/icons/logo-markup-notes.svg", import.meta.url).href,
    name: "Markup Notes",
    description: "Enables annotation and notes directly onto webpages for collaborative debugging.",
    isActive: true,
  },
  {
    logo: new URL("@/assets/icons/logo-grid-guides.svg", import.meta.url).href,
    name: "GridGuides",
    description: "Overlay customizable grids and alignment guides on any webpage.",
    isActive: false,
  },
  {
    logo: new URL("@/assets/icons/logo-palette-picker.svg", import.meta.url).href,
    name: "Palette Picker",
    description: "Instantly extracts color palettes from any webpage.",
    isActive: true,
  },
  {
    logo: new URL("@/assets/icons/logo-link-checker.svg", import.meta.url).href,
    name: "LinkChecker",
    description: "Scans and highlights broken links on any page.",
    isActive: true,
  },
  {
    logo: new URL("@/assets/icons/logo-dom-snapshot.svg", import.meta.url).href,
    name: "DOM Snapshot",
    description: "Capture and export DOM structures quickly.",
    isActive: false,
  },
  {
    logo: new URL("@/assets/icons/logo-console-plus.svg", import.meta.url).href,
    name: "ConsolePlus",
    description: "Enhanced developer console with advanced filtering and logging.",
    isActive: true,
  },
]);

const filteredData = computed(() => {
  return filterType.value == "all"
    ? data.value
    : filterType.value == "active"
      ? data.value.filter((el) => el.isActive)
      : filterType.value == "inactive"
        ? data.value.filter((el) => !el.isActive)
        : data.value;
});

function toggle(name: string) {
  const index = data.value.findIndex((el) => el.name == name);
  if (data.value[index] != null) {
    data.value[index].isActive = !data.value[index].isActive;
  }
}

function removeExtension(name: string) {
  data.value = data.value.filter((el) => el.name != name);
}

onMounted(async () => {
  themeController.applyTheme(themeController.theme?.value);
});
</script>

<template>
  <HeaderMain
    :theme="themeController.theme?.value"
    @setLightTheme="themeController.applyTheme('light')"
    @setDarkTheme="themeController.applyTheme('dark')"
  />
  <main class="main">
    <div class="container">
      <div class="main__top">
        <h1 class="site-heading text text-700">Extensions List</h1>
        <div class="filter">
          <ButtonMain
            class="filter__button"
            :class="{ active: filterType == 'all' }"
            @click="filterType = 'all'"
            >All</ButtonMain
          >
          <ButtonMain
            class="filter__button"
            :class="{ active: filterType == 'active' }"
            @click="filterType = 'active'"
            >Active</ButtonMain
          >
          <ButtonMain
            class="filter__button"
            :class="{ active: filterType == 'inactive' }"
            @click="filterType = 'inactive'"
            >Inactive</ButtonMain
          >
        </div>
      </div>
      <div class="extensions">
        <ExtensionItem
          v-for="item in filteredData"
          :key="item.name"
          :logo="item.logo"
          :description="item.description"
          :is-active="item.isActive"
          :name="item.name"
          @toggle="toggle"
          @remove-extension="removeExtension"
        />
      </div>
    </div>
  </main>
</template>

<style scoped lang="scss">
.main {
  padding: 20px 0px 200px 0px;

  &__top {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 40px 0px;

    @media (max-width: 550px) {
      flex-direction: column;
      gap: 20px;
    }
  }
}

.extensions {
  display: grid;
  grid-template-columns: repeat(
    auto-fill,
    minmax(calc(calc(var(--site-max-width) - 52px) / 3), 1fr)
  );
  grid-auto-rows: 300px;
  gap: 16px;

  @media (max-width: 500px) {
    grid-template-columns: 1fr;
  }
}

.site-heading {
  font-size: 28px;
  line-height: 28px;
}

.filter {
  &__button {
    background-color: var(--filter-btn);
    margin-left: 8px;
    padding-inline: 16px;

    &.active {
      background-color: var(--color-red-400);
    }

    &:focus {
      outline: none;
    }
  }
}

:root[data-theme="light"] {
  & .filter__button.active {
    color: snow;
  }
}
</style>
