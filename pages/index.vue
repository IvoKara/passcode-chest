<script setup lang="ts">
const open = ref<boolean>()
</script>

<template>
  <div>
    <SplineCanvas
      loading-text="Зареждам, един момент..."
      url="https://prod.spline.design/1r0Gndnxe2QP6AhR/scene.splinecode"
      mx-auto max-w-250
      :win="open"
    />
    <CodeInput px-10 @check="isValid => open = isValid" />
  </div>
</template>
