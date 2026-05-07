<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Alert Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-alert title="Info alert" type="info" data-testid="alert-basic" />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Primary Interaction</h3>
      <el-button
        data-testid="alert-toggle-btn"
        @click="alertVisible = !alertVisible"
        >Toggle</el-button
      ><el-alert
        v-if="alertVisible"
        title="Toggleable"
        type="warning"
        data-testid="alert-interact"
      />
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation</h3>
      <el-button
        data-testid="alert-cycle-type"
        @click="alertType = alertType === 'success' ? 'error' : 'success'"
        >Cycle:
        <span data-testid="state-indicator">{{ alertType }}</span></el-button
      ><el-alert
        :type="alertType"
        data-testid="alert-state-target"
        :title="`alert-${alertType}`"
      />
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const alertVisible = ref(true)
const alertType = ref('success')
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
