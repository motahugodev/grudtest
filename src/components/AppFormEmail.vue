<template>
  <Form @submit="next" class="register">
    <app-input
      label="Endereço de e-mail"
      name="email"
      type="email"
      rules="required|email"
      v-model="form.email"
    />
    <div class="register-checkbox">
      <app-checkbox
        v-for="item in options"
        :name="item.name"
        :value="item.name"
        v-model="form.tipo"
        :label="item.label"
      ></app-checkbox>
    </div>
    <app-button type="submit">Continuar</app-button>
  </Form>
</template>
<script setup>
import AppInput from "@/components/AppInput.vue";
import AppCheckbox from "./AppCheckbox.vue";
import AppButton from "./AppButton.vue";
import { Form } from "vee-validate";
import { ref, defineProps, defineEmits } from "vue";

const emit = defineEmits(["next"]);
const props = defineProps({
  modelValue: {
    type: Object,
    default: {},
  },
});

const options = ref([
  { name: "PJ", label: "Pessoa Juridica" },
  { name: "PF", label: "Pessoa Fisica" },
]);

const form = ref(props.modelValue);

const next = (value) => {
  console.log("🚀 ~ next ~ value:", value);
  console.log(form.value);
  emit("next", form.value);
};
</script>
<style scoped lang="scss">
.register {
  &-checkbox {
    display: flex;
    justify-content: center;
  }
}
</style>
