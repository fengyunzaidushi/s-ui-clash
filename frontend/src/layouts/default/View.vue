<template>
  <v-main>
    <tms-banner />
    <router-view />
  </v-main>
</template>

<script lang="ts" setup>
import TmsBanner from '@/components/TmsBanner.vue'
</script>

<style>
.v-main {
  margin: 10px;
}
</style>