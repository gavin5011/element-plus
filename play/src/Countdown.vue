<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Countdown Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-countdown :value="cdValue" data-testid="countdown-basic" />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Primary Interaction</h3>
      <el-button
        data-testid="countdown-reset"
        @click="cdValue = Date.now() + 60000"
        >Reset 60s</el-button
      ><el-countdown :value="cdValue" data-testid="countdown-interact" />
      <div data-testid="picked-value-display">
        Target: <span data-testid="picked-value">{{ cdValue }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation</h3>
      <el-button
        data-testid="countdown-toggle-format"
        @click="cdFormat = cdFormat === 'HH:mm:ss' ? 'mm:ss' : 'HH:mm:ss'"
        >Format:
        <span data-testid="state-indicator">{{ cdFormat }}</span></el-button
      ><el-countdown
        :value="cdValue"
        :format="cdFormat"
        data-testid="countdown-state-target"
      />
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const cdValue = ref(Date.now() + 60000)
const cdFormat = ref('HH:mm:ss')
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
