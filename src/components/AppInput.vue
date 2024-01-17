<template>
  <div>
    <label :for="label">{{ label }}</label>
    <input
      :value="inputValue"
      v-bind="attrs"
      :name="name"
      v-maska:[maskOptions]
      @input="update"
      @keyup.enter="$emit('on-keyup-enter')"
    />
    <p v-if="errorMessage">{{ errorMessage }}</p>
  </div>
</template>
<script setup>
import { computed, defineEmits, defineProps, toRef, useAttrs } from "vue";
import { useVeeField } from "@/composables";
import { vMaska } from "maska";

const emits = defineEmits(["update:modelValue", "on-keyup-enter"]);
const attrs = useAttrs();

const props = defineProps({
  name: { type: String },
  modelValue: { type: [String, Number] },

  mask: {
    type: String,
    required: false,
    default: null,
  },

  label: {
    required: false,
    type: String,
  },

  rules: {
    type: String,
    default: undefined,
  },
});

const name = toRef(props, "name");

const {
  value: inputValue,
  errorMessage,
  handleBlur,
  handleChange,
  meta,
} = useVeeField({
  name,
  rules: props.rules,
  initialValue: props.modelValue,
});

const update = (el) => {
  handleChange(el.target.value);
  emits("update:modelValue", el.target.value);
};

const maskOptions = computed(() => {
  return {
    mask: props.mask,
    eager: true,
  };
});
</script>
<style scoped>
label {
  display: block;
  margin-bottom: 8px;
}

input,
textarea,
select {
  background: rgba(255, 255, 255, 0.1);
  border: none;
  font-size: 16px;
  height: auto;
  margin: 0;
  outline: 0;
  padding: 15px;
  width: 100%;
  background-color: #e8eeef;
  color: #8a97a0;
  box-shadow: 0 1px 0 rgba(0, 0, 0, 0.03) inset;
  margin-bottom: 30px;
}
p {
  color: red;
}
</style>
