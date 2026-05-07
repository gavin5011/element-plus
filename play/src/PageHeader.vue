<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">PageHeader Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-page-header
        title="Back"
        content="Page Title"
        data-testid="page-header-basic"
      />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Primary Interaction</h3>
      <el-button data-testid="page-header-toggle-icon" @click="phIcon = !phIcon"
        >Toggle</el-button
      ><el-page-header
        :icon="phIcon ? null : undefined"
        content="Interact"
        data-testid="page-header-interact"
      />
      <div data-testid="picked-value-display">
        Icon:
        <span data-testid="picked-value">{{
          phIcon ? 'no-icon' : 'with-icon'
        }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation</h3>
      <el-button
        data-testid="page-header-cycle-content"
        @click="phContent = phContent === 'A' ? 'B' : 'A'"
        >Content:
        <span data-testid="state-indicator">{{ phContent }}</span></el-button
      ><el-page-header
        :content="phContent"
        data-testid="page-header-state-target"
      />
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const phIcon = ref(false)
const phContent = ref('A')
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
