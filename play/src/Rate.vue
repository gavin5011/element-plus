<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Rate Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-rate
        data-testid="rate-basic"
        v-model="basicValue"
        :max="5"
      />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (click star)</h3>
      <el-rate
        data-testid="rate-interact"
        v-model="pickedValue"
        :max="5"
      />
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (half-star toggle)</h3>
      <el-button data-testid="rate-toggle-half" @click="allowHalf = !allowHalf">
        Toggle half-star: <span data-testid="state-indicator">{{ allowHalf ? 'half allowed' : 'whole only' }}</span>
      </el-button>
      <el-rate
        data-testid="rate-state-target"
        v-model="stateValue"
        :max="5"
        :allow-half="allowHalf"
      />
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const basicValue = ref(3)
const pickedValue = ref(0)
const stateValue = ref(3)
const allowHalf = ref(true)
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>
