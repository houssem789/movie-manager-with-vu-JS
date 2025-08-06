<template>

<label class="checkbox-line">
        <input
        type="checkbox" 
        :checked="modelValue"
        @change="$emit('update:modelValue', $event.target.checked)"

         />
        {{ label }}
    </label>

</template>




<script setup>

const props = defineProps({
    label: String,
    modelValue: Boolean

})

console.log(props.label)
console.log(props.modelValue)
const emit = defineEmits(['update:modelValue'])

</script>


<style>

.checkbox-line {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
  font-size: 0.9rem;
  color: #555;
}
</style>