<template>
  <span>{{ formattedDateTime() }}</span>
</template>

<script setup lang="ts">
const props = defineProps({
  date: String
})
const formattedDateTime = () => {
  const date = new Date(props.date as string)
  return date.toLocaleDateString() + ' ' + date.toLocaleTimeString()
}
</script>