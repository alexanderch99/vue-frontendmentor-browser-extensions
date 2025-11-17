<script setup lang="ts">
const { active } = defineProps<{
  active: boolean;
}>();
</script>

<template>
  <div
    class="toggle"
    :style="active && { backgroundColor: 'var(--color-red-400)' }"
    @click="$emit('toggle')"
  >
    <div class="toggle__inside" :style="active && { transform: 'translateX(32px)' }"></div>
  </div>
</template>

<style scoped lang="scss">
.toggle {
  position: relative;
  width: 56px;
  height: 24px;
  background-color: var(--color-neutral-600);
  border-radius: 32px;
  padding: 4px;
  box-sizing: content-box;
  cursor: pointer;
  transition: background-color 0.3s ease;

  &__inside {
    position: absolute;
    top: 4px;
    left: 4px;
    background-color: white;
    width: 24px;
    height: 24px;
    border-radius: 50%;
    transition: transform 0.3s ease;
  }
}
</style>
