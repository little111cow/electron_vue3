<template>
  <div style="height: 100vh; widh: 100vw">
    <TitleBar style="height: 30.5px; position: fixed"></TitleBar>
    <router-view v-slot="{ Component }" style="margin-top: 30.5px">
      <component :is="Component" />
    </router-view>
  </div>
</template>

<script setup lang="ts">
import TitleBar from "@renderer/components/title-bar/title-bar.vue";
</script>

<style></style>
