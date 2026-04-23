<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">InputNumber Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-input-number
        data-testid="input-number-basic"
        v-model="basicValue"
        :min="0"
        :max="100"
        :step="1"
      />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (increment/decrement)</h3>
      <el-input-number
        data-testid="input-number-interact"
        v-model="pickedValue"
        :min="0"
        :max="100"
        :step="1"
      />
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (precision toggle)</h3>
      <el-button data-testid="input-number-toggle-precision" @click="highPrecision = !highPrecision">
        Toggle precision: <span data-testid="state-indicator">{{ highPrecision ? '2 decimals' : '0 decimals' }}</span>
      </el-button>
      <el-input-number
        data-testid="input-number-state-target"
        v-model="stateValue"
        :min="0"
        :max="100"
        :step="highPrecision ? 0.01 : 1"
        :precision="highPrecision ? 2 : 0"
      />
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const basicValue = ref(10)
const pickedValue = ref(0)
const stateValue = ref(5)
const highPrecision = ref(false)
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>
