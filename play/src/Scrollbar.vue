<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Scrollbar Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-scrollbar data-testid="scrollbar-basic" height="200px" style="width: 300px; border: 1px solid #dcdfe6">
        <div v-for="n in 30" :key="n" class="row">Row {{ n }}</div>
      </el-scrollbar>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (scroll to bottom)</h3>
      <el-scrollbar
        data-testid="scrollbar-interact"
        height="200px"
        style="width: 300px; border: 1px solid #dcdfe6"
        @scroll="onScroll"
      >
        <div v-for="n in 30" :key="n" class="row">Row {{ n }}</div>
      </el-scrollbar>
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ scrollTop }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (orientation)</h3>
      <el-button data-testid="scrollbar-toggle-orientation" @click="horizontal = !horizontal">
        Toggle orientation: <span data-testid="state-indicator">{{ horizontal ? 'horizontal' : 'vertical' }}</span>
      </el-button>
      <el-scrollbar
        data-testid="scrollbar-state-target"
        :height="horizontal ? '120px' : '200px'"
        style="width: 300px; border: 1px solid #dcdfe6"
      >
        <div v-if="horizontal" style="width: 900px; white-space: nowrap">
          <span v-for="n in 30" :key="n" style="display: inline-block; padding: 8px 14px">Col {{ n }}</span>
        </div>
        <div v-else>
          <div v-for="n in 30" :key="n" class="row">Row {{ n }}</div>
        </div>
      </el-scrollbar>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const scrollTop = ref(0)
const horizontal = ref(false)

function onScroll({ scrollTop: t }: { scrollTop: number; scrollLeft: number }) {
  scrollTop.value = Math.round(t)
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
.row { padding: 6px 10px; border-bottom: 1px solid #f0f0f0; }
</style>
