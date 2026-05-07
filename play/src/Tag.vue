<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Tag Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-tag data-testid="tag-basic">Default</el-tag>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Primary Interaction</h3>
      <el-button
        data-testid="tag-cycle-type"
        @click="tagType = tagType === 'success' ? 'warning' : 'success'"
        >Cycle</el-button
      ><el-tag :type="tagType" data-testid="tag-interact">{{ tagType }}</el-tag>
      <div data-testid="picked-value-display">
        Type: <span data-testid="picked-value">{{ tagType }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation</h3>
      <el-button
        data-testid="tag-toggle-effect"
        @click="tagEffect = tagEffect === 'light' ? 'dark' : 'light'"
        >Effect:
        <span data-testid="state-indicator">{{ tagEffect }}</span></el-button
      ><el-tag :effect="tagEffect" data-testid="tag-state-target">{{
        tagEffect
      }}</el-tag>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const tagType = ref('success')
const tagEffect = ref('light')
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
