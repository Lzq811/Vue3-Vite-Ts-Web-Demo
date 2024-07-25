<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import { onMounted } from 'vue'
import Login from './views/Login.vue'

onMounted(() => {
  InitLayout()
})

const InitLayout = () => {
  Adaptive()
  window.onresize = () => {
    Adaptive()
  }
}

const Adaptive = () => {
  /**
   * 根据UI给的规范定义
   * 主标题 20
   * 标题 18
   * 小标题 16
   * 正文 14
   * 辅助文字 12
   * 那默认使用正文文字 14
   * 在UI是 1920 * 1080的基础上进行计算
   * ! 如果UI基础不是 1920 的话还需要重新计算
   */
  const htmlEl: HTMLBaseElement | any = document.querySelector('html')
  const screenWidth = htmlEl.clientWidth
  if (screenWidth <= 1280) {
    // 窗口小于 1280 出现滚动条，页面大小不再缩放
    const miniSize = 14 / (1920 / 1280) //  ≈ 9.33
    htmlEl.style.fontSize = `${miniSize}px`
  } else if (screenWidth > 1920) {
    // 窗口大于 1 出现滚动条，页面大小不再缩放
    const maxSize = 20 / (1920 / 1280) //  ≈ 9.33
    htmlEl.style.fontSize = `${maxSize}px`
  } else {
    const baseMultiple = 1920 / 14 // ≈ 137.14
    htmlEl.style.fontSize = `${screenWidth / baseMultiple}px`
  }
}
</script>

<template>
  <div class="layout-container">
    <!-- <h1 class="level-title">hello world !!!</h1>
    <div class="son-box">子盒子</div> -->
    <Login />
  </div>
</template>

<style scoped>
.layout-container {
  height: 100%;
  overflow-x: auto;
  overflow-y: scroll;
}
.level-title {
  font-size: 28px;
  font-weight: 700;
}
.son-box {
  height: 150%;
  background-color: #e4393c;
}
</style>
