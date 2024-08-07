<script setup lang="ts">
import type { HTMLAttributes } from "vue";
import { useVModel } from "@vueuse/core";
import { cn } from "@/6_shared/lib/utils";

const props = defineProps<{
  defaultValue?: string | number;
  modelValue?: string | number;
  class?: HTMLAttributes["class"];
}>();

const emits = defineEmits<{
  (e: "update:modelValue", payload: string | number): void;
}>();

const modelValue = useVModel(props, "modelValue", emits, {
  passive: true,
  defaultValue: props.defaultValue,
});
</script>

<template>
  <input
    v-model="modelValue"
    :class="
      cn(
        'flex', // Layout
        'h-10 w-full', // Size
        'rounded-md border border-input', // Border
        'bg-background px-3 py-2 text-sm', // Background, Padding, Text
        'ring-offset-background', // Ring offset
        'file:border-0 file:bg-transparent file:text-sm file:font-medium', // File
        'placeholder:text-muted-foreground', // Placeholder
        'focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2', // Focus
        'disabled:cursor-not-allowed disabled:opacity-50', // Disabled
        props.class
      )
    "
  />
</template>
