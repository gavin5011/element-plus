<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">TimeSelect Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-time-select
        data-testid="timeselect-basic"
        v-model="basicValue"
        start="09:00"
        end="18:00"
        step="00:30"
        placeholder="Pick a time"
      />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Open → pick time)</h3>
      <el-time-select
        data-testid="timeselect-interact"
        v-model="pickedValue"
        start="09:00"
        end="18:00"
        step="00:30"
        placeholder="Pick one"
        clearable
      />
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue || '(none)' }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (24h/12h format toggle)</h3>
      <el-button data-testid="timeselect-toggle-format" @click="use24h = !use24h">
        Toggle format: <span data-testid="state-indicator">{{ use24h ? '24h' : '12h' }}</span>
      </el-button>
      <el-time-select
        data-testid="timeselect-state-target"
        v-model="stateValue"
        :start="use24h ? '09:00' : '9:00 AM'"
        :end="use24h ? '18:00' : '6:00 PM'"
        :step="use24h ? '00:30' : '00:30'"
        :format="use24h ? 'HH:mm' : 'h:mm A'"
        placeholder="State-variant"
      />
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const basicValue = ref('')
const pickedValue = ref('')
const stateValue = ref('')
const use24h = ref(true)
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>
