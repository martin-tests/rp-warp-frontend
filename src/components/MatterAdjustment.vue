<template>
  <div :style="style"></div>
</template>

<script setup lang="ts">
import { computed } from 'vue';
const props = defineProps({
  adjustment: Number
})

const style = computed(() => 'width: ' + Math.abs(props.adjustment as number) * 4 + 'rem; height: 1rem; display: inline-block; background-color: ' + (props.adjustment as number > 0 ? 'blue' : 'red') + ';')
</script>