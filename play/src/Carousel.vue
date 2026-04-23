<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Carousel Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-carousel
        data-testid="carousel-basic"
        height="150px"
        :autoplay="false"
        style="width: 400px"
      >
        <el-carousel-item v-for="item in slides" :key="item.id">
          <div class="slide" :style="{ background: item.color }">{{ item.label }}</div>
        </el-carousel-item>
      </el-carousel>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (change slide)</h3>
      <el-carousel
        data-testid="carousel-interact"
        height="150px"
        :autoplay="false"
        style="width: 400px"
        @change="onChange"
      >
        <el-carousel-item v-for="item in slides" :key="item.id">
          <div class="slide" :style="{ background: item.color }">{{ item.label }}</div>
        </el-carousel-item>
      </el-carousel>
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ activeIndex }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (autoplay toggle)</h3>
      <el-button data-testid="carousel-toggle-autoplay" @click="autoplay = !autoplay">
        Toggle autoplay: <span data-testid="state-indicator">{{ autoplay ? 'on-2000ms' : 'off-5000ms' }}</span>
      </el-button>
      <el-carousel
        data-testid="carousel-state-target"
        height="150px"
        :autoplay="autoplay"
        :interval="autoplay ? 2000 : 5000"
        style="width: 400px"
      >
        <el-carousel-item v-for="item in slides" :key="item.id">
          <div class="slide" :style="{ background: item.color }">{{ item.label }}</div>
        </el-carousel-item>
      </el-carousel>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const slides = [
  { id: 1, label: 'Slide 1', color: '#409eff' },
  { id: 2, label: 'Slide 2', color: '#67c23a' },
  { id: 3, label: 'Slide 3', color: '#e6a23c' },
  { id: 4, label: 'Slide 4', color: '#f56c6c' },
]

const activeIndex = ref(0)
const autoplay = ref(false)

function onChange(index: number) {
  activeIndex.value = index
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
.slide { height: 100%; width: 100%; display: flex; align-items: center; justify-content: center; color: white; font-size: 20px; }
</style>
