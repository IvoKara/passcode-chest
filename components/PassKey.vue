<script setup lang="ts">

const emit = defineEmits<{
  check: [isValid: boolean]
}>()

const passkeyInputs = ref(['', '', '', '', '', ''])

// const code = ref<string[]>([])
const isValid = ref<boolean>()

function check() {
  // Check if all inputs are filled
  if (passkeyInputs.value.every(value => value !== '')) {
    // Perform validation
    if (passkeyInputs.value.join('') === '302671') {
      isValid.value = true;
    } else {
      isValid.value = false;
    }
    // Emit the validation result
    emit('check', isValid.value);
  }
}

function handleInput(index: number, event: Event): void {
  const input = (event.target as HTMLInputElement).value
  if (!Number.isNaN(Number(input)) && input !== '') {
    if (index < passkeyInputs.value.length) {
      const nextInput = document.querySelector(`#passkeyInput${index + 1}`) as HTMLInputElement
      if (nextInput)
        nextInput.focus()
        }
    }
}
</script>

<template>
    <div class="space-y-4">
        <ul class="flex items-center justify-center gap-2">
            <li v-for="index in 6" :key="`input${index}`">
                <input
                :id="`passkeyInput${index}`"
                v-model="passkeyInputs[index - 1]"
                :name="`input${index}`"
                maxlength="1"
                type="text"
                class="h-10 w-10 rounded-2 border-none text-center font-700 transition-all-300 focus-visible:outline-amber focus:outline-amber focus-visible:outline-offset-4 focus:outline-offset-4"
                pattern="[0-9]"
                title="Въведи число бачка"
                inputmode="numeric"
                @input="handleInput(index, $event)"
                >
            </li>
     </ul>
    <button bg="amber" class="rounded-2 px-5 py-3 font-bold" @click="check">
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
