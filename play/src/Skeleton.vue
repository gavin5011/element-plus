<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Skeleton Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-skeleton :rows="3" data-testid="skeleton-basic" />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Primary Interaction</h3>
      <el-button
        data-testid="skeleton-toggle-loading"
        @click="skLoading = !skLoading"
        >Toggle</el-button
      ><el-skeleton
        :loading="skLoading"
        :rows="3"
        data-testid="skeleton-interact"
        ><template #default><div>Loaded content</div></template></el-skeleton
      >
      <div data-testid="picked-value-display">
        Loading: <span data-testid="picked-value">{{ String(skLoading) }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation</h3>
      <el-button
        data-testid="skeleton-cycle-rows"
        @click="skRows = skRows === 3 ? 6 : 3"
        >Rows:
        <span data-testid="state-indicator">{{ skRows }}</span></el-button
      ><el-skeleton :rows="skRows" data-testid="skeleton-state-target" />
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const skLoading = ref(true)
const skRows = ref(3)
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
