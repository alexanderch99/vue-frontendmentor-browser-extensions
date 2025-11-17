<script setup lang="ts"></script>

<template>
  <button class="button-main text text-s"><slot /></button>
</template>

<style scoped lang="scss">
.button-main {
  border: 2px solid var(--border);
  background-color: transparent;
  padding: 6px 12px;
  border-radius: 32px;
}
</style>
