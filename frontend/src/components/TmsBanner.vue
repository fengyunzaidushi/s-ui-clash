<template>
  <v-alert
    v-if="show"
    class="tms-banner mb-2"
    type="info"
    variant="tonal"
    density="compact"
    closable
    @click:close="dismiss"
  >
    {{ $t('tmsBanner.text') }}
    <a :href="TMS_URL" target="_blank" rel="noopener noreferrer">{{ $t('tmsBanner.link') }}</a>
  </v-alert>
</template>

<script lang="ts" setup>
import { ref } from 'vue'

const TMS_URL = 'https://3yuedaohang.com/tms-download.html?ref=sui'
const KEY = 'tmsBannerDismissed'

const readDismissed = (): boolean => {
  try {
    return localStorage.getItem(KEY) === '1'
  } catch {
    return false
  }
}

const show = ref(!readDismissed())

const dismiss = () => {
  show.value = false
  try {
    localStorage.setItem(KEY, '1')
  } catch {
    // storage unavailable: hide for this session only
  }
}
</script>
