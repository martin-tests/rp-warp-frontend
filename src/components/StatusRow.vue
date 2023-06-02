<template>
  <tr v-if="status">
    <td>
      <DateTime :date="status.latestDT" />
    </td>
    <td>{{ status.secondsElapsed }}</td>
    <td>{{ status.flowRate }}</td>
    <td>{{ status.intermix }}</td>
    <td><MatterAdjustment :adjustment="status.matterAdjustment" /> {{ status.matterAdjustment }}</td>
    <td><MatterAdjustment :adjustment="status.antimatterAdjustment" /> {{ status.antimatterAdjustment }}</td>
  </tr>
</template>

<script setup lang="ts">
import DateTime from '@/components/DateTime.vue'
import MatterAdjustment from './MatterAdjustment.vue';

const props = defineProps({
  status: Object
})
</script>