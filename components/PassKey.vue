<script setup lang="ts">
const passkeyInputs = ref(['', '', '', '', '', ''])

function handleInput(index: number, event: Event): void {
  const input = (event.target as HTMLInputElement).value
  if (!Number.isNaN(Number(input)) && input !== '') {
    if (index < passkeyInputs.value.length - 1) {
      const nextInput = document.querySelector(`#passkeyInput${index + 1}`) as HTMLInputElement
      if (nextInput)
        nextInput.focus()
    }
    else {
      // проверява дали са попълнени
      if (passkeyInputs.value.every(value => value !== ''))
        submitForm()
    }
  }
}

function submitForm(): void {
  const form = document.querySelector('form') as HTMLFormElement
  if (form)
    form.submit()
}
</script>

<template>
  <form @submit.prevent="submitForm">
    <div class="mx-a w-fit flex">
      <input
        v-for="(input, index) in passkeyInputs"
        :id="`passkeyInput${index}`"
        :key="index"
        v-model="passkeyInputs[index]"
        maxlength="1"
        type="text"
        class="mx-2 h-12 w-12 w-3rem border border-gray-300 rounded text-center focus:border-blue-500 focus:outline-none"
        pattern="[0-9]"
        title="Въведи число бачка"
        inputmode="numeric"
        @input="handleInput(index, $event)"
      >
    </div>
    <button type="submit" class="hidden">
      Submit
    </button>
  </form>
</template>
