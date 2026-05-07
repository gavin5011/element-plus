<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Space Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-space data-testid="space-basic"
        ><el-button>A</el-button><el-button>B</el-button></el-space
      >
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Primary Interaction</h3>
      <el-button
        data-testid="space-toggle-size"
        @click="spSize = spSize === 'small' ? 'large' : 'small'"
        >Toggle</el-button
      ><el-space :size="spSize" data-testid="space-interact"
        ><el-button>X</el-button><el-button>Y</el-button></el-space
      >
      <div data-testid="picked-value-display">
        Size: <span data-testid="picked-value">{{ spSize }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation</h3>
      <el-button
        data-testid="space-cycle-direction"
        @click="spDir = spDir === 'horizontal' ? 'vertical' : 'horizontal'"
        >Dir: <span data-testid="state-indicator">{{ spDir }}</span></el-button
      ><el-space :direction="spDir" data-testid="space-state-target"
        ><el-button>1</el-button><el-button>2</el-button></el-space
      >
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const spSize = ref('small')
const spDir = ref('horizontal')
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
