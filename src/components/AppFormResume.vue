<template>
  <div v-for="item in Object.keys(modelValue)">
    <p>{{ item }}</p>
    <span></span>
  </div>

  {{ modelValue }}
</template>
<script setup>
import { defineProps } from 'vue';
const props = defineProps({
  modelValue: {
    type: Object,
    default: {},
  },
});
</script>
