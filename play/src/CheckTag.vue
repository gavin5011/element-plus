<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">CheckTag Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-check-tag data-testid="check-tag-basic" v-model:checked="ctBasic"
        >Basic</el-check-tag
      >
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Primary Interaction</h3>
      <el-check-tag
        data-testid="check-tag-interact"
        v-model:checked="ctInteract"
        >Interact</el-check-tag
      >
      <div data-testid="picked-value-display">
        Checked:
        <span data-testid="picked-value">{{ String(ctInteract) }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation</h3>
      <el-button
        data-testid="check-tag-toggle-color"
        @click="ctType = ctType === 'primary' ? 'success' : 'primary'"
        >Type:
        <span data-testid="state-indicator">{{ ctType }}</span></el-button
      ><el-check-tag
        :type="ctType"
        data-testid="check-tag-state-target"
        :checked="true"
        >{{ ctType }}</el-check-tag
      >
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const ctBasic = ref(false)
const ctInteract = ref(false)
const ctType = ref('primary')
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
