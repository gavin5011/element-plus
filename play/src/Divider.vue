<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Divider Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <div>Top<el-divider data-testid="divider-basic" />Bottom</div>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Primary Interaction</h3>
      <el-button
        data-testid="divider-toggle-direction"
        @click="divDir = divDir === 'horizontal' ? 'vertical' : 'horizontal'"
        >Direction</el-button
      ><el-divider :direction="divDir" data-testid="divider-interact" />
      <div data-testid="picked-value-display">
        Dir: <span data-testid="picked-value">{{ divDir }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation</h3>
      <el-button
        data-testid="divider-cycle-content"
        @click="divContent = divContent === 'mid' ? 'end' : 'mid'"
        >Pos:
        <span data-testid="state-indicator">{{ divContent }}</span></el-button
      ><el-divider
        :content-position="divContent"
        data-testid="divider-state-target"
        >{{ divContent }}</el-divider
      >
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const divDir = ref('horizontal')
const divContent = ref('mid')
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
