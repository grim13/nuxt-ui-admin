<template>
  <div class="flex">
    <Sidebar />
    <div class="flex-1">
      <slot />
    </div>
  </div>
</template>

<script setup>
  import Sidebar from '~/components/Sidebar.vue';
</script>

<style lang="scss" scoped></style>