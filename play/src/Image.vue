<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Image Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-image
        data-testid="image-basic"
        v-for="(src, i) in images"
        :key="`basic-${i}`"
        :src="src"
        lazy
        style="width: 120px; height: 120px; margin-right: 8px"
      />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (click thumbnail)</h3>
      <el-image
        data-testid="image-interact"
        v-for="(src, i) in images"
        :key="`interact-${i}`"
        :src="src"
        lazy
        style="width: 120px; height: 120px; margin-right: 8px; cursor: pointer"
        @click="pickIndex(i)"
      />
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedIndex === -1 ? '(none)' : `image-${pickedIndex}` }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (fit mode)</h3>
      <el-button data-testid="image-toggle-fit" @click="useCover = !useCover">
        Toggle fit: <span data-testid="state-indicator">{{ useCover ? 'cover' : 'contain' }}</span>
      </el-button>
      <el-image
        data-testid="image-state-target"
        :src="images[0]"
        :fit="useCover ? 'cover' : 'contain'"
        style="width: 200px; height: 120px; border: 1px solid #dcdfe6"
      />
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const images = [
  'https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg',
  'https://fastly.jsdelivr.net/npm/@vant/assets/leaf.jpeg',
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-1.jpeg',
]

const pickedIndex = ref(-1)
const useCover = ref(false)

function pickIndex(i: number) {
  pickedIndex.value = i
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>
