<template>
  <Form @submit="next" class="register">
    <app-input
      label="Nome"
      name="name"
      type="text"
      rules="required"
      v-model="form.nome"
    />
    <app-input
      label="CPF"
      name="cpf"
      type="text"
      mask="###.###.###-##"
      rules="required"
      v-model="form.cpf"
    />
    <app-input
      label="Data de Nascimento"
      name="nascimento"
      type="date"
      rules="required"
      v-model="form.data_nascimento"
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
      <app-button type="submit">Continuar</app-button>
    </div>
  </Form>
</template>
<script setup>
import AppInput from "@/components/AppInput.vue";
import AppButton from "./AppButton.vue";
import { Form } from "vee-validate";
import { defineProps, defineEmits, ref } from "vue";

const emits = defineEmits(["next"]);

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
  &-checkbox {
    display: flex;
    justify-content: center;
  }
}
</style>
