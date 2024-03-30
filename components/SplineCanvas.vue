<script setup lang="ts">
import { Application } from '@splinetool/runtime'
import { breakpointsTailwind } from '@vueuse/core'

const props = withDefaults(defineProps<{
  url: string
  loadingText?: string
  win?: boolean
}>(), {
  win: false,
})

const breakpoints = useBreakpoints(breakpointsTailwind)

const canvas = ref<HTMLCanvasElement | null>()

const loaded = ref(false)
const spline = ref<Application | null>(null)

onMounted(async () => {
  const app = new Application(canvas.value)
  await app.load(props.url)
  loaded.value = true

  if (breakpoints.isSmallerOrEqual('md'))
    canvas.value?.setAttribute('width', '500')

  spline.value = app
})

whenever(() => props.win, () => {
  spline.value?.setVariable('isOpen', true)
})
</script>

<template>
  <div
    min-h-40 :class="{
      relative: !loaded,
    }"
  >
    <canvas ref="canvas" mx-auto />
    <div v-if="!loaded" absolute inset-0 h-full w-full flex flex-col items-center justify-center gap-2>
      <div i-carbon:circle-dash animate-1s h-8 w-8 animate-spin bg-black />
      <p>{{ loadingText }}</p>
    </div>
  </div>
  <!-- <div border="1 blue" grid place-items-center>
    <spline-viewer
      :url border="1 red"
    />

  </div> -->
</template>
