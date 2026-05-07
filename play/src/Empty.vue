<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Empty Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-empty description="No data" data-testid="empty-basic" />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Primary Interaction</h3>
      <el-button
        data-testid="empty-toggle-text"
        @click="emptyDesc = emptyDesc === 'No data' ? 'Empty list' : 'No data'"
        >Toggle</el-button
      ><el-empty :description="emptyDesc" data-testid="empty-interact" />
      <div data-testid="picked-value-display">
        Desc: <span data-testid="picked-value">{{ emptyDesc }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation</h3>
      <el-button
        data-testid="empty-toggle-size"
        @click="emptySize = emptySize === 100 ? 200 : 100"
        >Size:
        <span data-testid="state-indicator">{{ emptySize }}</span></el-button
      ><el-empty
        :image-size="emptySize"
        data-testid="empty-state-target"
        description="state"
      />
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const emptyDesc = ref('No data')
const emptySize = ref(100)
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
