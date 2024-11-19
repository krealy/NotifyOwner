<template>
  <input
    class="input"
    :type="type"
    :placeholder="placeholder"
    :value="modelValue"
    @input="updateValue"
  />
</template>

<script lang="ts" setup>
import { defineProps, defineEmits } from "vue";

// 定义 Props
defineProps({
  type: {
    type: String,
    default: "text",
  },
  placeholder: {
    type: String,
    default: "请输入内容",
  },
  modelValue: {
    type: String,
    required: true,
  },
});

// 定义事件
const emit = defineEmits(["update:modelValue"]);

// 输入时更新值
function updateValue(event: Event) {
  const target = event.target as HTMLInputElement;
  emit("update:modelValue", target.value);
}
</script>

<style scoped>
.input {
  width: 100%;
  max-width: 100%;
  padding: 13px 14px;
  border: 1px solid #ccc;
  font-size: 14px;
  font-weight: 700;
  font-family: "Microsoft soft";
}
.input:focus {
  border-color: #66afe9;
  outline: none;
  box-shadow: 0 0 8px rgba(102, 175, 233, 0.6);
}
</style>