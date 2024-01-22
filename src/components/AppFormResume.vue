<template>
  <div class="list">
    <div class="list-item" v-for="(item, index) in Object.keys(modelValue)">
      <p>{{ item }}:</p>
      <span>{{ modelValue[item] }}</span>
    </div>
    <div class="register-buttons">
      <app-button @click="$emit('back')" second>Voltar</app-button>
      <app-button @click="next()">Cadastrar</app-button>
    </div>
  </div>
</template>
<script setup>
import AppButton from "./AppButton.vue";
import { defineProps, defineEmits } from "vue";
const emits = defineEmits(["next", "back"]);

const props = defineProps({
  modelValue: {
    type: Object,
    default: {},
  },
});

const next = () => {
  emits("next", props.modelValue);
};
</script>
<style scoped lang="scss">
.list {
  &-item {
    display: flex;

    p {
      margin-right: 16px;
      text-transform: uppercase;
    }
  }
}
</style>
