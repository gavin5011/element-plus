<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Result Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-result
        icon="success"
        title="Success"
        sub-title="Operation completed"
        data-testid="result-basic"
      />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Primary Interaction</h3>
      <el-button
        data-testid="result-toggle-icon"
        @click="resultIcon = resultIcon === 'success' ? 'warning' : 'success'"
        >Toggle</el-button
      ><el-result
        :icon="resultIcon"
        data-testid="result-interact"
        title="Interact"
      />
      <div data-testid="picked-value-display">
        Icon: <span data-testid="picked-value">{{ resultIcon }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation</h3>
      <el-button
        data-testid="result-cycle-title"
        @click="resultTitle = resultTitle === 'Done' ? 'Failed' : 'Done'"
        >Title:
        <span data-testid="state-indicator">{{ resultTitle }}</span></el-button
      ><el-result :title="resultTitle" data-testid="result-state-target" />
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const resultIcon = ref('success')
const resultTitle = ref('Done')
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
