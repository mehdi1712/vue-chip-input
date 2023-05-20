<script setup lang="ts">
import { defineProps, reactive, ref } from 'vue'

const props = defineProps({
  chips: {
    type: Array as () => string[],
    default: () => [],
  },
})
const emit = defineEmits(['selectInput'])

const chips = reactive(props.chips)
const currentInput = ref('')

function saveChip() {
  if (currentInput.value) {
    chips.push(currentInput.value)
    emit('selectInput', currentInput.value)
    currentInput.value = ''
  }
}

function deleteChip(index: number) {
  chips.splice(index, 1)
}

function backspaceDelete() {
  console.log("slm");

  if (!currentInput.value)
    chips.splice(-1, 1)
}
</script>


<template>
  <div class="chip-container  border-black border-1 rounded-10px flex py-2 px-3 max-full flex-wrap gap-2">
    <div v-for="(chip, i) of chips" :key="i" class="flex bg-surfaceVariant rounded-25px py-3px px-4 justify-center items-center">
      <svg @click="deleteChip(i)" class="h-2 w-2 cursor-pointer" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
        stroke="currentColor" >
        <path stroke-linecap="round" stroke-linejoin="round"
          d="M9.75 9.75l4.5 4.5m0-4.5l-4.5 4.5M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
      </svg>
      <span class="text-gray-70 text-13px whitespace-nowrap w-fit">{{ chip }}</span>
    </div>
    <input v-model.trim="currentInput" class="chips-input !text-xs !max-w-170px !min-w-20px"
      :class="chips.length && '!border-r-1 !border-black !pr-1'" @keypress.enter.prevent="saveChip"
      @keyup.delete="backspaceDelete">
  </div>
</template>

<style lang="css" scoped></style>
