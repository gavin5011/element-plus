<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">DateTimePicker Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-date-picker
        data-testid="datetimepicker-basic"
        v-model="basicValue"
        type="datetime"
        placeholder="Select date and time"
      />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Pick datetime)</h3>
      <el-date-picker
        data-testid="datetimepicker-interact"
        v-model="pickedValue"
        type="datetime"
        placeholder="Pick a datetime"
        clearable
      />
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue ? String(pickedValue) : '(none)' }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (single vs range)</h3>
      <el-button data-testid="datetimepicker-toggle-range" @click="isRange = !isRange">
        Toggle type: <span data-testid="state-indicator">{{ isRange ? 'range' : 'single' }}</span>
      </el-button>
      <el-date-picker
        v-if="!isRange"
        data-testid="datetimepicker-state-target"
        v-model="stateSingle"
        type="datetime"
        placeholder="Single datetime"
      />
      <el-date-picker
        v-else
        data-testid="datetimepicker-state-target"
        v-model="stateRange"
        type="datetimerange"
        range-separator="to"
        start-placeholder="Start datetime"
        end-placeholder="End datetime"
      />
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const basicValue = ref<Date | null>(null)
const pickedValue = ref<Date | null>(null)
const isRange = ref(false)
const stateSingle = ref<Date | null>(null)
const stateRange = ref<[Date, Date] | null>(null)
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>
