<script setup lang="ts">
import { computed } from 'vue'
import { currentCamera, currentMic } from '../state'
import { cameras, ensureDevicesListPermissions, microphones } from '../logic/recording'
import SelectList from './SelectList.vue'
import type { SelectionItem } from './types'

const camerasItems = computed<SelectionItem<string>[]>(() => [
  {
    value: 'none',
    display: 'None',
  },
  ...cameras.value.map(i => ({
    value: i.deviceId,
    display: i.label,
  })),
])

const microphonesItems = computed<SelectionItem<string>[]>(() => [
  {
    value: 'none',
    display: 'None',
  },
  ...microphones.value.map(i => ({
    value: i.deviceId,
    display: i.label,
  })),
])

ensureDevicesListPermissions()
</script>

<template>
  <div class="text-sm">
    <SelectList v-model="currentCamera" title="Camera" :items="camerasItems" />
    <SelectList v-model="currentMic" title="Microphone" :items="microphonesItems" />
  </div>
</template>
