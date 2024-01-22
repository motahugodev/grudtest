<script setup>
import AppFormEmail from "@/components/AppFormEmail.vue";
import AppFormPF from "@/components/AppFormPF.vue";
import AppFormPJ from "@/components/AppFormPJ.vue";
import AppFormPassword from "@/components/AppFormPassword.vue";
import AppFormResume from "@/components/AppFormResume.vue";
import { shallowRef, markRaw, ref } from "vue";

const components = markRaw({
  AppFormEmail,
  AppFormPF,
  AppFormPJ,
  AppFormPassword,
  AppFormResume,
});

const step = ref(0);
const steps = shallowRef([
  { title: "Seja bem vindo(a)", value: {}, component: components.AppFormEmail },
  {
    title: "Senha de acesso",
    value: {},
    component: components.AppFormPassword,
  },
  {
    title: "Revisa suas informações",
    value: {},
    component: components.AppFormResume,
  },
]);

const next = (value) => {
  console.log("🚀 ~ next ~ value:", value);

  const newStep = step.value;
  console.log("🚀 ~ next ~ newStep:", newStep);

  switch (newStep) {
    case 0:
      steps.value[0].value = value;

      if (value.tipo == "PF") {
        steps.value.splice(1, 0, {
          title: "Pessoa fisica",
          value: {},
          component: components.AppFormPF,
        });
      } else {
        steps.value.splice(1, 0, {
          title: "Pessoa Juridica",
          value: {},
          component: components.AppFormPJ,
        });
      }
      step.value = 1;

      break;

    case 1:
      steps.value[1].value = value;
      step.value = 2;

      break;

    case 2:
      step.value = 3;
      steps.value[2].value = value;

      const concat_value = Object.assign(
        steps.value[0].value,
        steps.value[1].value,
        steps.value[2].value
      );

      steps.value[3].value = concat_value;
      break;

    case 3:
      requestSave(steps.value[3].value);
      break;

    default:
      break;
  }
};

const requestSave = (body) => {
  const options = {
    method: "POST",
    body: Object.keys(body)
      .map((k) => `${encodeURIComponent(k)}=${encodeURIComponent(body[k])}`)
      .join("&"),
  };
  fetch("api/registration", options)
    .then((response) => response.text())
    .then((texto) => console.log(texto))
    .catch((err) => console.log(err.message));
};
const back = () => {
  step.value = step.value - 1;
};
</script>

<template>
  <div class="main">
    <div class="main-container">
      <div class="main-container-header">
        <span>Etapa {{ step + 1 }} de 4</span>
        <h1>{{ steps[step].title }}</h1>
      </div>
      <component
        @next="next"
        @back="back"
        v-model="steps[step].value"
        :is="steps[step].component"
      ></component>
    </div>
  </div>
</template>
<style scoped lang="scss">
.main {
  display: flex;
  justify-content: center;

  &-container {
    width: 450px;
    padding: 20px 2px 20px 2px;

    &-header {
      padding-bottom: 26px;
    }
  }
}
</style>
