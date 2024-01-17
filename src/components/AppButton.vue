<template>
  <button :class="color"><slot></slot></button>
</template>
<script setup>
import { computed } from "vue";

const props = defineProps({
  second: { type: Boolean, default: false },
});

const color = computed(() => {
  if (props.second) {
    return "second";
  } else {
    return "primary";
  }
});
</script>
<style scoped>
button {
  padding: 19px 39px 18px 39px;
  font-size: 18px;
  text-align: center;
  font-style: normal;
  border-radius: 5px;
  width: 100%;
  border-width: 1px 1px 3px;
  box-shadow: 0 -1px 0 rgba(255, 255, 255, 0.1) inset;
  margin-bottom: 10px;
  margin-top: 16px;
}

.primary {
  background-color: rgb(255, 196, 0);
  color: #fff;
}
.second {
  background-color: #fff;
  color: black;
}
</style>
