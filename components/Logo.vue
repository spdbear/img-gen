<template>
  <svg
    class="NuxtLogo"
    width="960"
    height="540"
    viewBox="0 0 960 540"
    xmlns="http://www.w3.org/2000/svg">
    <text class="background2 text" :x="pos.x" :y="pos.y" :font-size="size" :stroke="color2" :stroke-width="stroke1+stroke2">{{text}}</text>
    <text class="background text" :x="pos.x" :y="pos.y" :font-size="size" :stroke="color1" :stroke-width="stroke2">{{text}}</text>
    <text class="foreground text" :x="pos.x" :y="pos.y" :font-size="size" :stroke="color2" :fill="color1" :stroke-width="stroke1">{{text}}</text>
    <rect x="0" y="0" width="960" height="540" fill="transparent" stroke="black"/>
  </svg>
</template>
<script lang="ts">
import { defineComponent, ref, reactive, computed } from '@vue/composition-api'

type Props = {
  text: string
}

export default defineComponent({
  props: {
    text: {
      type: String,
      default: ""
    }
  },
  setup(props: Props) {
    const pos = reactive({
      x: 0,
      y: 100
    })
    const size = ref(80)
    const color1 = ref("rgb(255,255,255)")
    const color2 = ref("rgb(0,0,0)")
    const stroke1 = ref(3)
    const stroke2 = ref(10)
    const text = computed(()=>props.text)
    return {
      color1,
      color2,
      stroke1,
      stroke2,
      text,
      pos,
      size
    }
  }
})
</script>

<style>
.NuxtLogo {
  animation: 1s appear;
  margin: auto;
}
text {
  stroke-linejoin: round;
  font-family: 'けいふぉんと', sans-serif
}
</style>
