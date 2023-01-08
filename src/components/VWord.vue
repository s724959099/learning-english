<template>
  <span :class="{ 'text-gray': !active }" class="mr-1 pointer">{{ word }}</span>
</template>
<script lang="ts" setup>
defineProps<{
  word: string;
  active?: boolean;
}>();
</script>
<style>
.text-gray {
  color: #9e9e9e;
}

.pointer {
  cursor: pointer;
}
</style>
