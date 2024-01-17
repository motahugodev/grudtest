<template>
  <div class="checkbox">
    <label :for="name">{{ label }}</label>
    <input
      :value="value"
      v-bind="attrs"
      :name="name"
      :id="name"
      type="radio"
      @change="update"
    />
    <span v-if="errorMessage">{{ errorMessage }}</span>
  </div>
</template>
<script setup>
import { defineEmits, defineProps, toRef, useAttrs } from "vue";
import { useVeeField } from "@/composables";

const emits = defineEmits(["update:modelValue"]);
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

  value: {
    required: false,
    type: String,
  },

  rules: {
    type: String,
    default: undefined,
  },
});

const { handleChange, errorMessage } = useVeeField({
  name: props.name,
  rules: props.rules,
  initialValue: props.modelValue,
});

const update = (el) => {
  console.log("🚀 ~ update ~ el:", el);

  handleChange(el.target.value);
  emits("update:modelValue", el.target.value);
};
</script>
<style scoped>
.checkbox {
  display: flex;
  flex-direction: row-reverse;

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
    width: 50px;
    background-color: #e8eeef;
    color: #8a97a0;
    box-shadow: 0 1px 0 rgba(0, 0, 0, 0.03) inset;
    margin-bottom: 30px;
  }

  input[type="radio"],
  input[type="checkbox"] {
    margin: 0 4px 8px 0;
    flex: 1;
  }
}
</style>
