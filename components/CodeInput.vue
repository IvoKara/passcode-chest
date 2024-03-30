<script setup lang="ts">
const emit = defineEmits<{
  check: [isValid: boolean]
}>()

const code = ref<number[]>([])
const isValid = ref<boolean>()

function check() {
  if (code.value.join('') === '302671')
    isValid.value = true
  else
    isValid.value = false

  emit('check', isValid.value)
}
</script>

<template>
  <div space-y-4>
    <ul flex items-center justify-center gap-2>
      <li v-for="i in 6" :key="`input${i}`">
        <input
          :id="`input${i}`"
          v-model.number="code[i - 1]" :name="`input${i}`" type="number" min="0" max="9"
          step="1"
          aspect-square rounded-2 border-none text-center font-700 transition-all-300
          focus-visible:outline-amber focus:outline-amber
          focus-visible:outline-offset-4
          focus:outline-offset-4
        >
      </li>
    </ul>
    <button bg="amber" rounded-2 px-5 py-3 font-bold @click="check">
      Пробвай кода
    </button>

    <small v-if="isValid !== undefined" block>
      <span v-if="isValid" class="animate-tada text-xl text-amber font-bold">
        Супер ти отвори съндъка!
      </span>
      <span v-else class="text-red-7 font-bold">
        Нем, това не е правилният код
      </span>
    </small>
  </div>
</template>

<style>
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

/* Firefox */
input[type='number'] {
  -moz-appearance: textfield;
}
</style>
