<template>
  <Form @submit="next" class="register">
    <app-input
      label="Razão social"
      name="razao-social"
      type="text"
      rules="required"
      v-model="form.rezao_social"
    />
    <app-input
      label="CNPJ"
      name="cpnj"
      type="text"
      mask="##.###.###/####-##"
      rules="required"
      v-model="form.cnpj"
    />
    <app-input
      label="Data abertura"
      name="data-abertura"
      type="date"
      rules="required"
      v-model="form.data_abertura"
    />
    <app-input
      label="Telefone"
      name="telefone"
      type="tel"
      mask="(##) #####-####"
      rules="required"
      v-model="form.telefone"
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

const emit = defineEmits(["next"]);

const props = defineProps({
  modelValue: {
    type: Object,
    default: {},
  },
});

const form = ref(props.modelValue);

const next = (value) => {
  emit("next", form.value);
};
</script>
<style scoped lang="scss">
.register {
  &-buttons {
    display: flex;
    justify-content: center;
  }
  &-checkbox {
    display: flex;
    justify-content: center;
  }
}
</style>
