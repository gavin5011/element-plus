<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Steps Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-steps :active="stepsActive" data-testid="steps-basic"
        ><el-step title="A" /><el-step title="B" /><el-step title="C"
      /></el-steps>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Primary Interaction</h3>
      <el-button
        data-testid="steps-next"
        @click="stepsActive = (stepsActive + 1) % 3"
        >Next</el-button
      ><el-steps :active="stepsActive" data-testid="steps-interact"
        ><el-step title="P" /><el-step title="Q" /><el-step title="R"
      /></el-steps>
      <div data-testid="picked-value-display">
        Active: <span data-testid="picked-value">{{ stepsActive }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation</h3>
      <el-button
        data-testid="steps-toggle-direction"
        @click="
          stepsDir = stepsDir === 'horizontal' ? 'vertical' : 'horizontal'
        "
        >Dir:
        <span data-testid="state-indicator">{{ stepsDir }}</span></el-button
      ><el-steps
        :direction="stepsDir"
        :active="1"
        data-testid="steps-state-target"
        ><el-step title="1" /><el-step title="2"
      /></el-steps>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const stepsActive = ref(0)
const stepsDir = ref('horizontal')
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
