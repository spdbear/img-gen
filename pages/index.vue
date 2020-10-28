<template>
  <div class="container">
    <h1 class="title">be-youtuber</h1>
    <div>
      <Logo
        :text="text"
        :size="size"
        :color1="color1"
        :color2="color2"
        :url="url"
      />
    </div>
    <div>
      <input v-model="text" placeholder="ここにテキストを入力" />
      <input v-model="size" type="range" value="80" min="20" max="200" />{{
        size
      }}
      <input v-model="color1" type="color" value="#ffffff" />色1
      <input v-model="color2" type="color" value="#000000" />色2
      <input
        type="file"
        accept="image/jpg,image/png,image/gif"
        @change="handleInputImage"
      />
    </div>
    <div>
      <button @click="saveImage">画像を保存</button>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import Logo from '~/components/Logo.vue'
const ssap = require('save-svg-as-png')
type HTMLInputEvent = Event & {
  target: HTMLInputElement & EventTarget
}

export default Vue.extend({
  components: {
    Logo,
  },
  data() {
    return {
      text: '',
      color1: '#ffffff',
      color2: '#000000',
      url: '',
      size: 80,
    }
  },
  methods: {
    handleInputImage(e: HTMLInputEvent) {
      if (!e.target.files?.length) {
        return
      }
      const file = e.target.files[0]
      this.url = window.URL.createObjectURL(file)
    },
    saveImage() {
      ssap.saveSvgAsPng(document.getElementById('svg'), 'download.png')
    },
  },
})
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'けいふぉんと', sans-serif;
  display: block;
  font-weight: 600;
  font-size: 80px;
  margin: 10px;
  color: #35495e;
}
</style>
