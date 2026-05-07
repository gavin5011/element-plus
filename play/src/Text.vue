<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Text Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-text data-testid="text-basic">Default text</el-text>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Primary Interaction</h3>
      <el-button
        data-testid="text-cycle-type"
        @click="textType = textType === 'primary' ? 'success' : 'primary'"
        >Cycle</el-button
      ><el-text :type="textType" data-testid="text-interact"
        >{{ textType }} text</el-text
      >
      <div data-testid="picked-value-display">
        Type: <span data-testid="picked-value">{{ textType }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation</h3>
      <el-button
        data-testid="text-toggle-tag"
        @click="textTag = textTag === 'span' ? 'p' : 'span'"
        >Tag:
        <span data-testid="state-indicator">{{ textTag }}</span></el-button
      ><el-text :tag="textTag" data-testid="text-state-target"
        >{{ textTag }} element</el-text
      >
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const textType = ref('primary')
const textTag = ref('span')
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
