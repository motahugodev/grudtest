<template>
  <Form class="register" @submit="next">
    <app-input
      label="Sua senha"
      name="senha"
      rules="required"
      type="password"
      v-model="form.password"
    />
    <div class="register-buttons">
      <app-button @click="$emit('back')" second>Voltar</app-button>
      <app-button type="submit">Salvar</app-button>
    </div>
  </Form>
</template>
<script setup>
import AppInput from "@/components/AppInput.vue";
import AppButton from "./AppButton.vue";
import { Form } from "vee-validate";
import { defineProps, defineEmits, ref } from "vue";

const emits = defineEmits(["next", "back"]);

const props = defineProps({
  modelValue: {
    type: Object,
    default: {},
  },
});

const form = ref(props.modelValue);

const next = (value) => {
  emits("next", form.value);
};
</script>
<style scoped lang="scss">
.register {
  &-buttons {
    display: flex;
    justify-content: center;
  }
}
</style>
