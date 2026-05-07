<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Watermark Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-watermark content="WM" data-testid="watermark-basic"
        ><div style="height: 80px; width: 200px; background: #f0f0f0">
          Watermarked content
        </div></el-watermark
      >
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Primary Interaction</h3>
      <el-button
        data-testid="watermark-cycle-content"
        @click="wmContent = wmContent === 'WM' ? 'OK' : 'WM'"
        >Cycle</el-button
      ><el-watermark :content="wmContent" data-testid="watermark-interact"
        ><div style="height: 80px; width: 200px; background: #f0f0f0">
          Body
        </div></el-watermark
      >
      <div data-testid="picked-value-display">
        Content: <span data-testid="picked-value">{{ wmContent }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation</h3>
      <el-button
        data-testid="watermark-toggle-rotate"
        @click="wmRotate = wmRotate === 0 ? -45 : 0"
        >Rotate:
        <span data-testid="state-indicator">{{ wmRotate }}</span></el-button
      ><el-watermark
        :rotate="wmRotate"
        content="rotated"
        data-testid="watermark-state-target"
        ><div style="height: 80px; width: 200px">Body</div></el-watermark
      >
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const wmContent = ref('WM')
const wmRotate = ref(0)
</script>

<style scoped>
.demo-page {
  padding: 24px;
  font-family: system-ui;
}
section {
  margin-top: 16px;
  display: flex;
  gap: 16px;
  align-items: center;
  flex-wrap: wrap;
}
section h3 {
  width: 100%;
  margin-bottom: 8px;
  color: #606266;
}
</style>
