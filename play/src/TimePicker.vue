<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">TimePicker Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <div data-testid="timepicker-basic">
        <el-time-picker v-model="basicValue" placeholder="Select time" />
      </div>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Pick time)</h3>
      <div data-testid="timepicker-interact">
        <el-time-picker
          v-model="pickedValue"
          placeholder="Pick a time"
          clearable
        />
      </div>
      <div data-testid="picked-value-display">
        Value:
        <span data-testid="picked-value">{{
          pickedValue ? String(pickedValue) : '(none)'
        }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (12h vs 24h format)</h3>
      <el-button
        data-testid="timepicker-toggle-format"
        @click="use12h = !use12h"
      >
        Toggle format:
        <span data-testid="state-indicator">{{ use12h ? '12h' : '24h' }}</span>
      </el-button>
      <div data-testid="timepicker-state-target">
        <el-time-picker
          v-model="stateValue"
          :format="use12h ? 'hh:mm:ss A' : 'HH:mm:ss'"
          placeholder="State-variant time"
        />
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const basicValue = ref<Date | null>(null)
const pickedValue = ref<Date | null>(null)
const use12h = ref(false)
const stateValue = ref<Date | null>(null)
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
