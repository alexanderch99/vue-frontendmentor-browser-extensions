<script setup lang="ts">
import ToggleMain from "./ToggleMain.vue";
import ButtonMain from "./UI/ButtonMain.vue";

const { logo, name, description, isActive } = defineProps<{
  logo: string;
  name: string;
  description: string;
  isActive: boolean;
}>();

const emit = defineEmits<{
  toggle: [name: string];
  removeExtension: [name: string];
}>();

function removeExtension() {
  emit("removeExtension", name);
}
</script>

<template>
  <div class="extension">
    <div class="extension__side extension__side-top">
      <img :src="logo" alt="logo" class="extension__logo" />
      <div class="extension__text text">
        <h2 class="extension__name text-700">{{ name }}</h2>
        <p class="extension__description text-s">{{ description }}</p>
      </div>
    </div>
    <div class="extension__side extension__side-bottom">
      <ButtonMain @click="removeExtension">Remove</ButtonMain>
      <ToggleMain :active="isActive" @toggle="$emit('toggle', name)" />
    </div>
  </div>
</template>

<style scoped lang="scss">
.extension {
  display: flex;
  flex-direction: column;
  padding: 16px;
  border-radius: 16px;
  background-color: var(--bg-ext);
  user-select: none;
  height: 100%;
  border: 4px solid var(--border);

  &__logo {
    width: 64px;
    height: 64px;
  }

  &__text {
    user-select: text;
  }

  &__name {
    letter-spacing: 0.5px;
  }

  &__description {
    color: var(--text-secondary);
    margin-top: 16px;
    line-height: 24px;
  }

  &__side {
    display: flex;

    &-top {
      gap: 16px;
    }

    &-bottom {
      justify-content: space-between;
      align-items: center;
      margin-top: auto;
    }
  }
}
</style>
