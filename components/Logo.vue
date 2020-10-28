<template>
  <div>
    <svg
      class="NuxtLogo"
      width="960"
      height="540"
      viewBox="0 0 960 540"
      xmlns="http://www.w3.org/2000/svg"
      @mousemove="touchMove($event)"
      @mouseup="touchEnd($event)"
      @mouseleave="touchEnd($event)"
    >
      <image :href="url" width="960" height="540" />
      <rect
        x="0"
        y="0"
        width="960"
        height="540"
        fill="transparent"
        stroke="black"
      />
      <text
        class="background2 text"
        :x="pos.x"
        :y="pos.y"
        :font-size="size"
        :stroke="color2"
        :stroke-width="stroke1 + stroke2"
        @mousedown="touchStart($event)"
      >
        {{ text }}
      </text>
      <text
        class="background text"
        :x="pos.x"
        :y="pos.y"
        :font-size="size"
        :stroke="color1"
        :stroke-width="stroke2"
        @mousedown="touchStart($event)"
      >
        {{ text }}
      </text>
      <text
        class="foreground text"
        :x="pos.x"
        :y="pos.y"
        :font-size="size"
        :stroke="color2"
        :fill="color1"
        :stroke-width="stroke1"
        @mousedown="touchStart($event)"
      >
        {{ text }}
      </text>
    </svg>
  </div>
</template>
<script lang="ts">
import { defineComponent, ref, reactive, computed } from '@vue/composition-api'

type Props = {
  text: string
  color1: string
  color2: string
  url: string
}

export default defineComponent({
  props: {
    text: {
      type: String,
      default: '',
    },
    color1: {
      type: String,
      default: '#ffffff',
    },
    color2: {
      type: String,
      default: '#000000',
    },
    url: {
      type: String,
      default: '',
    },
  },
  setup(props: Props) {
    const pos = reactive({
      x: 0,
      y: 100,
    })
    const size = ref(80)
    const stroke1 = ref(3)
    const stroke2 = ref(10)
    const text = computed(() => props.text)
    const color1 = computed(() => props.color1)
    const color2 = computed(() => props.color2)
    const isMouseDown = ref(false)
    const prevPos = reactive({
      x: pos.x,
      y: pos.y,
    })

    const touchStart = (e: MouseEvent) => {
      isMouseDown.value = true
      console.log('touch start:%d,%d', e.offsetX, e.offsetY)
      prevPos.x = e.offsetX
      prevPos.y = e.offsetY
    }
    const touchMove = (e: MouseEvent) => {
      // 押下中だったら
      if (isMouseDown.value) {
        // 前回座標との差分を算出
        const movedX = e.offsetX - prevPos.x
        const movedY = e.offsetY - prevPos.y

        pos.x += movedX
        pos.y += movedY

        // 前回のクリック座標を更新
        prevPos.x = e.offsetX
        prevPos.y = e.offsetY
      }
    }
    const touchEnd = () => {
      isMouseDown.value = false
      console.log('touch end')
    }

    return {
      color1,
      color2,
      stroke1,
      stroke2,
      text,
      pos,
      size,
      touchStart,
      touchMove,
      touchEnd,
    }
  },
})
</script>

<style>
.NuxtLogo {
  animation: 1s appear;
  margin: auto;
}
text {
  stroke-linejoin: round;
  font-family: 'けいふぉんと', sans-serif;
}
</style>
